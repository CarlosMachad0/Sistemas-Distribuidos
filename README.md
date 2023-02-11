# Sistemas-Distribuidos

## Requisitos Funcionais
- rf1. O cliente submete um pedido armazenamento de dados no processo líder da camada de storage, e recebe um identificador para os dados.
- rf2. O cliente submete um pedido de processamento ao balanceador de carga, que será encaminhado para um dos processadores e recebe um identificador para o pedido, juntamente com o identificador do processador responsável pelo processamento.
- rf3. O cliente verifica o estado do pedido a qualquer momento junto do processador.
- rf4. O cliente obtém o resultado do processamento junto do storage, utilizando o identificador do pedido.

## Requisitos Não Funcionais
- rnf1. Os processadores devem fazer o broadcast de heartbeats periódicos com a informação dos seus recursos e tarefas. Desta forma, o balanceador obtém informação dos recursos disponíveis em cada processador e o coordenador determina quais são os processadores válidos (sem falhas).
- rnf2. Quando o balanceador arranca, deverá contactar o coordenador para obter a lista de processadores válidos. Nesta fase, o balanceador não conhece o endereço do coordenador atual.
- rnf3. Quando um coordenador deixa de receber heartbeats de um processador durante um período de tempo superior a 30 seg, deverá remover o respetivo processador da lista de processadores disponíveis. Posteriormente, notifica o processador com mais recursos, para resumir os pedidos pendentes do processor com falhas, e o balanceador para comunicar a falha de um dos processadores.
- rnf4. Quando um coordenador recebe um heartbeat do tipo "setup", vindo de um processador que não se encontra na lista, adiciona o processador e notifica o balanceador.
- rnf5. Os ids dos elementos e dos pedidos devem ser universais
- rnf6. O acesso aos recursos partilhados por várias threads têm de ser thread-safe
- rnf7. A comunicação unicast deverá ser realizada através do middleware RMI
- rnf8. A execução dos pedidos deverá ser FIFO ordering
- rfn9. Os processos da camada de storage garantem consistência eventual, onde o líder é eleito por um algoritmo de consenso
- rfn10. A comunicação multicast deverá garantir a integridade
- rfn11. A falha do coordenador pode ser detetada por qualquer processador, mas só é considerada definitiva por consenso por maioria
- rfn12. O sistema distribuído apenas considerar falhas do tipo fail-stop


