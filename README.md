## Descrição do Problema

O transporte aéreo de cargas no Brasil opera sob uma topologia predominantemente *Hub-and-Spoke*, concentrando o fluxo logístico em poucos aeroportos centrais (hubs) que interconectam terminais regionais e portões internacionais. Embora eficiente em condições normais de operação, essa alta centralização gera vulnerabilidades sistêmicas: panes operacionais, interrupções meteorológicas ou paralisações nesses hubs podem fragmentar a rede e interromper o abastecimento de insumos essenciais em diversas regiões do país.

Este projeto modela a rede de transporte cargueiro brasileiro a partir de dados reais de voos regulares ativos (VRA/ANAC) como um grafo direcionado e ponderado pela frequência de operações. O objetivo do software é avaliar a robustez estrutural da malha e planejar desvios logísticos automáticos em cenários de falha, respondendo a duas questões centrais:

1. **Vulnerabilidade Estrutural:** Quais aeródromos e rotas atuam como pontos únicos de falha cuja interrupção isola componentes da rede (pontos de articulação e pontes estruturais)?
2. **Contingência Operacional:** Diante do fechamento imprevisto de um hub central crítico, qual é a rota de menor custo/tempo alternativa viável para manter a conexão entre polos de origem e destino?

### Metodologia e Algoritmos

- **Modelagem do Grafo:** Grafo direcionado ponderado $G = (V, E)$, onde os vértices $V$ representam os aeródromos e as arestas direcionadas $E$ representam rotas ativas com peso equivalente ao fluxo/capacidade mensal de voos.
- **Identificação de Vulnerabilidades (Tarjan):** Aplicação de busca em profundidade ($DFS$) com tempos de descoberta e menores ancestrais alcançáveis ($low$) em complexidade $O(V + E)$ para mapear pontos de articulação e pontes.
- **Roteamento e Contingência (Dijkstra):** Algoritmo de caminho mínimo utilizando fila de prioridade (*min-heap*) em $O((V + E) \log V)$ para determinar trajetos nominais e recalcular dinamicamente rotas alternativas desviando de nós em pane.
