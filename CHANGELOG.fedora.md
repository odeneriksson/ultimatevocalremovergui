# Fedora / Linux adaptation changelog

## 2026-10-18 — Initial Fedora 44 adaptation (working tree)

This document describes **changes present in the supplied local diff** relative to its Git base. It is not an upstream release changelog, and individual changes have not been independently tested on all platforms.

### Compatibility
- On Linux, prefer a system-installed `tkdnd` package rather than the bundled platform binary. Keep the platform-specific bundled loading paths for Windows and macOS.
- Remove the hard requirement for Tk 8.6 in the dark theme so that the theme can load with newer Tk versions.

### GUI scaling and layout
- Add a configurable `UVR_UI_SCALE` factor (default `1.6`, clamped to `1.0`–`2.5`) for the legacy Tk `place`-based GUI and matching window/section dimensions.
- Rework input/output path controls and option placements to accommodate the scaled interface.
- Add Fedora-specific checkbutton styling and adjust checkbutton placement to prevent label truncation.
- Reposition the Start Processing / settings / stop controls, console and progress bar with a `<Configure>`-driven footer layout.
- Preserve multiple `<Configure>` handlers by registering the existing position handler with `add="+"`.

### Help and status output
- Display hover help inside the main window and avoid duplicate scaling of its pixel coordinates; delay hover hints by 500 ms.
- Suppress the generic upstream update-available console message on Linux while retaining the update check and model-related data functionality.

### Scope and limitations
- `models/**/model_data/*.json` changes in the supplied working-tree diff are deliberately **excluded** from the distributable patch: they are model catalog / metadata changes, not the Fedora GUI adaptation. Review and commit those separately only if intended.
- The supplied diff does **not** include changes to Python dependencies, install instructions or `gui_data/tkinterdnd2/tkdnd` binaries. Those are not claimed here.
- Validation here covers patch structure and Python syntax in reconstructed changed files; full Fedora GNOME / XWayland integration and audio processing are **not** tested as part of building this patch.
