# XeniaVR

XeniaVR is a VR-focused fork built on Xenia Canary, targeting OpenXR headset support for Xbox 360 titles.

## What This Fork Adds
- OpenXR runtime integration path with VR rendering and VR input bridge modules.
- In-app VR settings dialog with per-title VR config save/install workflows.
- VR rendering controls for mode, depth source, swapchain sizing/scaling, and per-eye camera behavior.
- VR diagnostics controls (debug overlay, debug logging, performance summary/snapshot toggles).
- Stability and teardown cleanup across thread/timer/event flows.
- Submodule-pinned third-party dependency layout for reproducible builds.

## User Options

### GUI (`VR` menu)
- `VR (OpenXR)` opens the VR settings dialog.
- `Toggle VR runtime (restart required)`.
- `Toggle VR debug overlay`.
- `Save VR settings to current game config` when a title is running.
- `Install bundled VR presets to config folder`.
- `Open VR config folder`.
- `Open Vulkan VR smoke checklist`.

### In-Dialog Controls
- Runtime and input: VR runtime, input enhancements, comfort features, controller preset.
- Rendering: render mode, output pass mode, eye selection, depth source.
- Swapchain/scaling: size mode, scaling mode, CAS sharpness, FSR sharpness reduction.
- Per-eye camera: mode, hybrid scaling allowance, guest camera override/eye/auto-eye/strength.
- Input tuning: aim deadzone, aim curve, aim sensitivity, trigger deadzone, invert X/Y.
- Diagnostics: debug overlay, debug logging, perf summary on exit, one-shot perf snapshot, stereo scaffold toggle.

### Command-Line / Config (`vr_*`)
- Core: `vr_enable`, `vr_enable_input_enhancements`, `vr_enable_comfort_features`.
- Rendering/depth: `vr_render_mode`, `vr_depth_source`, `vr_output_pass_mode`, `vr_output_single_eye`.
- Swapchain/scaling: `vr_swapchain_size_mode`, `vr_swapchain_scaling_mode`, `vr_cas_sharpness`, `vr_fsr_sharpness_reduction`.
- Per-eye camera: `vr_per_eye_camera_mode`, `vr_hybrid_allow_shader_scaling`, `vr_guest_camera_override`, `vr_guest_camera_eye`, `vr_guest_camera_auto_eye`, `vr_guest_camera_strength`.
- Input tuning: `vr_aim_deadzone`, `vr_aim_curve`, `vr_aim_sensitivity`, `vr_trigger_deadzone`, `vr_invert_aim_x`, `vr_invert_aim_y`, `vr_map_left_thumbstick_to_dpad`, `vr_controller_preset`.
- Diagnostics: `vr_debug_overlay`, `vr_debug_logging`, `vr_perf_summary_on_exit`, `vr_perf_snapshot`, `vr_true_stereo_scaffold`.

Example:

```powershell
xenia_canary.exe --vr_enable=true --vr_render_mode=stereo_fast --vr_depth_source=host --vr_swapchain_scaling_mode=fsr
```

## Current Priority TODO
- Depth reprojection validation on real titles for D3D12 and Vulkan.
- Complete true stereo path and full per-eye guest camera integration.
- Expand diagnostics polish and per-title perf reporting.

## Build Notes
```powershell
git clone --recurse-submodules <repo-url>
# or, after clone:
git submodule update --init --recursive
```

## Original Xenia Canary README
The section below is preserved from upstream for reference.

<details>
<summary>Show original README</summary>
<p align="center">
    <a href="https://github.com/xenia-canary/xenia-canary/tree/canary_experimental/assets/icon">
        <img height="256px" src="https://raw.githubusercontent.com/xenia-canary/xenia/master/assets/icon/256.png" />
    </a>
</p>

<h1 align="center">Xenia Canary - Xbox 360 Emulator</h1>

Xenia Canary is an experimental fork of the Xenia emulator. For more information, see the
[Xenia Canary wiki](https://github.com/xenia-canary/xenia-canary/wiki).

Come chat with us about **emulator-related topics** on [Discord](https://discord.gg/Q9mxZf9).
For developer chat join `#dev` but stay on topic. Lurking is not only fine, but encouraged!
Please check the [FAQ](https://github.com/xenia-canary/xenia-canary/wiki/FAQ) page before asking questions.
We've got jobs/lives/etc, so don't expect instant answers.

Discussing illegal activities will get you banned.

## Status

Buildbot | Status | Releases
-------- | ------ | --------
Windows | [![CI](https://github.com/xenia-canary/xenia-canary/actions/workflows/Windows_build.yml/badge.svg?branch=canary_experimental)](https://github.com/xenia-canary/xenia-canary/actions/workflows/Windows_build.yml) [![Codacy Badge](https://app.codacy.com/project/badge/Grade/cd506034fd8148309a45034925648499)](https://app.codacy.com/gh/xenia-canary/xenia-canary/dashboard?utm_source=gh&utm_medium=referral&utm_content=&utm_campaign=Badge_grade) | [Latest](https://github.com/xenia-canary/xenia-canary-releases/releases/latest) â—¦ [All](https://github.com/xenia-canary/xenia-canary-releases/releases) â—¦ [Old](https://github.com/xenia-canary/xenia-canary/releases)
Linux | [![CI](https://github.com/xenia-canary/xenia-canary/actions/workflows/Linux_build.yml/badge.svg?branch=canary_experimental)](https://github.com/xenia-canary/xenia-canary/actions/workflows/Linux_build.yml)
Netplay Build | | [Latest](https://github.com/AdrianCassar/xenia-canary/releases/latest)

## Quickstart

See the [Quickstart](https://github.com/xenia-canary/xenia-canary/wiki/Quickstart) page.

## FAQ

See the [frequently asked questions](https://github.com/xenia-canary/xenia-canary/wiki/FAQ) page.

## Game Compatibility

See the [Game compatibility list](https://github.com/xenia-canary/game-compatibility/issues)
for currently tracked games, and feel free to contribute your own updates,
screenshots, and information there following the [existing conventions](https://github.com/xenia-canary/game-compatibility/blob/canary/README.md).

## Building

See [building.md](docs/building.md) for setup and information about the
`xb` script. When writing code, check the [style guide](docs/style_guide.md)
and be sure to run clang-format!

## Contributors Wanted!

Have some spare time, know advanced C++, and want to write an emulator?
Contribute! There's a ton of work that needs to be done, a lot of which
is wide open greenfield fun.

**For general rules and guidelines please see [CONTRIBUTING.md](.github/CONTRIBUTING.md).**

Fixes and optimizations are always welcome (please!), but in addition to
that there are some major work areas still untouched:

* Help work through [missing functionality/bugs in games](https://github.com/xenia-canary/xenia-canary/labels/compat)
* Reduce the size of Xenia's [huge log files](https://github.com/xenia-canary/xenia-canary/issues/1526)
* Skilled with Linux? A strong contributor is needed to [help with porting](https://github.com/xenia-canary/xenia-canary/labels/platform-linux)

See more projects [good for contributors](https://github.com/xenia-canary/xenia-canary/labels/good%20first%20issue). It's a good idea to ask on Discord and check the issues page before beginning work on
something.

## Disclaimer

The goal of this project is to experiment, research, and educate on the topic
of emulation of modern devices and operating systems. **It is not for enabling
illegal activity**. All information is obtained via reverse engineering of
legally purchased devices and games and information made public on the internet
(you'd be surprised what's indexed on Google...).

</details>
