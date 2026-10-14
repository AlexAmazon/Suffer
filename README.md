# Suffer

**Original visual effects for** [**EffectCraft**](https://github.com/storytold/effectcraft)**, written in Rust and compiled to WebAssembly plug-ins.**

Suffer is a growing set of motion-graphics effects (glows, glints, distortions, VHS and TV damage, film wear and more). It is inspired by the *kind* of look found in commercial effects suites, but every effect here is written from scratch from publicly known techniques. No third-party code, presets or textures are used.

> **Status: early / alpha.** The effects are built and tuned by reasoning rather than on lots of real footage yet. Expect rough edges, odd default values and the occasional bug. Bug reports and "this looks wrong" screenshots are very welcome.

---

## Effects

| Effect | What it does |
| --- | --- |
| **Glint Rainbow** | Star-shaped glints on bright spots, with the colour cycling along each ray |
| **Glint** | The same star glints in the source colour (or white) |
| **Glow** | Soft bloom from highlights, with size, falloff and tint |
| **Rays** | Light rays streaming outward from a point |
| **Shake** | Procedural camera shake (position, rotation, zoom) with motion blur |
| **Waves** | Travelling sine ripples |
| **Vortex** | Twist around a point |
| **Blur** / **Directional Blur** | Gaussian-style and straight-line blur |
| **Distort**, **Distort RGB**, **Distort Chroma**, **Distort Blur** | Refraction-style warps driven by a built-in lens (source brightness, animated noise, or a round bump) |
| **VHS Damage** | Tracking errors, colour bleed, tape noise, dropouts, scanlines |
| **TV Damage** | CRT curvature, horizontal hold, vertical roll, ghosting, interference, static, hum bars |
| **Film Damage** | Grain, scratches, dust, flicker, gate weave |
| **Edge Detect** | Sobel edges, white or source colour |
| **Duotone** | Maps brightness onto a two-colour gradient |

17 effects so far, with more planned (lightning, lens flare, light leaks, pixel sorting and others).

---

## Install a plug-in

1. Download a build from the **Releases** page (or build it yourself, see below).
2. In EffectCraft, select a layer and choose **Effect \> Load Effect Plug-in...**
3. Pick a `.wasm` file from the `dist` folder (for example `suffer_glow.wasm`).

Each effect is its own `.wasm` file, so you only load the ones you want.

---

## Build it yourself (Windows, PowerShell)

You do **not** need Visual Studio.

```
# 1. Install Rust (once), then open a NEW PowerShell window
winget install Rustlang.Rustup

# 2. Add the WebAssembly target (once)
rustup target add wasm32-unknown-unknown

# 3. Go to this folder and build everything
cd path\to\suffer-suite
.\build.bat
```

The finished plug-ins appear in the `dist` folder. If one effect fails to build, the others still build and the script lists which one failed.

To build a single effect:

```
cargo build --release --target wasm32-unknown-unknown -p suffer_glow
```

---

## Repository layout

```
common/        shared code (sampling, blurs, noise, colour, lens, glint engine)
<effect>/      one folder per effect: Cargo.toml + src/lib.rs
build.bat      builds every effect into dist\
CLAUDE.md      notes for AI coding assistants (project rules and status)
```

To add an effect, copy a small one such as `blur/`, rename it, edit `src/lib.rs`, then add its folder name to `Cargo.toml` and `build.bat`.

---

## Contributing

- Bug reports: say which effect, the parameter values, your resolution, and attach a screenshot if you can.
- Pull requests are welcome. Please keep effects **clean-room**: work from publicly described behaviour only, and do not copy code, presets, textures or parameter sets from commercial products.
- Speed matters. Plug-ins run in an interpreter, so keep per-pixel work small and use the reduced-resolution helpers in `common/` for soft effects.

---

## Support the project

Suffer is free and made in spare time. If it is useful to you, a tip on Ko-fi helps keep it going. Thank you!
<a href="https://ko-fi.com/alexamazon" target="_blank">
  <img src="![Support me on Ko-fi](https://shields.io)]" alt="Support me on Ko-fi" height="36">
</a>

---

## Credits and disclaimer

- Built for [EffectCraft](https://github.com/storytold/effectcraft) by storytold (MIT / Apache-2.0).
- Suffer is an independent project. It is **not affiliated with, endorsed by, or sponsored by** Boris FX, Adobe or Maxon. "Sapphire", "After Effects" and any other product names are trademarks of their respective owners and are mentioned only to describe the kind of effect.

## License

Dual licensed under **MIT** or **Apache-2.0**, at your option, matching EffectCraft. Add `LICENSE-MIT` and `LICENSE-APACHE` files to the repository root before publishing.
