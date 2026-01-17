# Sindri Engine

A cross-platform game engine written in Rust, targeting Windows and Linux with a modern GPU rendering pipeline.

---

## Devlog — 2026-01-16

### Milestone: First Render (Triangle)

The Sindri Engine successfully completed its first rendering milestone.

The engine initializes a window, selects a GPU adapter, builds a graphics pipeline, and renders geometry using a custom render loop. While the output is a simple triangle, this confirms that the core rendering stack is functional end-to-end.

---

## Current Architecture

Sindri is structured as a Rust workspace with clear separation of responsibilities:

- **sindri_core**  
  Engine core logic. Intended for world data, chunk systems, meshing, ECS, and shared engine utilities.

- **sindri_client**  
  Client-side application. Handles window creation, input, rendering, and presentation.

- **sindri_server**  
  Planned authoritative simulation and networking layer.

This layout is designed to support both single-player and networked use cases without major refactors.

---

## Platform & Rendering Stack

- **Windowing / Events:** `winit`
- **Rendering API:** `wgpu`
- **Languages:** Rust
- **Targets:** Windows, Linux

The engine uses wgpu to provide a modern, cross-platform abstraction over Vulkan, DirectX 12, and Metal. This avoids platform-specific renderer implementations while maintaining access to modern GPU features.

---

## Runtime Options

The client supports basic runtime flags for compatibility and debugging:

- `--fallback-gpu`  
  Forces use of a fallback (CPU) adapter.

- `--low-power`  
  Requests a low-power GPU preference when selecting an adapter.

At startup, the engine prints adapter and backend information to assist with diagnostics on different systems.

---

## Verified Functionality

- Window creation and event loop
- GPU adapter selection and surface configuration
- Graphics pipeline creation
- Stable render loop and frame presentation
- Successful rendering on Windows (MSVC toolchain)

---

## Running the Client

```bash
cargo run -p sindri_client
cargo run -p sindri_client -- --fallback-gpu
cargo run -p sindri_client -- --low-power
```
### Planned Next Steps

Render an indexed cube with depth buffering

Implement a camera system (keyboard + mouse)

Generate and render a minimal voxel chunk mesh

Establish the first in-engine world representation
