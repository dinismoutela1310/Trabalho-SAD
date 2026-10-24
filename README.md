Versão 1.0
- Modelo lógico base feito
- As distribuições de cada posto neste momento foram arbitrárias e não refletem os tempos recolhidos
- Pontos físicos para a animação 2d/3d definidos, mas sem representar ainda perfeitamente a realidade

A lógica de waiting bay foi implementada da seguinte forma:
O carro 1 chega ao Posto de Recolha e tem um Delay de X segundos nesse posto. O carro 2 acaba o pagamento e fica em fila de espera para o Posto de Recolha, onde terá um delay de Y segundos. 
Se (Delay X - Tempo passado do Carro 1 no Posto de recolha) > (Delay Y), então o carro 1 avança para a waiting bay e ficará lá até receber o pedido, enquanto que o carro 2 avança para o Posto de Recolha.
Não sei se é a melhor forma de fazer isto por isso se tiverem sugestões força ;)
