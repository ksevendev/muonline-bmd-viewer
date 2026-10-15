# MU Online Studio Web & BMD Viewer - Visão Geral do Projeto e Plano de Evolução

Este documento apresenta a análise completa da arquitetura, módulos, funcionalidades e o **Plano de Ação Prático** para transformar o visualizador em um estúdio profissional de criação de banners e mídias do **MU Online**.

---

## 🛠️ Arquitetura e Tecnologias

- **Core 3D Engine**: Three.js (com suporte a WebGL e WebGPU via `RendererBackend`).
- **Linguagem**: TypeScript estrito (`strict: true`).
- **Empacotador e Servidor de Desenvolvimento**: Vite (servido na porta `3000`).
- **Suporte Desktop**: Electron (`electron/` e `package.json` configurados para empacotamento com `electron-builder`).
- **Testes**: Jest (`jest.config.js` com `ts-jest`).

---

## 📦 Módulos Principais e Funcionalidades

### 1. Visualizador de Modelos 3D (`src/main.ts` & `src/bmd-loader.ts`)
- **Carregamento de BMD**: Parser binário completo para arquivos de modelo 3D `.bmd` do MU Online (vértices, triângulos, normais, ossos e animações).
- **Decodificação de Texturas**: Suporte a texturas nos formatos `.jpg`, `.png`, `.tga`, `.ozj` e `.ozt` (com decodificador XOR para `.ozj`/`.ozt`).
- **Exportação**: Capacidade de exportar modelos para `.glb`/`.gltf` e gravação de animações em formato GIF animado (`gif.js`).

### 2. Estúdio de Personagens & Sets (`src/character-test-scene.ts`)
- **Seleção de Classes**: Suporte a todas as classes clássicas e evoluções do MU Online (Dark Wizard, Dark Knight, Fairy Elf, Magic Gladiator, Dark Lord, Summoner, etc.).
- **Partes Base do Personagem**: Carregamento modular das partes corporais base (`HelmClass`, `PantClass`, `GloveClass`, `BootClass`) por ID de classe.
- **Sistema de Encaixe em Ossos (Bone Sockets)**: Fixação precisa de itens, armas (mão esquerda e direita) e asas nas costas utilizando os índices de ossos do esqueleto do personagem.
- **Efeitos de Itens**: Sistema de brilho avançado para itens com nível (`+0` a `+15`), itens *Excellent* e *Ancient*, com shaders personalizados e ajuste de intensidade.
- **Animações**: Seletor de animações em tempo real com controle deslizante de velocidade de reprodução.

### 3. Visualizador de Terrenos e Mundos (`src/terrain-scene.ts`)
- **Exploração de Mapas**: Carregamento de mundos do MU Online a partir da pasta `Data`.
- **Atributos de Terreno (ATT)**: Leitura de parâmetros ATT, bandeiras de colisão (`TWFlags`) e sobreposição de malhas de navegação (*ATT Overlay*).
- **Minimapa e Navegação**: Minimapa interativo, saltos de coordenadas (X, Z) e salvamento de favoritos/bookmarks de câmera.

### 4. Biblioteca de Itens, Habilidades e Efeitos (`src/item-bmd.ts`, `src/skill-bmd.ts`)
- **Item Browser**: Inspeção de definições de itens do arquivo item.bmd.
- **Skill Browser**: Visualização de magias e efeitos visuais.
- **GFx e Sound Browsers**: Inspeção de interfaces e sons do cliente original.

---

## 🚀 Plano de Ação Prático para Evolução Avançada

1. **Isolamento do Renderizador para Exportação HD**:
   - Implementação de redimensionamento temporário (Offscreen / High-Res Resolution Scaling em 1080p ou 4K) com `{ alpha: true, preserveDrawingBuffer: true }` para captura de imagens PNG em alta resolução com fundo transparente.
2. **Integração da API MediaRecorder**:
   - Conexão do stream do canvas via `canvas.captureStream(60)` para gravação fluida de animações, skills e ciclos de caminhada em formato `.webm`.
3. **Módulo de Map Builder e Composição de Cenários (React + Zustand)**:
   - Gerenciamento de estado global para posicionamento de objetos em mapas (coordenadas X, Y, Z, rotação e escala) combinando personagens e cenários.
4. **Painel de Cadastro e Ajuste Fino de Assets (CRUD & Offsets)**:
   - Interface lateral estilo Cyberpunk/Dark Mode para upload de arquivos `.bmd`/`.ozj` com sliders em tempo real para ajuste de offsets de posicionamento de asas, armas e sets.

---

## 🛠️ Como Executar

1. **Desenvolvimento Web**:
   ```bash
   npm run dev
   ```
   Acesse a aplicação em `http://localhost:3000`.

2. **Modo Desktop (Electron)**:
   ```bash
   npm run electron
   ```

3. **Testes Unitários**:
   ```bash
   npm test
   ```
