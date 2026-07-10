# Planos de implementação

Gerado em 2026-07-10. Execute o plano abaixo na ordem interna indicada. O jogo não está em um repositório Git; por isso o plano usa hashes SHA-256 dos arquivos como verificação de alterações em vez de um commit.

## Ordem e status

| Plano | Título | Prioridade | Esforço | Dependência | Status |
|------|--------|------------|---------|-------------|--------|
| 001 | Evoluir City Void para uma experiência `.io` ampla, vibrante e competitiva | P1 | L | — | IN PROGRESS — etapas 1–8 concluídas |

Valores de status: `TODO`, `IN PROGRESS`, `DONE`, `BLOCKED (motivo)` ou `REJECTED (motivo)`.

## Dependências internas

O plano 001 é deliberadamente único, mas contém etapas dependentes. A sequência obrigatória é:

1. Base visual e arquitetura interna.
2. Índice espacial e desempenho.
3. Câmera dinâmica.
4. Cidade ampliada e bairros.
5. Combate entre buracos e renascimento.
6. Inteligência dos bots.
7. Interface, efeitos e otimização móvel.
8. Verificação final.

Não aumente o mapa antes de concluir o índice espacial. O algoritmo atual percorre todos os objetos e ficaria lento com centenas deles.

## Decisões consideradas e rejeitadas

- **Bloom e desfoque na tela inteira:** rejeitados porque recriariam o aspecto nublado que precisa ser removido e teriam custo alto em celulares.
- **Modelos ou texturas externas obrigatórias:** rejeitados para preservar o requisito de que o jogo executável permaneça em um único `index.html`.
- **Eliminação permanente ao ser engolido:** rejeitada porque deixaria o jogador assistindo ao restante de uma partida curta. O plano usa renascimento com penalidade.
- **Apenas aumentar `WORLD_W` e `WORLD_D`:** rejeitado porque produziria um mapa vazio ou lento, sem resolver variedade, busca espacial e comportamento dos bots.
