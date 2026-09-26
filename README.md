<p align="center">
  <img src="assets/readme/hero.svg" width="100%" alt="StrainLink: synchrotron in-situ tensile data mapping tool.">
</p>

# StrainLink｜同步辐射原位拉伸数据映射工具

**Map missing stress or strain in in-situ SXRD tensile tables using a reference σ–ε curve.**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3%2B%20(tkinter)-green.svg)](https://www.python.org/downloads/)

Desktop **Tk** GUI (v3). Each table row is one spectrum / frame / acquisition. A complete lab reference stress–strain curve fills the missing column, converts units, checks alignment, and exports publication-ready plots.

<p align="center">
  <img src="assets/readme/section-01-map.svg" width="100%" alt="01 Map: reference curve fills station gaps.">
</p>

## Features

| Station has… | Mapper does… |
|--------------|--------------|
| Strain only | Interpolate → stress |
| Stress only | Inverse-interpolate → strain |
| Both | Units · alignment check · export |

- **PCHIP** shape-preserving interpolation when SciPy is available; otherwise linear fallback
- Optional Savitzky–Golay / smoothing guides (SciPy signal)
- Unit warnings (fraction vs percent strain; stress in MPa)
- High-contrast plotting and publication export presets
- Excel / CSV friendly table I/O via pandas + openpyxl

## Install / Quick start

Windows (double-click):

```text
start_stress_strain_mapper.bat
```

From source:

```powershell
pip install pandas numpy matplotlib scipy openpyxl
python sxrd_stress_strain_mapper_gui_v3.py
```

Requires Python 3 with **tkinter** (standard on most Windows / macOS Python installs).

## Usage

1. Load a **complete** lab reference σ–ε curve.
2. Load the beamline / station table (one row per frame).
3. Choose which column is missing (stress or strain) and confirm units.
4. Map → review overlay → export aligned table and plots.

## Scientific boundary — what it is NOT

- **Not** a constitutive material model, crystal plasticity solver, or FEM post-processor
- **Not** a DIC / virtual-extensometer strain extractor (see [StrainTrace](https://github.com/D-sudoasd/StrainTrace), formerly ezDIC, for image-based strain)
- Output quality **tracks the reference curve**; garbage in → garbage out
- Always verify **fraction vs percent** strain before publishing figures or tables

## Tests

```powershell
python -m unittest tests/test_stress_strain_mapper.py -v
```

## License

MIT — see [LICENSE](LICENSE).
