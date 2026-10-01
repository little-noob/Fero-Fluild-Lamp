# Virtual Ferrofluid Lamp Pro

A browser-based, sound-reactive ferrofluid simulation built with **WebGL + Web Audio API**.

This project recreates the visual behavior of a ferrofluid lamp virtually, including:

- fluid-like blob merging
- droplet splitting
- smooth magnetic attraction
- strong music response
- bass / mids / highs reactivity
- mouse / pointer attraction
- extreme-hover burst behavior
- calm regrouping after interaction
- uploaded audio playback
- live microphone input
- mobile-friendly controls
- no framework dependency

---

## Demo concept

The simulation is inspired by physical ferrofluid lamps where magnetic liquid forms organic black shapes, droplets, spikes, and clusters inside a transparent circular chamber.

The current implementation uses a **WebGL metaball field** for rendering and a lightweight custom particle system for movement.

Audio is analyzed using the **Web Audio API**.

---

## Main Features

### Sound Reactive

The visual simulation reacts to different parts of the audio spectrum.

- **Bass**
  - large magnetic movement
  - stronger blob attraction
  - larger fluid deformation
  - stronger central motion

- **Mids**
  - turbulence
  - stretching
  - wobble
  - organic movement

- **Highs**
  - smaller droplet vibration
  - edge movement
  - sharper surface activity

---

## Audio Sources

The project supports:

### Uploaded music

Users can upload an audio file directly in the browser.

Supported formats depend on the browser but normally include:

- MP3
- WAV
- OGG
- M4A
- AAC

### Microphone input

The simulation can react to live microphone input.

Microphone access requires:

- HTTPS

or

- localhost

Most modern browsers will block microphone permissions on a normal HTTP page.

---

## Pointer Interaction

The lamp is interactive.

Move the mouse or pointer around the glass chamber and the ferrofluid will react.

### Pointer attraction

When the pointer moves close to the fluid, the mass is pulled toward it.

### Fast pointer movement

Moving the pointer quickly creates turbulence and throws droplets outward.

### Extreme hover interaction

If the pointer remains very close to the fluid for a short period:

1. the ferrofluid becomes unstable
2. droplets split apart
3. smaller droplets move outward
4. when the pointer moves away, they slowly regroup

Clicking or holding the pointer creates an even stronger burst.

---

## Recovery / Re-Coalescence

After splitting, the fluid does not remain scattered permanently.

A recovery system gradually pulls droplets back toward the magnetic center.

The result is:

```text
Large blob
    ↓
Pointer interaction
    ↓
Instability
    ↓
Droplet split
    ↓
Scattered ferrofluid
    ↓
Pointer leaves
    ↓
Magnetic attraction
    ↓
Droplets merge
    ↓
Large blob again
```

The recovery speed can be adjusted from the controls.

---

## Controls

The UI includes several simulation controls.

### Audio Sensitivity

Controls how strongly the ferrofluid reacts to music.

Higher values create:

- stronger bass movement
- larger displacement
- more active turbulence
- greater high-frequency vibration

---

### Magnet Strength

Controls the attraction force toward the active magnetic point.

Higher values create:

- faster blob movement
- stronger regrouping
- more aggressive pulling
- larger directional changes

---

### Base Movement

Controls the natural movement of the ferrofluid even without strong audio.

This prevents the simulation from appearing static.

---

### Pointer Force

Controls how strongly the mouse or touch pointer influences the fluid.

Higher values make the ferrofluid follow the pointer more aggressively.

---

### Split Strength

Controls how violently droplets separate when the split interaction is triggered.

---

### Recovery Speed

Controls how quickly scattered droplets regroup into a single mass.

---

### Viscosity

Controls how much momentum the ferrofluid retains.

Lower viscosity:

- more energetic movement
- longer momentum
- more chaotic droplets

Higher viscosity:

- slower movement
- smoother transitions
- calmer fluid behavior

---

### Droplet Count

Controls the number of metaball particles used in the simulation.

Higher values can create:

- more detailed fluid shapes
- more small droplets
- more complex merging behavior

Current maximum:

```text
30 droplets
```

This limit is intentional to keep the WebGL shader lightweight.

---

## Simulation Modes

### Demo Mode

Demo mode generates artificial bass, mids, and highs.

This allows the simulation to move without uploading music.

Useful for:

- testing
- previews
- development
- screenshots
- demos

---

### Uploaded Audio Mode

When an audio file is playing, the analyzer reads the live frequency spectrum.

The simulation automatically switches away from demo mode.

---

### Microphone Mode

When microphone input is enabled:

- demo mode is disabled
- uploaded audio is paused
- live sound frequencies control the simulation

---

## Technology Stack

The project is intentionally lightweight.

### HTML

Used for:

- layout
- controls
- audio player
- canvas container

### CSS

Used for:

- responsive layout
- UI styling
- dark control panel
- mobile adaptation

### JavaScript

Used for:

- simulation physics
- pointer tracking
- audio analysis
- microphone input
- particle movement
- droplet splitting
- recovery behavior

### WebGL

Used for rendering the ferrofluid.

The shader creates:

- metaball merging
- smooth black liquid surfaces
- glass shading
- light reflection
- edge deformation
- high-frequency surface noise
- ferrofluid-style spikes

### Web Audio API

Used for:

- FFT frequency analysis
- bass detection
- mids detection
- highs detection
- microphone analysis
- uploaded audio analysis

---

## Project Structure

The project currently requires only one file.

```text
ferrofluid-lamp-pro/
│
└── index.html
```

No build process is required.

No npm installation is required.

No JavaScript framework is required.

---

## Running Locally

You can open `index.html` directly in a browser for most functionality.

However, microphone access may not work when opening the file through:

```text
file://
```

For full functionality, use a local web server.

### Python

```bash
python3 -m http.server 8080
```

Then open:

```text
http://localhost:8080
```

### VS Code

You can also use the **Live Server** extension.

---

## Deploying to a Server

Upload the file to a web-accessible folder.

Example:

```text
public_html/
└── ferrofluid/
    └── index.html
```

Then visit:

```text
https://yourdomain.com/ferrofluid/
```

HTTPS is strongly recommended and is required for microphone access in production.

---

## Deploying to GitHub Pages

Create a GitHub repository.

Example:

```text
virtual-ferrofluid-lamp
```

Add:

```text
index.html
README.md
```

Push the files to GitHub.

Then go to:

```text
Repository
→ Settings
→ Pages
```

Under **Build and deployment**:

```text
Source: Deploy from a branch
Branch: main
Folder: /root
```

Save the settings.

GitHub Pages will provide a URL similar to:

```text
https://USERNAME.github.io/virtual-ferrofluid-lamp/
```

Because GitHub Pages uses HTTPS, microphone access can work after the user grants permission.

---

## Browser Support

Recommended browsers:

- Google Chrome
- Microsoft Edge
- Firefox
- Safari
- Chrome Android
- Safari iOS

The browser must support:

- WebGL
- Web Audio API

For microphone support, it must also support:

```javascript
navigator.mediaDevices.getUserMedia()
```

---

## Performance

The project is designed to stay lightweight.

Current characteristics:

```text
Frameworks: none
External libraries: none
External assets: none
Build process: none
WebGL metaballs: up to 30
```

Performance depends on:

- device GPU
- screen resolution
- device pixel ratio
- number of droplets
- browser

The canvas device pixel ratio is capped to reduce excessive GPU load.

---

## Current Visual Model

The current implementation uses:

```text
Particle physics
        +
Metaball scalar field
        +
WebGL fragment shader
        +
Frequency-driven deformation
```

This creates smooth merging liquid shapes.

It is not a full Navier-Stokes fluid simulation.

---

## Current Interaction Model

```text
Pointer movement
      ↓
Magnetic target changes
      ↓
Fluid follows target
      ↓
Pointer velocity adds turbulence
      ↓
Extended close hover
      ↓
Split trigger
      ↓
Droplets receive outward impulse
      ↓
Split state decays
      ↓
Recovery force increases
      ↓
Droplets regroup
```

---

## Audio Processing

The analyzer uses an FFT size of:

```javascript
1024
```

The spectrum is divided into approximate bands.

### Bass

```text
0% – 8%
```

of the analyzer frequency bins.

### Mids

```text
8% – 34%
```

### Highs

```text
34% – 85%
```

These values are intentionally broad because the simulation uses them for visual response rather than precise audio mastering.

---

## Smoothing

Audio values are smoothed before they affect the simulation.

This reduces:

- visual flicker
- sudden shaking
- unstable movement
- harsh transitions

Bass, mids, and highs each have separate smoothing values.

---

## WebGL Ferrofluid Rendering

The liquid appearance is generated from a scalar field.

Each simulated droplet contributes to the field.

Conceptually:

```text
field += radius² / distance²
```

When multiple fields overlap, they visually merge.

This is what creates the metaball effect.

---

## Glass Chamber

The simulation renders a circular glass chamber around the liquid.

The shader adds:

- circular clipping
- glass shading
- light highlight
- edge shadow
- subtle bottom shading
- metallic ferrofluid highlights

---

## Ferrofluid Spike Effect

The shader adds radial oscillation around the field boundary.

The spike effect reacts primarily to:

- mids
- highs
- overall energy
- magnet strength

This is an approximation of the pointed structures formed by real ferrofluid under magnetic fields.

---

## Responsive Design

The page is responsive.

### Desktop

Layout:

```text
Simulation | Controls
```

### Mobile / Tablet

Layout changes to:

```text
Simulation
Controls
```

Touch interaction is supported through Pointer Events.

---

## Security and Privacy

Audio files selected through the upload field remain local to the browser.

The project does not upload audio to a server.

Microphone audio is processed directly inside the browser.

The current implementation does not:

- store recordings
- upload microphone audio
- use cookies
- use localStorage
- send analytics
- call external APIs

---

## Future Improvements

Several upgrades could make the simulation much closer to a real ferrofluid lamp.

### 1. Full GPU fluid simulation

Replace the current particle physics model with a GPU-based 2D fluid solver.

Possible techniques:

- Navier-Stokes simulation
- velocity field advection
- pressure projection
- vorticity confinement

---

### 2. Magnetic field simulation

Use one or more virtual magnetic poles.

This would allow the ferrofluid to create directional structures instead of only moving toward a single target.

---

### 3. Real ferrofluid Rosensweig spikes

Implement a more physically-inspired surface instability model.

This would produce long pointed ferrofluid peaks similar to real magnetic ferrofluid.

---

### 4. Dynamic spike direction

Spikes could orient themselves toward virtual magnetic poles instead of using only radial shader deformation.

---

### 5. Multi-magnet mode

Support multiple magnets moving around the chamber.

Example:

```text
Magnet A → upper left
Magnet B → lower right
Magnet C → follows pointer
```

This could create more dramatic splitting and stretching.

---

### 6. Beat detection

Add transient / beat detection so large bass hits cause specific events.

Example:

```text
Bass hit
   ↓
Ferrofluid compression
   ↓
Expansion
   ↓
Droplet burst
```

---

### 7. Tempo tracking

Estimate BPM and synchronize larger magnetic movements to the beat.

---

### 8. Presets

Possible presets:

```text
Calm
Liquid
Magnetic
Aggressive
Bass Heavy
Ambient
Galaxy
Chaotic
```

---

### 9. Fullscreen visualizer mode

Add a mode that removes the controls and displays only the ferrofluid lamp.

Useful for:

- music visualization
- installations
- screens
- projection
- ambient displays

---

### 10. Automatic UI hiding

Controls could fade away after inactivity and return when the pointer moves.

---

### 11. Background customization

Allow users to change:

- glass color
- background color
- liquid color
- chamber size
- glow
- reflections

---

### 12. Screenshot mode

Allow capturing the current ferrofluid state as a PNG image.

---

### 13. Video recording

Use `MediaRecorder` with `canvas.captureStream()` to record the visualizer.

---

### 14. Mobile gyroscope support

On compatible devices, the ferrofluid could react to phone movement.

Possible interactions:

- tilt left → fluid moves left
- tilt right → fluid moves right
- shake → droplet burst

This would require motion sensor permission on some browsers.

---

### 15. WebGL2 / GPU optimization

A future version can migrate to WebGL2 for:

- more particles
- framebuffer simulations
- texture-based particle data
- better fluid effects
- more complex magnetic fields

---

## Recommended Production Roadmap

### Phase 1 — Current Version

Complete.

Includes:

```text
WebGL metaballs
Audio analysis
Microphone input
Pointer attraction
Droplet splitting
Recovery
Interactive controls
Responsive UI
```

---

### Phase 2 — Visual Realism

Recommended next step.

Focus on:

```text
long magnetic tendrils
sharper spikes
better droplet merging
more organic stretching
surface tension
multiple magnetic poles
```

---

### Phase 3 — GPU Fluid Physics

Move the underlying fluid behavior to GPU framebuffers.

Goal:

```text
more realistic liquid motion
stronger fluid continuity
more natural turbulence
magnetic field deformation
```

---

### Phase 4 — Music Visualizer

Add:

```text
beat detection
BPM synchronization
presets
fullscreen mode
recording
performance profiles
```

---

## GitHub Repository Suggestions

Suggested repository names:

```text
virtual-ferrofluid-lamp
```

or

```text
ferrofluid-webgl
```

or

```text
sound-reactive-ferrofluid
```

---

## Suggested GitHub Description

```text
Interactive sound-reactive ferrofluid lamp simulation built with WebGL and the Web Audio API. Supports music, microphone input, metaball physics, pointer interaction, droplet splitting and magnetic re-coalescence.
```

---

## Suggested GitHub Topics

```text
webgl
ferrofluid
audio-visualizer
web-audio-api
javascript
shader
glsl
metaballs
creative-coding
music-visualizer
interactive
generative-art
```

---

## Recommended Files for GitHub

```text
virtual-ferrofluid-lamp/
│
├── index.html
├── README.md
├── LICENSE
└── .gitignore
```

Since the current application is entirely client-side, no special `.gitignore` rules are required yet.

A minimal `.gitignore` could contain:

```gitignore
.DS_Store
Thumbs.db
.vscode/
.idea/
```

---

## License

No license has been selected yet.

For an open-source repository, a common choice is the MIT License.

Example:

```text
MIT License
```

Choose the license based on how you want other people to use, modify, and redistribute the project.

---

## Development Notes

The project currently intentionally avoids third-party libraries.

This keeps it:

- portable
- easy to host
- easy to modify
- fast to load
- easy to deploy through GitHub Pages

If the simulation becomes significantly more complex, possible libraries for future versions include:

- Three.js
- PixiJS
- regl

However, they are not required for the current implementation.

---

## Known Limitations

The current simulation is an artistic approximation rather than a physically accurate ferrohydrodynamic simulation.

Current limitations include:

- no real magnetic-field physics
- no real surface-tension solver
- no Navier-Stokes fluid simulation
- maximum of 30 shader metaballs
- spikes are shader-generated approximations
- merging is based on scalar fields rather than actual liquid volume conservation
- audio frequency ranges are broad visual bands

These limitations are intentional to keep the project lightweight and browser-friendly.

---

## Goal

The long-term goal is to create a virtual ferrofluid experience that feels like a real physical ferrofluid lamp while remaining lightweight enough to run interactively inside a modern web browser.

The experience should eventually combine:

```text
realistic fluid movement
+
magnetic surface deformation
+
music reactivity
+
direct human interaction
```

without requiring a native application or dedicated graphics software.

## Version

Current prototype:

```text
v0.2
```

Current milestone:

```text
Interactive sound-reactive WebGL ferrofluid prototype
```
