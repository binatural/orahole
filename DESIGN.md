# Design System

## Direction

Cidade grande estilizada com materiais urbanos reconhecíveis e proporções legíveis para gameplay. A imagem deve lembrar uma maquete arquitetônica contemporânea: concreto, tijolo, pedra, aço, vidro escuro, asfalto e vegetação natural sob luz solar definida. Evitar fachadas em cores fantasia, aparência de brinquedo plástico, névoa próxima, bloom global e filtros que escondam silhuetas.

Estratégia de cor `restrained`: neutros minerais dominam o cenário. Vinho, azul-marinho, verde escuro e ocre aparecem em veículos, roupas e pequenos objetos plausíveis. Teal permanece reservado ao jogador e amarelo ao progresso/interface; as cores de gameplay não contaminam fachadas ou grandes superfícies.

## Color

- Primary/player: `#20b8ad`
- Sky: `#7fb7d1`
- Grass: `#547b4f`
- Asphalt: `#30363a`
- Sidewalk: `#aeb3b5`
- Road marking/reward: `#d7b94a`
- Concrete light/mid/dark: `#b7b8b5`, `#858b8e`, `#545d63`
- Brick: `#7b4b3c`
- Stone: `#747878`
- Glass: `#173541`
- Vegetation dark/light: `#2f633d`, `#4f7d4b`
- Vehicle accents: burgundy `#8c3e36`, navy `#334f67`, graphite `#55515f`
- HUD surface: `oklch(0.20 0.04 255 / 0.93)`
- HUD ink: `oklch(0.98 0.01 200)`
- HUD muted: `oklch(0.79 0.04 235)`
- Threat: `oklch(0.63 0.25 25)`
- Edible target: `oklch(0.74 0.21 145)`

## World Composition

- Mundo jogável de `180 × 180`, cercado por água azul para que os limites não revelem um vazio visual.
- A cidade começa com 520 objetos distribuídos em metas fixas por bairro: residencial 105, centro 130, parque 100, industrial 110 e marina 75.
- **Residencial:** gramado natural, casas de concreto/tijolo, piscinas, jardins e veículos particulares.
- **Centro:** calçadas em placas de concreto, fachadas minerais, vidro escuro, táxis, ônibus e mobiliário urbano.
- **Parque:** vegetação em verdes naturais, árvores, arbustos, bancos e fontes.
- **Industrial:** concreto escuro, aço, galpões, contêineres, caminhões e guindastes.
- **Marina:** areia dessaturada, água azul-acinzentada, palmeiras, quiosques e barcos.
- Estradas escuras e faixas amarelas atravessam os bairros e criam contraste com os terrenos.
- A geração usa semente reproduzível, mas escolhe uma nova semente a cada reinício.
- Objetos de maior raio são posicionados primeiro para reservar lotes ao skyline; pessoas, bicicletas, veículos e mobiliário preenchem os espaços restantes.

## Visual Density and Models

- O catálogo possui 36 tipos, incluindo grupos de pessoas, bicicletas, carrinhos de comida, edifícios residenciais, hotéis e torres comerciais.
- O centro usa pelo menos cinco famílias de edifícios altos com alturas, recuos e volumes diferentes; a torre final alcança aproximadamente 22 metros.
- Fachadas usam faixas de janelas nas quatro orientações, entradas, marquises, varandas, coroamentos e equipamentos de cobertura.
- Pessoas possuem cabeça suavizada, cabelo, braços e pernas animadas; grupos reúnem três variações sem criar uma nova regra de gameplay.
- Árvores, postes, rodas e formas redondas usam mais segmentos, preservando o estilo arcade sem a aparência excessivamente facetada.
- Faixas de janela não projetam sombras próprias, reduzindo o custo do shadow pass sem remover sua profundidade visual.

## Lighting and Materials

- Todos os objetos urbanos usam `MeshStandardMaterial`; toon/cel shading não faz parte da direção atual.
- Texturas procedurais determinísticas adicionam granulação ao concreto, asfalto, grama e areia, além de juntas de calçada e paginação de tijolos, sem arquivos externos.
- Ruas, gramado, concreto e calçadas têm alta rugosidade; aço, carros e vidro usam metalness/roughness controlados.
- `ACESFilmicToneMapping` e exposição neutra preservam contraste sem transformar cores em pastéis.
- Luz ambiente é contida; uma luz solar quente e mais intensa define os volumes e sombras.
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
- O enquadramento inicial é mais próximo para valorizar pessoas, veículos e fachadas; o afastamento proporcional continua conforme o crescimento.
- Altura e distância aumentam proporcionalmente ao raio do buraco, com limites mínimos e máximos.
- Posição, alvo e zoom usam amortecimento exponencial independente da taxa de quadros.
- O perfil móvel recebe altura e distância adicionais para compensar a tela estreita.
- Raycasting de mouse e toque é recalculado enquanto a câmera se move.
- A luz solar e o volume de sombras acompanham o jogador para manter iluminação consistente nos limites do mapa.

## Responsive Layout

No desktop, placar à esquerda e ranking à direita. No celular, placar compacto no topo, ranking recolhido e instruções próximas à base sem bloquear o controle por toque. O renderer limita pixel ratio e resolução de sombras por perfil para manter desempenho.

## Mobile Controls

- Em dispositivos com ponteiro grosso, tocar na área livre cria um joystick flutuante translúcido no ponto do toque.
- O deslocamento do botão interno controla direção e intensidade; uma zona morta central evita movimento acidental.
- Soltar o dedo, perder foco, trocar de aba ou ser engolido cancela o joystick imediatamente.
- Mouse continua usando destino no plano 3D e teclado mantém WASD/setas; os três métodos são independentes.
- O joystick possui área visual de 112 px, não recebe eventos próprios e respeita o HUD e as áreas seguras do aparelho.

## Render Stability

- O foco da luz direcional é alinhado à grade de texels do mapa de sombras para reduzir cintilação durante o acompanhamento da câmera.
- `normalBias`, `bias`, distância da câmera de sombra e raio de filtragem são limitados para evitar acne e instabilidade.
- Terrenos de bairro, ruas e faixas usam `polygonOffset` em camadas distintas para evitar z-fighting em ângulos inclinados.

## Adaptive Quality

- O perfil inicial considera formato móvel, memória informada pelo navegador e quantidade de núcleos disponíveis.
- `HIGH` limita pixel ratio a `1.75`, usa sombras `2048` e até 150 partículas.
- `MEDIUM` limita pixel ratio a `1.4`, usa sombras `1024`, reduz pela metade a emissão de partículas e atualiza a vegetação em quadros alternados.
- `LOW` limita pixel ratio a `1.1`, desativa sombras, limita o total a 32 partículas e mantém apenas movimentos essenciais de gameplay.
- FPS é medido em janelas de 2 segundos. Quatro segundos consecutivos abaixo de 30 FPS reduzem um nível; a qualidade não aumenta automaticamente durante a mesma partida.
- Uma nova partida pode restaurar o perfil inicial do dispositivo. O modo `?debug=1` permite forçar os três níveis para diagnóstico.
- Entidades móveis, vegetação animada e objetos em absorção usam listas dedicadas; modelos estáticos não são percorridos a cada quadro.
- O frustum culling padrão do Three.js permanece ativo.
