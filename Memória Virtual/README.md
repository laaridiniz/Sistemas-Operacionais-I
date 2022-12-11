<h1 align="center">🔸Memória Virtual🔸</h1>
<br id="topo">

## Conceito

<p align="justify">Dentro do ambiente de multiprogramação existe uma enorme quantidade de processos e quando todos esses processos não cabem na memória principal, esta precisa se valer de técnicas de processamento. Ou seja, para que a memória principal consiga dar conta de todos esses processos, existe a técnica da memória virtual, que garante maior eficiência a esses processos e ao funcionamento do computador como um todo.<br>
<br>
Essa técnica usa a memória secundária como uma “cache” para partes dos processos que não cabem na memória principal, permitindo que todos os processos possam utilizar a memória principal. Quem cria e gerencia essa memória virtual é o SO.<br>
<br>
Só são transportadas para a memória virtual as partes da memória principal que estão de fato sendo usadas pelos processos. Ou seja, temos duas vantagens principais:<br></p>

- Um processo pode executar sem ter todas as instruções e dados dentro da memória principal;
- O espaço de memória disponível ao programa pode exceder o tamanho da memória principal.

<p align="justify">Também utiliza o MMU (circuito dentro do processador) para conversão dos endereços lógicos em endereços físicos, considerando que um processo usa endereços virtuais e não físicos.<br>
<br></p>

<div align="center">
  <img src="Imagens/MMU.jpg" alt="esquema visual do funcionamento do MMU dentro do computador" width="80%" height="80%">
</div>

 <p align="center"> Funcionamento do MMU (IFRN).</p>
  <br>
  
→ [Voltar ao topo](#topo)

## Técnicas

<p align="justify"><b>PAGINAÇÃO:</b><br>
<br>
Consiste em quebrar os processos em páginas de tamanho fixo (p. ex. 4KB). Cada página contém partes do processo (do espaço de endereçamento do processo). Com isso, o espaço de endereçamento virtual é dividido em páginas virtuais.<br>
<br>
Obs.: Na paginação é possível misturar os tipos de informações, p. ex., códigos com textos, ou dados com pilhas etc.<br>
<br>
Dentro da paginação, existem as páginas (do lado do disco) e os frames (do lado da RAM). As páginas são as unidades de tamanho fixo no dispositivo secundário, ao passo que os frames consistem nas unidades correspondentes na memória física (RAM).<br>
<br>
Paginação sob demanda: as páginas serão criadas quando o sistema solicitar.<br>
<br>
Obs.: Page Fault => falta de página. Quando uma página não está na RAM é referenciada. Usa uma trap para carregar ou substituir uma página. (TRAP é o nome dado ao sinal de interrupção de software dado a CPU para que ela interrompa a execução de um processo para executar outro. O processo interrompido tem seus dados armazenados na memória para que seja executado posteriormente.)<br>
<br>
Obs. 2: Tabela de páginas => estrutura para mapear uma página ao frame correspondente. Cada processo tem uma. É uma espécie de índice de processos e também ocupa um espaço na memória.<br>
<br>
A busca do endereço pode ser sequencial ou binária, mas qualquer uma delas ainda é lenta, uma vez que ocorre um overhead (sobrecarga) do gerenciador de memória. O SO fica sobrecarregado em virtude das rotinas de gerenciamento dele próprio.<br>
<br>
Para encontrar o endereço físico, será essencial encontrar as seguintes informações:<br>
<br>
P = número da página<br>
<br>
D = deslocamento da página<br>
<br>Com esses dois valores teremos o chamado offset e conseguiremos definir o endereço de memória físico.<br>
<br></p>

<p align="justify"><b>EXEMPLO DE PAGINAÇÃO:</b><br>
<br>
Quando um programa executa a instrução mov REG, 20500, por exemplo, significa que ele deseja copiar o conteúdo do endereço de memória 20500 para o registrador REG.<br>
<br>
Partindo do esquema a seguir, cálculo do deslocamento será feito da seguinte forma:<br>
<br></p>

<div align="center">
  <img src="Imagens/enderecamentos.jpg" alt="ilustração da forma como são referenciados os endereços virtuais nos endereços físicos" width="80%" height="80%">
</div>

 <p align="center"> Referenciamento de páginas e frames (IFRN).</p>
  <br>

Deslocamento = Endereço virtual - Endereço virtual do 1º byte da página <br>
Deslocamento = 20500 - 20480 = 20<br>
<br>
Obs.: No esquema, o endereço virtual está contido no espaço 20K-24K, logo, o primeiro byte dessa página será 20480 (convertendo 20Kb em bytes).<br>
<br>
Endereço físico = Endereço do 1º byte do frame + deslocamento<br>
Endereço físico = 12288 + 20 = 12308<br>
<br>
Obs.: A página em questão está sendo referenciada no frame 3 (12K-16K), então, convertendo 12Kb em bytes teremos 12288 bytes.<br>

As tabelas podem ser armazenadas:<br></p>

- Em um array de registradores, se a memória for pequena (são mantidas no hardware);
- Na própria RAM, gerenciada pelo MMU, que utiliza 1 ou 2 registradores;
- Em uma memória cache no MMU (memória associativa), usada para melhorar o desempenho da tabela na RAM.

<p align="justify">Se um processo que não está na memória física (mas na MV) precisa ser utilizado e a memória física não tem mais espaço, o SO precisa usar algum algoritmo de substituição, p. ex.:<br></p>

a)	FIFO = o primeiro a entrar é o primeiro a sair (fila);<br>
<br>
b)	LRU = exclui a página que não é referenciada há mais tempo (pilha);<br>
<br>
c)	Optimal = exclui a página que levará mais tempo para ser novamente necessária (pilha);<br>
<br>
d)	Clock-FINUFO = tem como base valores aproximados dos reais quanto ao último acesso à página (implementação simplificada da LRU);<br>
<br>
e)	Segunda chance = a página escolhida para sair é a que tem os bits de acesso e de modificação zerados.<br>

→ [Voltar ao topo](#topo)

<p align="justify"><b>SEGMENTAÇÃO:</b><br>
<br>
Consiste em blocos de tamanho arbitrário chamados de segmentos que contêm informações do mesmo tipo. Aqui, o espaço de endereçamento é quebrado em vários espaços (textos, códigos, dados etc.).<br>
<br>
Um programa é dividido logicamente em sub-rotinas e estruturas de dados, que são alocados em segmentos na memória principal. <br>
<br></p>

<div align="center">
  <img src="Imagens/segmentacao.jpg" alt="ilustração da alocação de segmentos na memória principal" width="80%" height="80%">
</div>

 <p align="center"> Segmentação da memória (IFRN).</p>
  <br>

<p align="justify">A segmentação permite uma relação entre a lógica do programa e a sua divisão na memória. Além disso, é importante destacar que a definição dos segmentos é realizada pelo compilador e que o tamanho do segmento pode ser alterado durante a execução do programa.<br>
<br>
Obs.: O mecanismo de mapeamento é semelhante ao da paginação, neste caso, os segmentos são mapeados através de tabelas de segmentos. Cada processo possui sua própria tabela de segmentos.<br>
<br>
Vantagem: se a informação consistir em texto por exemplo, consigo dar um comando apenas de leitura, que afetará somente aquele segmento, sem influenciar nos demais.
Muitos SOs misturam essas duas técnicas para ter as vantagens de todas elas.<br>
<br>
<b>IMPORTANTE:</b><br>
<br>
Paginação: invisível ao programador, serve para prover um espaço maior de endereçamento. Memória dividida em páginas de igual tamanho, com qualquer conteúdo.<br>
<br>
Segmentação: em geral visível ao programador, serve para organizar programas e dados, associando atributos de privilégio e proteção a instruções e dados. Os segmentos de um programa residem no disco. Apenas segmentos em uso são carregados na memória. O tamanho de um segmento não é fixo.<br></p>

→ [Voltar ao topo](#topo)

## Referências

https://www.ime.usp.br/~song/mac344/slides07-virtual-memory.pdf <br>
http://www.ic.uff.br/~boeres/slidesSOI/SOSI-aula5-memoriavirtual-completo.pdf <br>
https://docente.ifrn.edu.br/tadeuferreira/disciplinas/2015.2/sistemas-operacionais/Aula16.pdf <br>
https://www.to-convert.com/pt/informatica/converter-kilobyte-para-byte.php <br>
MACHADO, Francis B; MAIA, Luiz P. Arquitetura de Sistemas Operacionais. 4. ed. Rio de Janeiro: LTC, 2007. 305 p. ISBN 978-85-216-1548-4.
