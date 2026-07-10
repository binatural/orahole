# Design System

## Direction

Cidade arcade em um dia ensolarado, vista como um brinquedo urbano colorido. A imagem deve ser nítida, energética e imediatamente legível: céu limpo, cores saturadas, sombras definidas e materiais em estilo toon/cel shading. Evitar névoa próxima, tons lavados, bloom global e filtros que escondam a silhueta dos objetos.

Estratégia de cor `full palette`: teal identifica o jogador, amarelo comunica recompensa, coral sinaliza ação, cobalto e violeta diferenciam objetos e competidores. As áreas grandes do cenário usam cores decididas, mas com luminâncias diferentes para preservar separação visual.

## Color

- Primary/player: `oklch(0.74 0.18 188)`
- Sky: `oklch(0.79 0.14 220)`
- Grass: `oklch(0.72 0.20 148)`
- Asphalt: `oklch(0.29 0.06 255)`
- Sidewalk: `oklch(0.94 0.01 250)`
- Road marking/reward: `oklch(0.84 0.18 88)`
- Coral/action: `oklch(0.65 0.24 28)`
- Cobalt/building: `oklch(0.58 0.23 264)`
- Violet/competitor: `oklch(0.62 0.23 300)`
- Vegetation dark: `oklch(0.61 0.20 148)`
- Water/window: `oklch(0.72 0.16 220)`
- HUD surface: `oklch(0.20 0.04 255 / 0.93)`
- HUD ink: `oklch(0.98 0.01 200)`
- HUD muted: `oklch(0.79 0.04 235)`
- Threat: `oklch(0.63 0.25 25)`
- Edible target: `oklch(0.74 0.21 145)`

## World Composition

- Mundo jogável de `180 × 180`, cercado por água azul para que os limites não revelem um vazio visual.
- **Residencial:** gramado vivo, casas, piscinas, jardins e veículos particulares.
- **Centro:** superfícies azul-ardósia, comércio, prédios, táxis, ônibus e mobiliário urbano.
- **Parque:** verde profundo, árvores, arbustos, bancos e fontes.
- **Industrial:** cinza-azulado escuro, galpões, contêineres, caminhões e guindastes.
- **Marina:** areia amarela, água, palmeiras, quiosques e barcos.
- Estradas escuras e faixas amarelas atravessam os bairros e criam contraste com os terrenos.
- A geração usa semente reproduzível, mas escolhe uma nova semente a cada reinício.

## Lighting and Materials

- Objetos coloridos usam materiais toon com três níveis de iluminação.
- Ruas, gramado e calçadas são foscos.
- Carros, janelas e lâmpadas podem ter reflexo local controlado.
- Luz ambiente é moderada; uma luz solar quente cria a hierarquia principal.
- Sombras usam 2048 px em perfil alto e 1024 px em perfil móvel/médio.
- Névoa atmosférica, quando presente, começa além da área jogável próxima e nunca deve criar uma camada azul sobre a ação.
- A borda do buraco pode emitir cor local; não usar bloom em toda a imagem.

## Typography

Uma única família sans-serif de sistema, com números tabulares e pesos fortes no HUD. Escala compacta e fixa para preservar espaço de jogo.

## Components

HUD com superfícies escuras opacas, contornos discretos e cantos de até 14 px. Botões em formato de pílula apenas quando são ações compactas. Ranking como lista densa, com jogador destacado em teal. O painel de diagnóstico só aparece com `?debug=1` e usa tipografia monoespaçada.

## Motion

Transições de 150–250 ms para estados da interface. Partículas e pulsos respondem apenas a ações do jogador. Em `prefers-reduced-motion`, eliminar pulsos ambientais e reduzir partículas. Não usar movimento ou brilho apenas para decorar.

## PvP States

- Um buraco só absorve outro quando possui pelo menos 15% de vantagem e envolve suficientemente o centro da vítima.
- Eliminação reduz o buraco até desaparecer e usa partículas na cor do vencedor.
- Quando o jogador é engolido, uma contagem central de 3 segundos substitui temporariamente a ação sem interromper a partida.
- O renascimento usa um ponto distante de ameaças e concede 2 segundos de proteção.
- Proteção é comunicada por anel branco pulsante; em movimento reduzido, permanece branco sem pulsação adicional.
- Mensagens de eliminação usam o toast existente e mantêm pontuação/ranking visíveis.

## Gameplay Feedback

- Minimapa mostra bairros, vias, jogador e cinco bots; objetos individuais não são desenhados para preservar clareza e desempenho.
- Adversários comestíveis recebem anel verde; ameaças recebem anel vermelho e uma seta de borda apontando sua direção.
- Feed compacto mantém até quatro eliminações recentes sem competir com o ranking.
- A barra inferior informa o próximo tipo de objeto liberado e o raio necessário.
- Veículos circulam pelas vias, pedestres percorrem trajetos curtos e barcos navegam lentamente; todos atualizam índice espacial e física.
- Árvores e palmeiras têm balanço sutil, rodas giram e a sucção inclina/rotaciona objetos durante a queda.
- Em movimento reduzido, balanço de vegetação, passos, rotação da aura e pulsos decorativos ficam desativados; movimento essencial de gameplay permanece.

## Camera

- A câmera permanece ancorada ao jogador, com o buraco ligeiramente abaixo do centro para revelar mais área à frente.
- Altura e distância aumentam proporcionalmente ao raio do buraco, com limites mínimos e máximos.
- Posição, alvo e zoom usam amortecimento exponencial independente da taxa de quadros.
- O perfil móvel recebe altura e distância adicionais para compensar a tela estreita.
- Raycasting de mouse e toque é recalculado enquanto a câmera se move.
- A luz solar e o volume de sombras acompanham o jogador para manter iluminação consistente nos limites do mapa.

## Responsive Layout

No desktop, placar à esquerda e ranking à direita. No celular, placar compacto no topo, ranking recolhido e instruções próximas à base sem bloquear o controle por toque. O renderer limita pixel ratio e resolução de sombras por perfil para manter desempenho.

## Adaptive Quality

- O perfil inicial considera formato móvel, memória informada pelo navegador e quantidade de núcleos disponíveis.
- `HIGH` limita pixel ratio a `1.75`, usa sombras `2048` e até 150 partículas.
- `MEDIUM` limita pixel ratio a `1.4`, usa sombras `1024`, reduz pela metade a emissão de partículas e atualiza a vegetação em quadros alternados.
- `LOW` limita pixel ratio a `1.1`, desativa sombras, limita o total a 32 partículas e mantém apenas movimentos essenciais de gameplay.
- FPS é medido em janelas de 2 segundos. Quatro segundos consecutivos abaixo de 30 FPS reduzem um nível; a qualidade não aumenta automaticamente durante a mesma partida.
- Uma nova partida pode restaurar o perfil inicial do dispositivo. O modo `?debug=1` permite forçar os três níveis para diagnóstico.
- Entidades móveis, vegetação animada e objetos em absorção usam listas dedicadas; modelos estáticos não são percorridos a cada quadro.
- O frustum culling padrão do Three.js permanece ativo.
