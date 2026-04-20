# Deep Think Pipeline Research - April 21, 2026

## Gemini Deep Think Capabilities

**What It Is:** "System 2" reasoning model for complex problem-solving, PhD-level logic, scientific research, and advanced code generation.

**Key Features:**
- Uses "thinking tokens" to show internal reasoning steps
- Temperature should stay at 1.0 for reasoning tasks (lowering causes issues)
- 2M token context window
- Thinking level control parameter
- Thought signatures for chain-of-thought verification

## Access Methods

### 1. API Programmatic Access
- Early access program for researchers/enterprise developers
- Set `includeThoughts: true` in request config to get thought summaries
- Available through Vertex AI endpoints and Google AI Studio

### 2. Browser Workflow (What We'll Use)
**URL:** `gemini.google.com` → Tools menu → Deep Think

**Automation Options:**
- **Gemini Auto Browse:** Integrated into Chrome (Settings > AI Features > Chrome AI Auto Browse)
- **Demonstration Mode:** Click through workflow while Gemini generates code in background
- **Gems & AI mini-apps:** Describe goal at gemini.google.com, Gemini generates step-by-step workflow

**Code Extraction:** "Copy Code" button appears at top-right of code blocks or within Gemini Drops interface

## Optimal Prompt Structure for 3D Game Dev

```
Act as a Lead Game Engineer. Develop a polished, mobile-optimized 3D [GAME CONCEPT] 
using Three.js (r171+) in a single HTML file.

Core Technical Requirements:
- Renderer: Implement WebGPURenderer for 2026 performance, with automatic WebGL 2 fallback. Use renderer.init() for async setup.
- Shaders: Author custom visual effects using Three Shader Language (TSL) instead of raw GLSL for cross-backend compatibility.
- Performance: Optimize for mobile by maintaining under 100 draw calls via InstancedMesh and BatchedMesh. Use lowp or mediump precision for mobile shaders.
- Physics: Implement lightweight custom physics loop or GPGPU compute shader for high-fidelity collisions.
- Controls: Design responsive mobile touch controls (Virtual Joysticks/Gestures) with inertia and clamping.
- Architecture: Structure code using Entity Component System (ECS) pattern for modularity.

Provide complete, executable code including basic asset-loading strategy (placeholder geometries or embedded base64 assets).
```

## 2026 Mobile 3D Dev Standards

**WebGPU:** Supported on all major browsers including iOS Safari by late 2025. Up to 100x performance gains for compute-heavy tasks (particles, physics).

**TSL (Three Shader Language):** Node-based system replacing GLSL. Shaders run on both WebGL and WebGPU platforms.

**Vibe Coding:** AI-assisted workflow - describe complex game loops in natural language, Gemini translates to functional code.

**GPU-Driven Rendering:** Shift logic (frustum culling, physics) to GPU using compute shaders to bypass JavaScript single-thread limitations.

## Mobile Optimization Checklist

| Metric | Target | Method |
|--------|--------|--------|
| Draw Calls | < 100 per frame | InstancedMesh, BatchedMesh |
| Asset Size | ~10x reduction | Draco geometry compression, KTX2 textures |
| Memory | Prevent VRAM leaks | Call `.dispose()` on all geometries/materials/textures when removing |
| Shader Precision | Mobile-optimized | lowp or mediump precision |
| Distribution | Offline-capable | Package as PWA (Progressive Web App) for "Add to Home Screen" |

## Our Pipeline Workflow

```
1. I research via AI Mode (browser navigate + act evaluate) ✓ DONE
2. Spawn P3 (744B GLM-5.1) with optimized prompt
   - runtime: subagent
   - model: vllm-744b-p3/GLM-5.1-UD-Q2_K_XL-00001-of-00007.gguf
   - mode: run
   - task: [Deep Think prompt from above]
3. P3 generates code → announces result back
4. I QA the code:
   - Read full output
   - Check for bugs, missing requirements
   - Verify mobile optimization constraints met
5. Deploy via GitHub CLI:
   - gh command to push to eve-centaur-projects repo
   - GitHub Pages hosting
6. Test on mobile viewport simulator
```

## Key Learnings

1. **Deep Think = System 2 Reasoning:** Not for simple queries, reserved for complex multi-step engineering tasks
2. **Temperature Critical:** Must stay at 1.0 for reasoning - lowering breaks the thinking process
3. **Prompt Placement Matters:** Core instruction goes at END of prompt after context/examples
4. **Few-Shot Works Best:** Provide examples to guide reasoning depth
5. **Define Format Early:** Specify output format at top of prompt

## Next Steps

- Test pipeline with actual Deep Think spawn (744B P3)
- Validate code quality meets mobile constraints
- Automate browser workflow for Copy Code button extraction if needed
- Document scar tissue from first run (what worked, what didn't)
