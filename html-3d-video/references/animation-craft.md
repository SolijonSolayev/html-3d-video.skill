# Animation craft: timing, composition, and polish

Use these principles when composing a short 3D video. They are practical defaults, not rigid rules.

## Composition

- Establish a clear focal subject and a simple hierarchy: subject first, supporting detail second, background last.
- Use depth deliberately: foreground accents, subject plane, and a restrained background. Avoid clutter that competes with the subject.
- Frame for the requested aspect ratio and keep titles, logos, and essential details away from the edges. Check the composition at the final render dimensions.
- Use contrast, silhouette, and controlled highlights to keep the subject readable. Avoid clipping bright materials to pure white or crushing all shadow detail.

## Timing and motion

- Give the viewer time to understand the opening image. A useful short-clip structure is: establish, reveal/action, hero hold, resolve.
- Prefer smooth, intentional easing over constant-speed movement for camera and object transitions. Use a gentle ease-in/out, and avoid abrupt changes unless the style calls for them.
- Keep one primary movement at a time. Secondary motion (particles, orbiting details, light sweeps) should support the focal action.
- Build animation from normalized time `u = clamp((t - start) / duration, 0, 1)` and an easing function. This makes it deterministic and easy to adjust.
- Give transitions enough time to read. A brief final hold creates a clean ending and improves thumbnail selection.
- For a loop, ensure both pose and velocity at the end match the beginning; matching only the positions can still produce a visible jerk.

## Camera and lighting

- Move the camera only when movement adds information or energy. A small orbit, dolly, or push-in is usually more effective than combining several moves.
- Avoid moving the camera through geometry or changing focal length abruptly. Use a stable target and keep the subject in frame.
- Start with a key light, a softer fill, and a rim/accent light. Add fog, bloom, or particles only when they improve the story and performance allows.
- Test the scene with tone mapping and color space configured intentionally; ensure the result is consistent between preview and capture.

## Performance and review

- Reuse geometry and materials for repeated objects; avoid creating new GPU resources inside the animation loop.
- Limit particle count, shadow-map size, and device pixel ratio for real-time playback. Provide a quality setting if the scene is expensive.
- Review the first frame, key transitions, and final frame at full size. Also review a reduced-size view to catch weak silhouettes and unreadable text.
- Ask whether each effect helps the brief. Remove effects that do not.
