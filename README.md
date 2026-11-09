# HTML 3D Video Skill

A Claude skill for designing, implementing, previewing, and exporting polished 3D animations as browser-rendered HTML.

## Install

Copy the `html-3d-video` directory into Claude's skills directory so the final path is:

```text
.claude/skills/html-3d-video/SKILL.md
```

For a user-level installation, use the equivalent `~/.claude/skills/html-3d-video/` path. Restart or reopen Claude Code if the skill is not picked up immediately.

The repository also contains `html-3d-video.skill`, the original packaged skill archive. Use the directory version for reviewing or editing its source; package it with your preferred skill-packaging tool when you need an archive.

## Use

Ask Claude for a concrete deliverable, for example:

> Create a 10-second 16:9 3D product reveal in a dark studio. Use procedural geometry, gold lighting, a slow camera orbit, and provide a browser preview plus a video export button.

The skill guides Claude to clarify only essential requirements, create a runnable HTML scene, validate playback/export, and explain browser limitations.

## Previewing generated projects

Three.js ES modules and some browser APIs require a local web server. From the project directory, run:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000` in a modern browser. Do not rely on opening the file directly with `file://` if module loading or recording APIs fail.

## Export notes

A page can record its WebGL canvas using `captureStream()` and `MediaRecorder` in supported browsers. Codec support differs across browsers and operating systems; a generated project should detect supported MIME types and report a useful error if recording is unavailable. Real-time browser recording is not frame-accurate. For final delivery, an image sequence encoded with FFmpeg can offer more control.

## Repository contents

- `html-3d-video/SKILL.md` — skill metadata and creation workflow.
- `html-3d-video/references/` — focused guidance on motion, Three.js, and FFmpeg.
- `html-3d-video/assets/template.html` — starter preview/recording page.
- `html-3d-video.skill` — original archive, preserved as supplied.
