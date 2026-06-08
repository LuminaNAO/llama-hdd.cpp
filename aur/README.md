# llama-hdd AUR package

Reference PKGBUILD for the `llama-hdd` AUR package. The canonical AUR repo (when published) lives separately; this copy is for tracking the package recipe alongside the source.

## Build a backend variant

```sh
# CPU (default)
makepkg -si

# Vulkan
LLAMA_HDD_BACKEND=vulkan makepkg -si

# ROCm (Strix Halo: gfx1151; RDNA3 dGPU: gfx1100)
LLAMA_HDD_BACKEND=rocm AMDGPU_TARGETS=gfx1151 makepkg -si

# CUDA
LLAMA_HDD_BACKEND=cuda makepkg -si
```

## Provides / conflicts

`llama-hdd` declares `provides=('llama.cpp')` and conflicts with the official `llama.cpp*` packages. Installing it transparently substitutes upstream — anything that depends on `llama.cpp` (e.g. `llamacpp-helper` via `optdepends`) is satisfied.

## Versioning

`pkgver` is derived from `git describe`: `b<upstream-tag>.r<commits-since-tag>`. Upstream merges bump the tag; fork-only commits bump the `.r` suffix. `pkgrel` is for PKGBUILD changes that don't change the source.
