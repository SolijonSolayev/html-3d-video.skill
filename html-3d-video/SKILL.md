---
name: html-3d-video
description: Create polished, self-contained 3D animated videos as browser-rendered HTML using Three.js, then preview and export them as video. Use when asked to create a 3D video, animated 3D scene, motion-design clip, or browser-based video deliverable.
---

# HTML 3D Video Creator

Create a complete HTML animation project that can be previewed in a browser and captured as a video. Prefer a small, readable implementation over unnecessary dependencies. Explain what files you created and how to preview/export them.

## Workflow

1. **Clarify the brief from context.** Identify subject, visual style, duration, aspect ratio, colors, text, and intended audience. Ask only for details that are necessary; otherwise choose sensible defaults and state them. Default to 1920×1080, 30 fps, 8–12 seconds, and a seamless or cleanly resolved ending.
2. **Plan the shot.** Describe the scene, camera movement, lighting, animation beats, and final frame before coding. Keep important objects and text within the safe area.
3. **Build the scene.** Use Three.js with an import map or a stable CDN import when no local project dependencies exist. Keep rendering, scene setup, animation, and capture controls clearly separated. Use deterministic time-based animation so the scene can be reproduced and recorded consistently.
4. **Make it usable.** Include a visible preview, play/pause or replay controls, and a clear export/record control when video export is requested. Show status and errors in the page; do not silently fail.
5. **Validate.** Check browser console errors, verify the scene renders at the requested aspect ratio, test the animation from start to finish, and confirm the export path works in a supported browser. Provide a fallback when a codec or capture API is unavailable.
6. **Deliver.** Summarize the result, list files, give exact local preview instructions, explain export format/browser limitations, and mention any external assets or network requirements.

## Implementation requirements

- Deliver a complete runnable HTML file or project, not pseudocode. Avoid omitted sections such as “add animation here.”
- Prefer procedural geometry, materials, lights, and generated text when that satisfies the brief. If external assets are used, use assets the user supplied or clearly identify the source and licensing considerations.
- Use `requestAnimationFrame` for preview. Keep animation based on elapsed time, not frame counts, so it remains smooth at different refresh rates.
- Handle resizing and device pixel ratio; avoid excessive pixel ratios that cause slow rendering.
- Set the renderer's drawing buffer to the intended export dimensions when recording. Capture from the canvas with `canvas.captureStream(fps)` and `MediaRecorder` where supported. Select a supported MIME type with `MediaRecorder.isTypeSupported()` rather than assuming a codec. Stop all tracks and release resources when finished.
- Explain that browser video recording is real-time and can vary by machine/browser. For frame-accurate or production encoding, provide an optional FFmpeg workflow using a numbered image sequence or another explicitly generated input; never imply that the browser guarantees a particular codec.
- Treat imported files and assets as untrusted. Do not execute user-provided scripts or download arbitrary assets without explaining what they do.
- Keep controls accessible: labels, keyboard-operable buttons, visible focus, and status text. Respect reduced-motion preferences when appropriate.

## Suggested project structure

For a single-scene request, a self-contained `index.html` is usually enough. For a larger deliverable, use:

```text
project/
├── index.html
├── src/
│   ├── main.js
│   └── scene.js
├── assets/
└── README.md
```

## References

- Read [animation craft guidance](references/animation-craft.md) for composition, timing, and motion polish.
- Read [Three.js mini API notes](references/mini3d-api.md) for common scene and renderer patterns.
- Read [FFmpeg recipes](references/ffmpeg-recipes.md) when the user needs a post-processing or image-sequence workflow.
- Use `assets/template.html` as a starting point for a browser preview and recording UI; adapt it to the brief rather than returning it unchanged.
