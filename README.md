# Synth City Radio

A vaporwave-styled desktop music player with a real-time 3D visualiser, written in C++ on raw OpenGL 3.3.

Pick a folder of music, and the app plays it inside a neon city scene: a texture-mapped skybox, a glowing sun, a perspective grid, and on-screen transport controls rendered with custom GLSL shaders.

## Features

- **Playback** of `.ogg`, `.wav` and `.flac` files from a folder chosen through a native file dialog
- **Transport controls** drawn in OpenGL: previous / play-pause / next buttons, a seek slider, and a volume bar, all clickable with the mouse
- **Track info** (title, elapsed and total time) rendered with FreeType
- **Free camera**: look around the scene with the keyboard
- **Audio on its own thread**, so playback never stalls the render loop; frame rate capped at 60 FPS

## Controls

| Input | Action |
|---|---|
| Mouse | Click buttons, drag seek slider, set volume |
| `W` `A` `S` `D` | Pitch / yaw the camera |
| Numpad `+` / `-` | Volume up / down |
| `Esc` | Quit |

## Tech

| Concern | Library |
|---|---|
| Window and input | GLFW 3.4 |
| OpenGL loading | GLEW 2.2 |
| Math | GLM |
| Text rendering | FreeType |
| Audio | SFML Audio |
| Textures | stb_image |
| File dialog | tinyfiledialogs |

Rendering is done with hand-written vertex and fragment shaders in `SynthCityRadio2D/Shaders/` (one pair each for the skybox cube, grid, sun, controls, volume bar and text). No engine or UI framework is used.

## Building

The project is a Visual Studio 2022 solution (`SynthCityRadio2D/SynthCityRadio2D.sln`), x64.

1. Open the solution in Visual Studio. GLFW, GLEW, GLM and FreeType are pulled in as NuGet packages on first restore.
2. Install [SFML](https://www.sfml-dev.org/) and point the project's include and library paths at it.
3. Add two textures to `SynthCityRadio2D/Textures/` (they are git-ignored): `city-background.png` for the skybox sides and `night-sky.jpg` for the top face.
4. Build and run. The shader and texture paths are relative, so run from the `SynthCityRadio2D` directory.

## Project layout

```
SynthCityRadio2D/
├── main.cpp            render loop, camera, input handling
├── graphics_utils.*    VAO/VBO setup, shader loading, draw calls, text rendering
├── music_utils.*       folder picking, SFML playback, play/pause/next/prev/seek
├── globals.h           shared state and static vertex data
└── Shaders/            GLSL vertex and fragment shaders
```
