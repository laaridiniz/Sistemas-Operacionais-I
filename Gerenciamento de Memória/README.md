<h1 align="center">🔸Gerenciamento de Memória🔸</h1>

## Noções preliminares

O sistema operacional tem duas funções principais:

- Ser a interface que facilita a comunicação do usuário com o computador;
- Ser um administrador de recursos (saber quando deve alocar um determinado recurso para um programa e quando deve retirar um recurso de outro programa).

<p align="justify">Um processo é um programa em execução que possui um processador. Esse processador é compartilhado de maneira que esse processo possa usar de forma otimizada o processador entre os vários processos (programas em execução).<br></p>


## Conceito

<p align="justify">Em se tratando de sistemas multiprogramáveis, caracterizados pelo compartilhamento de recursos entre usuários, surge a necessidade de um método de gerenciamento de recursos, mais especificamente, de gerenciamento de memória. Sendo assim, o gerenciamento de memória cuida do controle de quais partes da memória estarão em uso e quais não estarão.<br>
<br>
Os programas atuais podem ser muito grandes, sendo incapazes de ser completamente armazenados na memória cache. Então, com o gerenciamento de memória, passou a ser possível realocar espaços de memória entre memória principal (RAM) e memória secundária (HD), de acordo com as necessidades dos processos.<br>
<br>
Em um ambiente de multiprogramação, o SO deve proteger as áreas de memória ocupadas por cada processo, além da área onde reside o próprio sistema. Caso um programa tente realizar algum acesso indevido à memória, o sistema de alguma forma deve impedi-lo. Apesar de a gerência de memória garantir a proteção de áreas da memória, mecanismos de compartilhamento devem ser oferecidos para que diferentes processos possam trocar dados de forma protegida.<br></p>


## Etapas 

<p align="justify">O gerenciamento de memória é dividido nas seguintes etapas:<br>
<br>
- Partição da memória: divide a memória principal em várias partições diferentes, de maneira que cada uma delas fique alocada para determinada partição. Em cada partição poderá haver mais de um job/tarefa na fila.<br>
<br>
- Proteção dos processos: é feita por 2 registradores, um que armazena a base e outro que armazena o limite, para que um processo não invada o limite de outro processo. A CPU adiciona o valor base ao endereço e verifica se o endereço é maior ou igual ao limite. P. ex.: se o usuário tem um programa de 40KB e esse programa foi armazenado no endereço 20 da memória principal, seria necessário somar esses válores, chegando ao resultado 60. Ou seja, 60 seria o endereço que efetivamente o processo utilizará. Os processos só utilizam endereços lógicos (que vão de 0 ao número máximo correspondente ao tamanho do processo). Nesse exemplo, o 20 seria a base e o 60 seria o limite.<br>
</p>

## MMU (_Memory Management Unit_)

<p align="justify">Considerando que o ambiente de multiprogramação utiliza endereços lógicos, é necessário fazer a conversão desses endereços em endereços físicos (ou endereços físicos reais). E o circuito responsável por essa conversão é o MMU.<br>
</p>

## Tipos de partições

<p align="justify">Existem 2 tipos de memórias particionadas:<br>
<br>
a) Partições fixas (alocação estática): são determinadas no momento do boot do sistema.<br>
- Tamanho e número de partições são fixos;<br>
- Tendem a desperdiçar memória;<br>
- Mais simples.<br>
<br></p>

<div align="center">
  <img src="Imagens/particoes-fixas.jpg" alt="ilustração partições fixas" width="80%" height="80%">
</div>
  
<p align="center">Fonte: ICMC - USP</p>
<br>

<p align="justify">
b) Partições variáveis (alocação dinâmica): ocorrem durante o tempo de execução dos programas.<br>
- Tamanho e número de partições variam;<br>
- Otimiza a utilização da memória, mas complica a alocação e a liberação;<br>
- As partições são alocadas dinamicamente.<br>
- < fragmentação interna<br>
- > fragmentação externa<br>
<br>
</p>

<div align="center">
  <img src="Imagens/part-variveis.jpg" alt="ilustração partições variáveis" width="80%" height="80%">
</div>
  
<p align="center">Fonte: PUC-Rio</p>


## Swapping

<p align="justify">Nesse momento é necessário mencionar a questão do swapping, ou seja, a transferência de dados e partições entre a memória principal e a memória secundária. Como nem tudo cabe na memória principal, reservam-se partes que não estão sendo manuseadas em uma área de swapping, utilizada para fazer essa permuta.<br>
<br>
Swap-in = transferência do disco para a memória principal<br>
<br>
Swap-out = transferência da memória principal para o disco<br>
<br></p>

## Estruturas de gerenciamento de memória

a) Bitmap (mapa de bit):
- A memória é dividida em unidades de alocação;
- Cada unidade pode conter vários KB;
- Cada unidade corresponde a um bit no bitmap: 0 -> livre / 1 -> ocupado

b) Lista encadeada:
- Mantém uma lista ligada de segmentos de memória livres e alocados
- A lista contém o processo (P), o endereço de início e o endereço final
- O H denota Hole, a área de memória que não está ocupada. P. ex.: H 5 3 -> existe uma área vaga a partir do endereço 5 por 3 posições.

<br>

<div align="center">
  <img src="Imagens/bitmap-lista.jpg" alt="demonstração gráfica do bitmap e da lista encadeada" width="80%" height="80%">
</div>
  
<p align="center">Fonte: PUC-Rio</p>

## Algoritmos de alocação

Há três formas de alocar uma área livre para um processo:

a) Melhor escolha: escolher a área que mais se encaixa para o processo. Busca a lista inteira e toma a menor partição;

b) Pior escolha: inversamente à melhor escolha, busca a lista inteira e toma a maior partição;

c) Primeira escolha: o processo é alocado no primeiro espaço que couber.

<div align="center">
  <img src="Imagens/alocacao.jpg" alt="alocação de memória livre" width="80%" height="80%">
</div>

<p align="center">Fonte: ICMC - USP</p>

## Referências

http://www-di.inf.puc-rio.br/~endler/courses/inf1019/transp/aulas-teoricas/cap-4.pdf<br>
http://wiki.icmc.usp.br/images/c/c7/Aula10.pdf<br>
https://www.youtube.com/watch?v=TwlIiA1HhT4<br>
https://www.youtube.com/watch?v=Q8ZqjEafmNc<br>
https://www.youtube.com/watch?v=9AK_1gqEfkQ<br>
MACHADO, Francis B; MAIA, Luiz P. Arquitetura de Sistemas Operacionais. 4. ed. Rio de Janeiro: LTC, 2007. 305 p. ISBN 978-85-216-1548-4.
