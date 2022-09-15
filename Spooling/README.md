<h1 align="center">🔸Spooling🔸</h1>
<p align="center">[Em construção]</p>

## Conceito

<p align="justify"><i>Spooling</i> (Simultaneous Peripheral Operation On-line) é uma técnica que surgiu no final dos anos 1950 para aumentar o grau de concerrência e a eficiência dos sistemas operacionais.<br>
<br>
Obs.: a ideia de concorrência está diretamente ligada à possibilidade de o processador executar várias tarefas ao mesmo tempo, permitindo que vários programas sejam executados concorrentemente pelo sistema operacional.<br>
<br>
Antes os programas eram submetidos um a um ao processamento pelo operador, isto porque, como a velocidade de operação dos dispositivos de E/S é muito menor que a do processador, era comum que a CPU permanecesse ociosa enquanto esperava os programas e dados de entrada ou o término de uma impressão.<br>
<br>
O <i>spooling</i> é executado de modo parecido com o <i>buffering</i>, a diferença é que o primeiro utiliza uma área do disco enquanto processos são executados concorrentemente, ao passo que o segundo utiliza uma área da memória principal.
</p>

## Funcionamento

<p align="justify">A solução encontrada então foi armazenar os vários programas e seus dados (jobs) em uma fita magnética e, em seguida, submetê-los a processamento. Com isso, o processador foi capaz de executar sequencialmente cada job, diminuindo o tempo de processamento e transição entre eles.</p>

## Referências

<p>
https://www.youtube.com/watch?v=HpSi_W3x07I <br>
MACHADO, Francis B; MAIA, Luiz P. Arquitetura de Sistemas Operacionais. 4. ed. Rio de Janeiro: LTC, 2007. 305 p. ISBN 978-85-216-1548-4.
