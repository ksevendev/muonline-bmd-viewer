# Implementation Plan - Mu Online Studio Web Enhancements

## User Requirements Addressed
1. Full character display option with base mesh and equipped items/wings.
2. Background environment preset selector (Lorencia, Dungeon, Arena, or transparent/solid color background).
3. Smooth asset import workflow (multi-part character selection and item/weapon/wing attachments).

## Proposed Changes
1. **Scene & Background Management (`src/character-test-scene.ts` / UI controls)**:
   - Enhance background environment toggle (Map background presets: Lorencia sky/grid, Dungeon dark/fog, Arena golden/combat, and Transparent/Solid color).
   - Ensure full character base mesh visibility toggle works seamlessly with equipped sets and wings.

2. **UI Controls & Dock Enhancements (`src/components/dock/BottomControlDock.tsx` or control panel)**:
   - Add intuitive toggles for "Exibir Corpo do Personagem" (Show Character Base Mesh) and "Ambiente de Fundo" (Background Environment / Map Preset).

3. **Verification**:
   - Compile and test scene loading, rendering, and media export (HD transparent PNG and video recording).

## Verification Plan
- Run `compile_applet` to verify TypeScript build success.
- Verify user interactions for toggling full character model and map background environments.
