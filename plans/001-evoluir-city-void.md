# Plano 001: Evoluir City Void para uma experiência `.io` ampla, vibrante e competitiva

> **Instruções para o executor**: Leia este plano inteiro antes de alterar arquivos. Execute as etapas na ordem. Ao terminar cada etapa, faça a verificação indicada. Se ocorrer uma condição da seção “PARE”, interrompa e relate o problema; não improvise. Ao concluir, altere o status deste plano em `plans/README.md` para `DONE`.
>
> **Verificação de deriva — execute primeiro**:
>
> ```powershell
> (Get-FileHash index.html -Algorithm SHA256).Hash
> (Get-FileHash DESIGN.md -Algorithm SHA256).Hash
> ```
>
> O estado usado para este plano possui os hashes:
>
> - `index.html`: `0E446E5C19F7775C59F30F2813210675B424D22F46C3E39F7572DBAC2CDF1E75`
> - `DESIGN.md`: `A6E91A7AB9367C2F0E5AC1D90BB168D093BC0D71C0249A8196476F8F87C7FD81`
>
> Se os hashes forem diferentes antes da primeira alteração, compare o código atual com os trechos em “Estado atual”. Se funções ou constantes citadas tiverem mudado, PARE e peça atualização do plano.

## Status

- **Prioridade**: P1
- **Esforço**: L — várias etapas, estimativa grosseira de múltiplos dias
- **Risco**: HIGH — altera câmera, mundo, colisões, IA, renderização e interface
- **Depende de**: nenhum plano externo; respeitar as dependências internas
- **Categoria**: direction / perf / gameplay / visual
- **Planejado em**: projeto sem Git, 2026-07-10; hashes registrados acima

## Progresso de execução

- **Etapa 1 concluída em 2026-07-10:** configurações centralizadas, paleta vibrante documentada, névoa distante, iluminação com maior contraste, materiais toon, perfis visual alto/móvel e geometrias compartilhadas.
- **Etapa 2 concluída em 2026-07-10:** `SpatialGrid`, consultas locais para absorção e bots, `CANNON.SAPBroadphase`, métricas `?debug=1`, limite/reuso de partículas e verificação de desempenho.
- **Etapa 3 concluída em 2026-07-10:** câmera ancorada ao jogador, zoom proporcional ao raio, amortecimento independente de FPS, raycasting móvel e luz/sombras acompanhando o jogador.
- **Etapa 4 concluída em 2026-07-10:** mundo `180×180`, cinco bairros, 520 objetos, catálogo de 36 tipos, progressão por raio mínimo, novas sementes, modelos compartilhados e água no limite externo.
- **Etapa 5 concluída em 2026-07-10:** PvP com vantagem mínima de 15%, bônus limitado, penalidade de crescimento, animação de derrota, renascimento seguro em 3 segundos e proteção branca por 2 segundos.
- **Etapa 6 concluída em 2026-07-10:** cinco personalidades, estados `FORAGE/HUNT/FLEE/WANDER`, prioridade de fuga, reservas de alvo, separação entre bots e intervalo mínimo entre decisões.
- **Etapa 7 concluída em 2026-07-10:** minimapa, feed de eliminações, anéis de alvo/ameaça, seta de perigo, próximo desbloqueio, tráfego, pedestres, barcos, vegetação, rodas, aura e sucção aprimorada.
- **Etapa 8 concluída em 2026-07-10:** perfis `HIGH/MEDIUM/LOW`, seleção inicial por capacidade, redução automática após 4 segundos abaixo de 30 FPS, limites dinâmicos de sombras/pixel ratio/partículas e listas dedicadas de entidades animadas.
- **Refinamento visual concluído em 2026-07-10:** skyline com hotéis, apartamentos e torres comerciais, modelos mais suaves, fachadas detalhadas, 174 pessoas visíveis e densidade elevada para 520 objetos.
- **Próxima ação:** iniciar pela Etapa 9, ganchos de teste e verificação completa. Não repetir as Etapas 1–8.
- **Verificação registrada:** 59 FPS em desktop e 60 FPS em perfil móvel no ambiente de teste, sem erros de console; busca espacial com média de 1 candidato para aproximadamente 90 objetos ativos.
- **Verificação da câmera:** raio `1,9 → 6` alterou altura/distância de `38,4/37,3 → 63,0/66,0`; quatro extremos permaneceram enquadrados; mouse e toque moveram o jogador sem erros.
- **Verificação da cidade:** todos os bairros atingiram suas metas (`105/130/100/110/75`), 36 tipos apareceram, reinício muda a semente e recria 520 objetos; 18 prédios altos e 174 pessoas foram contabilizados.
- **Verificação PvP:** maior engoliu menor; menor e vantagem de 10% foram bloqueados; proteção bloqueou colisão; bônus inicial foi 20; crescimento da vítima caiu 35%; contagem real passou `3 → 2 → renascimento`, com proteção ativa e layout móvel sem overflow.
- **Verificação da IA:** teste local com as bibliotecas cacheadas confirmou cinco personalidades, estados de fuga, caça, coleta e exploração, separação não nula, 58 FPS em perfil móvel e nenhum erro. Reavaliações receberam intervalo mínimo de 160 ms para evitar uso excessivo.
- **Verificação do feedback:** perfil móvel manteve 59 FPS com 107 entidades móveis; minimapa, feed, anel vermelho, seta de ameaça e próximo desbloqueio funcionaram sem overflow. Movimento reduzido zerou balanço de árvores, passos e rotação da aura.
- **Verificação da qualidade adaptativa:** os três níveis respeitaram pixel ratio `1,75/1,4/1,1`, sombras `2048/1024/OFF` e limites de `150/80/32` partículas. Queda simulada reduziu uma vez de `HIGH` para `MEDIUM`; desktop e móvel mantiveram 60 FPS sem erros ou overflow.
- **Verificação do refinamento visual:** perfil móvel manteve 60 FPS no centro detalhado, sem redução automática de qualidade, com 337 draw calls, layout sem overflow e zero erros de console.

## Por que isso importa

O jogo atual demonstra a mecânica básica, mas a câmera fixa, o mapa de `58 × 82`, os 92 objetos e a ausência de colisão entre buracos limitam a sensação de escala e competição. A névoa azul e a luz ambiente forte também reduzem contraste e deixam as cores pastéis. Ao final deste plano, o jogador será acompanhado por uma câmera proporcional ao crescimento, explorará bairros maiores e variados, poderá engolir adversários menores e enfrentará bots que coletam, caçam e fogem, mantendo desempenho aceitável em celulares.

O produto deve continuar se chamando **City Void**. Não copiar nomes, arte, sons ou interface proprietária de outros jogos; usar apenas convenções gerais do gênero `.io`.

## Estado atual

### Arquivos e responsabilidades

- `index.html` — todo o código executável: CSS, HUD, cena Three.js, física Cannon.js, geração da cidade, controles, bots e regras.
- `DESIGN.md` — direção visual e tokens documentados; precisa refletir a nova aparência vibrante.
- `PRODUCT.md` — propósito e acessibilidade; não precisa ser alterado neste plano.

### Evidências importantes

`index.html:463-465` define uma partida de 120 segundos e um mundo pequeno:

```js
const GAME_DURATION = 120;
const WORLD_W = 58;
const WORLD_D = 82;
```

`index.html:548-553` cria névoa próxima e câmera fixa:

```js
scene.background = new THREE.Color(0xa8dff0);
scene.fog = new THREE.Fog(0xa8dff0, 62, 112);
camera = new THREE.PerspectiveCamera(47, innerWidth / innerHeight, 0.1, 180);
camera.position.set(0, 49, 49);
camera.lookAt(0, 0, -7);
```

`index.html:575-585` usa luz ambiente alta, que achata o contraste:

```js
scene.add(new THREE.HemisphereLight(0xe8faff, 0x40694a, 1.18));
const sun = new THREE.DirectionalLight(0xfff0cd, 1.15);
```

`index.html:599-645` cria 12 casas, 26 árvores, 20 postes, 24 pedestres e 10 carros. A cidade é determinística e usa uma única distribuição.

`index.html:980-1003` faz cada bot filtrar e ordenar a lista completa de objetos para escolher um destino.

`index.html:1006-1026` verifica absorção apenas contra `destructibles`; buracos nunca engolem buracos:

```js
function checkAbsorption() {
  destructibles.forEach(obj => {
    // jogador ou bot tenta engolir apenas o objeto da cidade
  });
}
```

### Convenções que devem ser preservadas

- Código executável inteiro em `index.html`, separado por comentários de seção.
- Funções e variáveis em inglês; textos apresentados ao usuário em português.
- Controles por mouse, toque, WASD e setas.
- Partida baseada em `performance.now()` com duração real de 120 segundos.
- Respeitar `prefers-reduced-motion`.
- Sons somente após interação do usuário e com botão de desligar.
- Usar Three.js e Cannon.js pelos CDNs já declarados.
- HUD escuro, legível e compacto; não encobrir a ação em telas pequenas.

### Direção visual obrigatória

O cenário físico é “uma cidade arcade em um dia ensolarado, vista como um brinquedo urbano colorido”. A nova paleta deve ser documentada em OKLCH no `DESIGN.md` e convertida para valores aceitos pelo Three.js no script. Usar céu ciano vivo, vegetação esmeralda, asfalto escuro, faixas amarelas e edifícios em coral, cobalto, violeta, turquesa e amarelo. Evitar névoa próxima, tons lavados, bloom global, gradientes decorativos e excesso de brilho.

## Comandos necessários

| Finalidade | Comando | Resultado esperado |
|---|---|---|
| Listar arquivos | `rg --files` | inclui `index.html`, `PRODUCT.md`, `DESIGN.md` e `plans/*` |
| Validar sintaxe JS | comando PowerShell abaixo | imprime `JS_SYNTAX_OK` |
| Conferir recursos | `rg -n "updateCamera|checkHoleVsHole|respawnHole|SpatialGrid|DISTRICTS" index.html` | encontra todos os cinco sistemas ao final |
| Conferir duração | `rg -n "GAME_DURATION = 120" index.html` | exatamente uma ocorrência |
| Conferir CDNs | `rg -n "three.min.js|cannon.min.js" index.html` | duas ocorrências, uma para cada biblioteca |

Validador de sintaxe reutilizável:

```powershell
@'
const fs = require('fs');
const html = fs.readFileSync('index.html', 'utf8');
const match = html.match(/<script>\s*('use strict';[\s\S]*?)<\/script>/);
if (!match) throw new Error('Script principal não encontrado');
new Function(match[1]);
console.log('JS_SYNTAX_OK');
'@ | node -
```

## Ferramentas sugeridas ao executor

- Usar a skill `impeccable` se disponível para preservar hierarquia, responsividade e acessibilidade da interface.
- Usar uma ferramenta de navegador/Playwright para testar desktop e celular após cada etapa visual ou de interação.
- Consultar apenas documentação oficial do Three.js e Cannon.js se uma API usada pela versão CDN atual for incerta.

## Escopo

**Arquivos que podem ser modificados:**

- `index.html`
- `DESIGN.md`
- `plans/README.md` — somente para atualizar o status ao final

**Fora do escopo:**

- `PRODUCT.md` — o propósito e a acessibilidade continuam válidos.
- Adicionar frameworks, bundlers, npm, arquivos JavaScript separados ou recursos obrigatórios externos.
- Alterar a duração de 120 segundos.
- Multiplayer real por rede; os outros cinco jogadores continuam sendo bots locais.
- Copiar modelos, ícones, sons, mapas, nomes ou layouts de produtos de terceiros.
- Persistência online, contas, anúncios, compras ou servidor.

## Fluxo de trabalho

O diretório não é um repositório Git. Não inicialize Git sem autorização. Antes de começar, faça cópias de segurança de `index.html` e `DESIGN.md` fora da pasta do projeto ou use a capacidade de desfazer do ambiente. Não crie cópias dentro do projeto final. Realize uma etapa por vez e mantenha o jogo executável entre etapas.

## Etapas

### Etapa 1: reorganizar as configurações e atualizar o sistema visual — CONCLUÍDA

Em `index.html`, agrupe constantes de configuração em objetos imutáveis próximos de `GAME_DURATION`, sem separar o arquivo:

- `WORLD_CONFIG`: dimensões, limites, célula espacial e contagens.
- `CAMERA_CONFIG`: FOV, altura base, distância base, fatores de crescimento e suavização.
- `PVP_CONFIG`: vantagem mínima de tamanho, bônus, atraso de renascimento e proteção.
- `QUALITY_CONFIG`: limites de partículas, pixel ratio e resolução de sombras por nível.
- `PALETTE`: cores semânticas do cenário.

Atualize `DESIGN.md` antes do código visual. Expanda a direção documentada para o cenário ensolarado e registre papéis de cor para céu, grama, asfalto, calçada, marcação viária, vegetação, água, prédios e estados de ameaça/alvo. Todos os valores documentados devem usar OKLCH e ter contraste distinguível.

No Three.js:

1. Troque a névoa atual por nenhuma névoa ou por névoa atmosférica começando somente além de 210 unidades e terminando depois de 340. Nunca reutilize `Fog(..., 62, 112)`.
2. Aumente o `far` da câmera para pelo menos 500.
3. Diminua a intensidade da `HemisphereLight` para a faixa `0.55–0.75` e aumente o sol para `1.45–1.80`.
4. Use materiais `MeshToonMaterial` ou uma combinação toon equivalente para objetos coloridos. Gere programaticamente um mapa tonal de três níveis; não adicione imagem externa.
5. Separe materiais foscos (rua/grama), brilhantes (carros/janelas) e emissivos (postes/borda do buraco).
6. Mantenha sombras, escolhendo mapa `2048` em qualidade alta e `1024` em móvel/qualidade média.
7. Não adicionar bloom global. A borda do buraco pode emitir luz visual por materiais locais.

**Verifique:** rode o validador JS e abra a tela inicial em 1280×800 e 390×844. Resultado esperado: cidade visível sem camada azul esbranquiçada, sombras claras, cores saturadas, HUD legível e nenhum erro no console.

### Etapa 2: adicionar índice espacial antes de aumentar o mapa — CONCLUÍDA

Crie uma classe ou objeto `SpatialGrid` dentro do script, com células quadradas de 12 unidades. Ele deve oferecer:

- `insert(entity)`
- `remove(entity)`
- `update(entity, oldX, oldZ)` para entidades móveis
- `queryCircle(x, z, radius)` retornando somente candidatos de células próximas
- `clear()` no reinício

Todo destrutível deve entrar no índice ao ser criado e sair ao ser engolido. Substitua o laço completo de `checkAbsorption()` por consulta de raio. Substitua o `filter().sort()` completo de cada bot por candidatos retornados pelo índice; escolha o melhor em um único laço, sem ordenar a coleção inteira.

Troque `CANNON.NaiveBroadphase` por `CANNON.SAPBroadphase(world)` e habilite sono nos corpos quando suportado pela versão usada. Continue removendo corpos engolidos do mundo físico. Reutilize instâncias de geometrias e materiais entre variações; não crie nova geometria idêntica para cada objeto.

Adicione um contador de desempenho interno que calcule FPS médio a cada 2 segundos, sem exibi-lo para jogadores fora de `?debug=1`.

**Verifique:** `rg -n "NaiveBroadphase|filter\(o => o.active" index.html` não deve encontrar o broadphase antigo nem o filtro global antigo dos bots. O validador JS imprime `JS_SYNTAX_OK`. Em `?debug=1`, o console ou painel de depuração mostra FPS médio e número de candidatos espaciais.

### Etapa 3: implementar câmera fixa no jogador e zoom proporcional — CONCLUÍDA

Crie `updateCamera(dt)` e invoque-a após `updatePlayer(dt)` e antes de renderizar. A função deve:

1. Calcular um ponto de observação a partir da posição atual do jogador.
2. Manter o jogador próximo ao centro visual, com leve deslocamento para a parte inferior para mostrar mais área à frente.
3. Aumentar altura e distância conforme `player.radius`, usando limites mínimos e máximos.
4. Interpolar posição e alvo com amortecimento independente de FPS (`1 - Math.exp(-speed * dt)`).
5. Atualizar `camera.lookAt()` com o alvo interpolado.
6. Manter o raycasting de mouse/toque correto no plano, porque a câmera agora se move.
7. Reposicionar a luz e a área de sombra junto da câmera ou do jogador para evitar que sombras desapareçam longe da origem.

Ponto inicial recomendado para ajuste, não valor obrigatório: altura `24 + radius × 6`, distância inclinada `20 + radius × 7`, limitadas para não atravessar o chão nem revelar todo o mapa. Ajuste visualmente em desktop e celular.

**Verifique:** mova o jogador até quatro extremos do mapa; ele permanece enquadrado. Force crescimento no modo de teste; a câmera afasta suavemente e volta a aproximar depois de um renascimento. Mouse e toque ainda levam o buraco ao ponto selecionado. Nenhum salto abrupto de câmera ao iniciar ou renascer.

### Etapa 4: ampliar a cidade e criar bairros variados — CONCLUÍDA

Depois do índice espacial estar funcionando, aumente o mundo para pelo menos `180 × 180`. Defina `DISTRICTS` com no mínimo cinco bairros:

- `downtown` — prédios, lojas, táxis, ônibus e placas.
- `residential` — casas, jardins, piscinas, cercas e carros.
- `park` — árvores, bancos, fonte, lago pequeno e brinquedos.
- `industrial` — galpões, caminhões, contêineres e guindaste.
- `marina` ou `beach` — areia, palmeiras, quiosques e barcos.

Crie um catálogo de objetos com, no mínimo: `type`, `value`, `radius`, `minimumHoleRadius`, `districts`, `weight` e função construtora. A progressão deve conter:

1. Pequenos: copos, cones, caixas, hidrantes, pedestres e placas.
2. Pequenos/médios: bancos, postes, árvores, barracas e motos.
3. Médios: carros, vans, quiosques e árvores grandes.
4. Médios/grandes: caminhões, ônibus, casas e piscinas.
5. Grandes: lojas, galpões e prédios pequenos.
6. Finais: prédios grandes, torre, guindaste e elementos especiais do bairro.

Entregar ao menos 25 tipos visuais e estas variações mínimas:

- 5 árvores/palmeiras
- 6 veículos
- 6 aparências de pedestres
- 8 construções
- 10 objetos urbanos menores compartilhados entre bairros

Use uma semente para que o mapa seja reproduzível, mas permita escolher nova semente ao reiniciar. Mantenha corredores livres, evite sobreposição de construções e distribua objetos pequenos suficientes em todas as áreas de nascimento.

Alvo de densidade: 350–550 objetos ativos, ajustado pelos testes de desempenho. Não ultrapasse 550 sem evidência de FPS estável em celular.

**Verifique:** no modo `?debug=1`, mostrar dimensões do mundo, semente, número total de objetos e contagem por bairro. Resultado esperado: cinco bairros identificáveis, pelo menos 25 tipos, nenhuma grande área vazia e FPS médio ≥30 em viewport móvel de referência.

### Etapa 5: implementar combate entre buracos e renascimento — CONCLUÍDA

Unifique operações comuns de jogador e bots em entidades de buraco com: `id`, `name`, `score`, `radius`, `targetRadius`, `active`, `invulnerableUntil`, `respawnAt`, `spawnPoint`, `mesh` e `isPlayer`.

Crie `checkHoleVsHole()` e execute-a uma vez por frame após movimentos e antes de absorção de objetos. Regras obrigatórias:

- O atacante precisa ter raio pelo menos 15% maior que a vítima.
- A vítima precisa estar suficientemente dentro da área do atacante; apenas encostar bordas não conta.
- Empates ou diferença abaixo de 15% não causam eliminação.
- Entidades inativas ou protegidas não podem atacar nem ser atacadas.
- Processar cada par uma vez por frame, evitando dupla eliminação.

Crie `onHoleEaten(eater, victim)`:

- Conceder bônus base de 20 pontos mais 25% da pontuação atual da vítima, arredondado.
- Transferir crescimento limitado para evitar saltos descontrolados.
- Exibir mensagem de eliminação e efeito de sucção.
- Tornar a vítima inativa por 3 segundos.
- Reduzir 35% do progresso de crescimento da vítima, nunca abaixo do raio inicial.
- Chamar `respawnHole(victim)` em um ponto seguro, distante de buracos maiores.
- Dar 2 segundos de proteção visual e lógica após renascer.
- Se a vítima for o jogador humano, manter o cronômetro correndo e mostrar uma contagem regressiva curta de renascimento, não a tela final.

Adicionar proteção contra efeito bola de neve: bônus transferido limitado e pontos de nascimento selecionados entre vários candidatos, escolhendo o mais distante de ameaças.

**Verifique:** no modo de teste, simule quatro casos: maior engole menor; menor não engole maior; diferença de 10% não elimina; protegido não é eliminado. Simule jogador sendo engolido: ele retorna após 3 segundos, menor e protegido. Ranking e pontuação refletem a eliminação.

### Etapa 6: substituir a IA simples por estados de decisão — CONCLUÍDA

Cada bot deve possuir estado `FORAGE`, `HUNT`, `FLEE` ou `WANDER`, personalidade e momento da próxima decisão. Decisões ocorrem em intervalos de `0.3–0.8` segundo, não a cada frame.

- `FORAGE`: buscar o melhor objeto comestível próximo considerando valor, distância e tamanho.
- `HUNT`: perseguir buraco pelo menos 15% menor dentro do raio de percepção.
- `FLEE`: afastar-se de buraco pelo menos 15% maior; este estado tem prioridade.
- `WANDER`: explorar outro bairro quando não há alvo útil.

Criar cinco personalidades usando pesos diferentes: agressivo, cauteloso, coletor, oportunista e equilibrado. Bots devem usar o mesmo índice espacial e as mesmas informações visíveis que o jogador poderia inferir; não teletransportar nem ignorar proteção.

Evitar agrupamento: aplicar pequena separação entre bots de tamanho semelhante e penalizar alvos já escolhidos por vários bots.

**Verifique:** observar uma partida completa acelerada no modo de teste. Cada estado deve ocorrer ao menos uma vez entre os cinco bots. Bots fogem de ameaças, caçam alvos válidos, coletam quando não há combate e não ficam presos continuamente nas bordas.

### Etapa 7: melhorar animações, feedback e interface para o mapa maior — CONCLUÍDA

Adicionar sem bibliotecas externas:

- Rodas girando e movimento simples de tráfego.
- Pedestres caminhando em trajetos curtos.
- Variação discreta de copa de árvore; desativar em movimento reduzido.
- Animação de sucção com inclinação, rotação, escala e partículas limitadas.
- Duas ou três camadas locais na borda do buraco para sensação de energia, sem pós-processamento global.
- Contorno/anel verde em adversário comestível próximo.
- Contorno/anel vermelho e seta de borda para ameaça próxima.
- Feed curto de eliminações.
- Minimapa compacto mostrando jogador, bots e limites/bairros, sem desenhar cada objeto.
- Indicador do próximo grupo de objetos que poderá ser engolido.

No celular, o ranking deve iniciar recolhido, o minimapa não deve cobrir tempo/pontos e o toque deve continuar disponível em toda a área livre. Respeitar áreas seguras do aparelho.

**Verifique:** desktop 1280×800 e móvel 390×844 sem rolagem horizontal. Com ranking aberto e fechado, HUD não bloqueia o jogador. Ameaças e alvos são distinguíveis sem depender somente de texto. Com `prefers-reduced-motion`, árvores e pulsos decorativos param e partículas são reduzidas.

### Etapa 8: adicionar qualidade adaptativa e limites de desempenho — CONCLUÍDA

Implemente níveis `HIGH`, `MEDIUM` e `LOW` escolhidos por capacidade inicial e FPS médio:

- `HIGH`: sombras 2048, pixel ratio até 1.75, partículas completas dentro do limite.
- `MEDIUM`: sombras 1024, pixel ratio até 1.4, metade das partículas.
- `LOW`: sombras reduzidas ou desativadas seletivamente, pixel ratio até 1.1, animações ambientais limitadas e poucas partículas.

Se FPS médio permanecer abaixo de 30 por 4 segundos, reduzir um nível. Não aumentar automaticamente durante a mesma partida para evitar oscilação. Limitar quantidade total de partículas e remover qualquer partícula expirada.

Atualizar somente entidades móveis e objetos em processo de absorção; não percorrer todos os modelos estáticos para animação. Frustum culling padrão do Three.js deve permanecer ativo.

**Verifique:** em modo debug, forçar cada nível e confirmar resolução de sombras, pixel ratio e limite de partículas. Simular queda de FPS e verificar uma única redução de nível. Nenhum vazamento crescente na contagem de partículas após múltiplas absorções.

### Etapa 9: criar ganchos de teste e realizar verificação completa

Somente quando a URL tiver `?test=1`, exponha `window.__CITY_VOID_TEST__` com funções seguras para:

- Ler tempo, score, raio, estado e posição das seis entidades.
- Adicionar crescimento ao jogador.
- Posicionar entidades para cenários de colisão.
- Avançar diretamente para o fim da partida.
- Ler FPS, nível de qualidade, contagem de objetos e candidatos espaciais.

Não exponha `eval`, escrita arbitrária ou funções de rede. Fora de `?test=1`, o objeto não deve existir.

Executar verificações no navegador:

1. Desktop 1280×800: iniciar, mover com mouse, engolir objetos, crescer, afastar câmera, engolir bot, ser engolido, renascer, abrir ranking e finalizar.
2. Móvel 390×844 com toque: iniciar por toque, mover, abrir/fechar ranking, verificar minimapa e ausência de overflow.
3. Teclado: WASD e setas movem corretamente com câmera em posições diferentes.
4. Acessibilidade: foco visível, som desligável e movimento reduzido.
5. Desempenho: uma partida com 350–550 objetos mantém FPS médio ≥30 na referência móvel do ambiente de teste.
6. Console: zero erros após início, absorção, PvP, renascimento, reinício e fim.
7. Cronômetro: começa em `02:00` e termina por tempo real em 120 segundos; o modo de teste pode acelerar apenas a automação.

**Verifique:** rode o validador JS; depois execute `rg -n "GAME_DURATION = 120|updateCamera|checkHoleVsHole|respawnHole|SpatialGrid|DISTRICTS|__CITY_VOID_TEST__" index.html`. Todos os sistemas devem aparecer e `GAME_DURATION = 120` deve permanecer inalterado.

## Plano de testes

Como o projeto não possui infraestrutura de testes e deve permanecer com um único arquivo executável, os testes são realizados pelo gancho `?test=1` e automação de navegador.

Casos obrigatórios:

- Cena carrega com seis buracos e pelo menos 350 objetos.
- Câmera segue o jogador nos quatro quadrantes.
- Crescimento aumenta distância da câmera de forma limitada e suave.
- Cada categoria só é engolida quando o raio permite.
- Índice espacial não retorna objetos removidos.
- Buraco 15% maior elimina; 10% maior não elimina.
- Proteção de renascimento impede eliminação.
- Jogador renasce após 3 segundos e a partida continua.
- Bot alterna entre fugir, caçar e coletar conforme vizinhança.
- Ranking ordena após pontuação de objeto e eliminação.
- Reinício recria mapa, índice, bots, partículas e temporizadores sem duplicações.
- Tela final aparece após 120 segundos.
- Layout móvel não produz rolagem ou controles inacessíveis.
- Movimento reduzido elimina animações ambientais não essenciais.
- Nenhum erro de console em um ciclo completo.

Não há teste existente para copiar. Mantenha os ganchos pequenos, documentados e totalmente condicionados a `?test=1`.

## Critérios de conclusão

Todos devem ser verdadeiros:

- [ ] Código executável continua inteiramente em `index.html`.
- [ ] Three.js e Cannon.js continuam carregados por CDN.
- [ ] `GAME_DURATION` continua exatamente `120`.
- [ ] Mapa tem pelo menos `180 × 180`, cinco bairros e 25 tipos visuais.
- [ ] Existem entre 350 e 550 objetos ativos no início, salvo redução documentada por desempenho.
- [ ] `SpatialGrid` é usado por absorção e busca de bots.
- [ ] `NaiveBroadphase` não é mais usado.
- [ ] Câmera segue o jogador e afasta proporcionalmente ao raio.
- [ ] Jogador e bots podem engolir buracos pelo menos 15% menores.
- [ ] Vítimas renascem após 3 segundos e recebem 2 segundos de proteção.
- [ ] Bots possuem os quatro estados e cinco personalidades.
- [ ] Névoa próxima foi removida e o cenário apresenta cores saturadas e sombras definidas.
- [ ] Minimapa, indicadores de ameaça/alvo e feed de eliminações funcionam.
- [ ] Mouse, toque, WASD e setas permanecem funcionais.
- [ ] `prefers-reduced-motion` e controle de som permanecem funcionais.
- [ ] Desktop e móvel não apresentam overflow nem erros de console.
- [ ] FPS médio de referência móvel é ≥30; caso contrário, a densidade foi reduzida e justificada.
- [ ] Validador de sintaxe imprime `JS_SYNTAX_OK`.
- [ ] `DESIGN.md` descreve fielmente a nova paleta e os gráficos.
- [ ] Apenas arquivos em escopo foram modificados.
- [ ] Status em `plans/README.md` foi atualizado para `DONE`.

## Condições para PARE

Interrompa e relate, sem improvisar, se:

- O código atual não corresponde aos trechos ou hashes deste plano antes das alterações.
- Uma API desejada não existe nas versões CDN atuais de Three.js ou Cannon.js.
- Manter um único `index.html` impedir uma etapa sem adicionar dependência obrigatória; peça decisão antes de dividir arquivos.
- O raycasting não puder ser mantido correto depois de duas tentativas razoáveis com câmera móvel.
- FPS móvel permanecer abaixo de 30 mesmo em qualidade `LOW` e com 350 objetos; apresente medições antes de reduzir mais.
- A colisão PvP permitir dupla eliminação ou eliminação por um buraco menor após duas tentativas de correção.
- Uma verificação falhar duas vezes após correção razoável.
- A implementação exigir modificar `PRODUCT.md` ou adicionar servidor/multiplayer real.

## Notas de manutenção

- Ao adicionar novos objetos, registre-os no catálogo e atribua bairros, tamanho mínimo, valor e peso. Não espalhe novos `if` por `createCity()`.
- Qualquer entidade móvel deve atualizar o índice espacial ao trocar de célula.
- Mudanças futuras na fórmula de crescimento precisam revalidar câmera, limite de PvP e categorias engolíveis.
- O revisor deve observar principalmente consumo de memória, duplicação de geometrias, seleção de spawn seguro e comportamento móvel.
- Multiplayer real, armazenamento de recordes, personalização e novos modos ficam explicitamente para planos futuros.
