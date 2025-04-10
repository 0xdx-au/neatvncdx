# neatvncdx (patched for whodx)

## Introduction

This is a fork of the original [neatvnc](https://github.com/any1/neatvnc) project, maintained for secure integration within the [`whodx`](https://github.com/0xdx-au/whodx) hardened remote desktop platform.

> 🎯 This version removes all H.264 encoding support to ensure compatibility, simplify builds, and maintain long-term reproducibility in Dockerized environments.

---

## Why This Fork?

The original upstream repository:
- Introduced `h264_encoder_create()`/`destroy()` logic without static linkage or proper wrap fallback
- Lacks stable tags or release versions
- Breaks reproducible builds due to dependency volatility

This fork:
- ✅ **Removes** `have_working_h264_encoder()` and OpenH264 blocks in `src/server.c`
- ✅ Ensures Meson/Ninja build **without FFmpeg**, H.264, or broken `libav*` dependencies
- ✅ Is pinned and patched specifically for containerized headless deployment

---

## Goals
- ⚡ Speed
- ✨ Clean interface
- 🧱 Hardened for ephemeral desktops in TOR/VNC isolation
- ♻️ Reproducible builds (CI/CD-ready)

---

## Building

### Runtime Dependencies
- aml - https://github.com/any1/aml/
- pixman
- zlib
- (others optional but not required)

### Build Dependencies
- libdrm
- meson
- pkg-config
- ninja

### Build Instructions

```bash
meson setup build
ninja -C build
```

---

## Project: [`whodx`](https://github.com/0xdx-au/whodx)

This fork powers the core secure display layer of `whodx`, a hardened, containerized desktop streaming system leveraging:
- Wayland + Weston
- TOR
- noVNC
- Ephemeral self-destructing volumes
