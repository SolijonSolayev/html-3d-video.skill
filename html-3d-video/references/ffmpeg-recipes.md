# FFmpeg recipes for generated 3D video

These recipes assume FFmpeg is installed and that you have permission to use all input assets. Verify output dimensions, frame rate, duration, and audio before delivery.

## Encode a numbered PNG sequence

If frames are named `frame_000001.png`, `frame_000002.png`, and so on:

```bash
ffmpeg -framerate 30 -i frame_%06d.png \
  -c:v libx264 -pix_fmt yuv420p -crf 18 -movflags +faststart \
  output.mp4
```

For a transparent sequence, use a codec/container that supports alpha (for example ProRes 4444 in MOV); H.264 in MP4 does not preserve alpha.

## Convert an existing browser recording

Inspect the input first, because browser recordings may use WebM or a codec that differs by platform:

```bash
ffprobe -hide_banner input.webm
ffmpeg -i input.webm -c:v libx264 -pix_fmt yuv420p -crf 18 \
  -movflags +faststart output.mp4
```

If audio is present and should be retained, explicitly map the desired streams and verify audio/video duration alignment. Do not overwrite the source recording.

## Quality checks

- Confirm the encoded file opens and plays from beginning to end.
- Check the first and final frames, frame rate, dimensions, and audio if any.
- Mention that encoding quality, file size, and supported codecs depend on the selected settings and local FFmpeg build.
