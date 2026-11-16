Versão 1.0
Modelo lógico base feito
As distribuições de cada posto neste momento foram arbitrárias e não refletem os tempos recolhidos
Pontos físicos para a animação 2d/3d definidos, mas sem representar ainda perfeitamente a realidade
A lógica de waiting bay foi implementada da seguinte forma: O carro 1 chega ao Posto de Recolha e tem um Delay de X segundos nesse posto. O carro 2 acaba o pagamento e fica em fila de espera para o Posto de Recolha, onde terá um delay de Y segundos. Se (Delay X - Tempo passado do Carro 1 no Posto de recolha) > (Delay Y), então o carro 1 avança para a waiting bay e ficará lá até receber o pedido, enquanto que o carro 2 avança para o Posto de Recolha. Não sei se é a melhor forma de fazer isto por isso se tiverem sugestões força ;)

Versão 1.1
25/10 - 23:00 
No bloco Pedido2 acrescentei em On exit isto: agent.tempoRecolhaTotal = agent.DelayRecolha; que faltava e existia no Pedido1. 
Fiz o statechart no agent Carro, com vários estados ligados por transições de mensagem e nos blocos do main coloquei por exemplo agent.statechart.receiveMessage("pedir") no On enter delay do Pedido1. Segundo o claude, nesta fase só serve de base para o comportamento dos carros, e a seguir podemos acrescentar paciência, avarias e perfis de condutor.

Versão 1.2
26/10/26 - 17:00 fim Tomás 
Alteração da Condição de desistência para um teste de sensibilidade em vez de um valor estático (função DesistenciaFilaEntrada). Este teste dá a probabilidade de alguém desistir face a fila, e tem valores para que com 5 carros na filaEntrada a probabilidade de desistir seja 10% e com 10 seja 50% Criação de uma variável desiste no agente Carro para facilitar a expressão de se desiste ou não Criação de duas funções, filaEntrada e filaTotal, que consideram a fila que um condutor vê antes de entrar no drive thru e a fila total (filaEntrada + Waiting Bay) e representação destas no gráfico Adição de Uma queue logo depois do primeiro bloco para resolver um problema Adição de novos pontos e caminhos e alteração do esquema de forma ao carro ser gerado no novo caminho "estrada", para, se houver desistência, haver um local onde possamos ver o caarro vermelho

Versão 1.3
26/10/26 - 23:59
Statecharts com mensagens completos
Mudança da cor de um retângulo no tejadilho do carro de acordo com o estado (não é possível mudar a cor do carro)
Colocação de 3 lugares específicos na Waiting Bay
Fecho do ciclo com os carros a terminar na estrada

Versão 1.4
27/10/26 14:59
Implementação dos blocos de restrictedAreaStart e restrictedAreaEnd em cada um dos postos para evitar o erro do Anylogic tentar "empurrar" entidades para postos que já estavam na capacidade máxima de utilização/fila de espera
Recolha e visualização dos KPI:
- Lead Time
- Average Queue Length per Stage
- Average Waiting Time per Stage

Versão 1.5
27/10/26 18h
Gráfico de Clientes perdidos: Criei variável nChegadas, nBalking e nServidos. A %Blaking mostra os carros que nem chegam a entrar no restaurante e vão embora assim que veem a fila cheia à entrada, o Throughput mede a velocidade real a que a equipa entrega os pedidos. O objetivo é quando o Throughput bate no teto e não consegue andar mais rápido, a fila acumula logo e a curva do Balking dispara. É este gráfico que vai mostrar a quantidade de clientes que estamos a perder nas horas de ponta.

Versão 1.6
15/11/26 23h
Waiting Time total: criada a Statistics discreta filaTotalTempo, alimentada no On enter do SaídaCarros com a soma esperaPedido + esperaPagamento + esperaRecolha, para comparar com as três esperas por estágio. Corrigido o seizePagamento, que não tinha pool associado, e passa a usar FuncionariosPagamento (necessário para a utilização do pagamento). Utilização: a utilização dos postos é lida dos três pools de funcionários (FuncionariosPedido, FuncionariosPagamento, FuncionariosRecolha) com utilization(), e mede a ocupação do staff, que coincide com a da janela enquanto houver um funcionário por posto. Warm-up: criado o parâmetro tWarmup e o evento eventoWarmup, que faz reset das estatísticas de fila e espera, do lead time, da utilização dos pools e dos contadores nChegadas, nBalking e nServidos, para que as médias só contem o período estável. Decisão de âmbito: o reneging (KPI 6 e pergunta 6 da proposta) fica de fora, porque a pista é FIFO e quem entra não consegue sair; a perda de clientes é medida só pelo balking. Removida a variável nReneging.

Versão 1.7
16/11/26 12h45
Definição das distribuições para os tempos de espera/taxa de chegadas. Correção de pequeno erro no WarmUp (a função statsUtilization.reset() não existia nas pools, substituí por resetStats()).
