# StudioRender - AI Coding Guidelines

## Project Overview
StudioRender is a single-page web application for 3D model visualization using Three.js. It features real-time rendering with post-processing effects, HDRI environment lighting, and interactive controls for render settings.

## Architecture
- **Single-file design**: All HTML, CSS, and JavaScript contained in `index.html`
- **Modular imports**: Uses ES6 import maps for Three.js and addons from CDN
- **Post-processing pipeline**: EffectComposer with RenderPass, SSAOPass, and OutputPass
- **State management**: Simple object-based state for render parameters

## Key Technologies
- Three.js v0.169.0 (modular imports)
- Tailwind CSS (CDN)
- WebGL renderer with ACES tone mapping
- GLTF/GLB model loading with automatic scaling and centering

## Development Workflow
- **No build process**: Open `index.html` directly in a modern browser
- **Hot reload**: Refresh browser to see changes
- **Debugging**: Use browser dev tools; console logs for model loading errors

## Code Patterns

### Import Structure
```javascript
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';
// ... other addons
```

### Scene Setup
- Camera positioned at (5, 3, 6) with OrbitControls
- HDRI environment loaded from Poly Haven (studio_small_09_1k.hdr)
- Directional light for shadows, positioned relative to environment rotation
- Shadow-receiving floor plane at y=-0.01

### Model Loading
- Automatic scaling to fit 4x4x4 unit box
- Centering and lifting to place bottom at y=0
- Shadow casting/receiving enabled on all meshes
- Texture anisotropy set to 8 for quality

### UI Integration
- Glass-panel styled controls using Tailwind + custom CSS
- Real-time parameter updates via event listeners
- State object synchronized with UI values

### Render Loop
- Uses requestAnimationFrame with controls.update()
- Conditional rendering: composer.render() for SSAO, renderer.render() otherwise
- Screenshot capture via canvas.toDataURL()

## Conventions
- **Styling**: Tailwind classes with custom `.glass-panel` for UI overlays
- **State**: Centralized in `state` object, updated via UI events
- **Error handling**: Basic try/catch for model loading, alert on failure
- **Performance**: Pixel ratio capped at 2, antialiasing disabled for performance
- **Shadows**: PCFSoftShadowMap with bias -0.0001

## File References
- `index.html`: Complete application (HTML structure, styles, scripts)</content>
<parameter name="filePath">/home/jn2002dk/Documents/source/javascript/studiorender/.github/copilot-instructions.md