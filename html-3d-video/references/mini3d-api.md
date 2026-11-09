# Three.js mini API notes

Use the current Three.js module API and check the version used by the project. These notes are intentionally concise; consult the official Three.js documentation for version-specific details.

## Basic setup

```js
import * as THREE from 'three';

const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 100);
camera.position.set(0, 1, 6);

const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: false });
renderer.setSize(width, height);
renderer.setPixelRatio(Math.min(window.devicePixelRatio || 1, 2));
document.body.appendChild(renderer.domElement);

scene.add(new THREE.HemisphereLight(0xffffff, 0x202030, 1.5));
const key = new THREE.DirectionalLight(0xffffff, 2);
key.position.set(3, 5, 4);
scene.add(key);

const mesh = new THREE.Mesh(
  new THREE.TorusKnotGeometry(0.8, 0.24, 160, 24),
  new THREE.MeshStandardMaterial({ color: 0x62d9ff, metalness: 0.45, roughness: 0.25 })
);
scene.add(mesh);
```

## Deterministic animation

Use elapsed seconds from a clock or an explicit timeline time. For reproducible capture, update the scene from a supplied time value rather than advancing state by a fixed amount per rendered frame:

```js
function renderAt(seconds) {
  mesh.rotation.y = seconds * 0.45;
  mesh.rotation.x = Math.sin(seconds * 0.7) * 0.12;
  renderer.render(scene, camera);
}
```

For a timeline of duration `D`, compute `t = clamp(elapsed, 0, D)` and pass `t` into each animation function. Do not base motion on assumptions such as “add 0.01 each frame.”

## Resize and export dimensions

For preview, update camera aspect and renderer size when the container changes. For capture, use an explicit render size and restore the preview size afterwards. Avoid changing the drawing buffer during an active recording. To set output dimensions:

```js
renderer.setPixelRatio(1);
renderer.setSize(outputWidth, outputHeight, false);
camera.aspect = outputWidth / outputHeight;
camera.updateProjectionMatrix();
```

`captureStream(fps)` captures the canvas at real-time frame cadence; it does not guarantee exact frame timing. Use feature detection and report unsupported browsers rather than assuming the APIs exist.

## Resource cleanup

When tearing down a scene, dispose of geometries, materials, and textures that are no longer used, then dispose the renderer if the page is done. Do not allocate meshes, materials, or arrays on every animation frame.

## CDN and local server

When using a CDN, pin a compatible Three.js version and use an import map so `three` and any addons resolve consistently. A local server (for example `python3 -m http.server`) avoids common ES-module restrictions associated with opening HTML through `file://`. Network access is required for CDN imports; explain this dependency and offer local dependency bundling when offline use is required.
