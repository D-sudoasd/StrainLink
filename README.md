<p align="center">
  <img src="assets/readme/hero.svg" width="100%" alt="Stress-Strain Mapper: complete missing stress or strain for in-situ SXRD tensile tables.">
</p>

# Stress–Strain Mapper

**Complete missing stress or strain for in-situ SXRD tensile tables using a reference curve.**

Desktop Tk GUI (v3) for beamline-style tables where **each row is one spectrum / frame / acquisition**. A complete lab reference stress–strain curve is used to fill the missing column, convert units, check alignment, and export plots.

## Typical cases

| Station table has… | Mapper does… |
|--------------------|--------------|
| Strain only | Interpolate reference → stress |
| Stress only | Inverse-interpolate reference → strain |
| Both | Convert units, check, export aligned table |

## Method

- **PCHIP** shape-preserving interpolation when SciPy is available  
- Automatic fallback to **linear** interpolation without SciPy  
- Optional smoothing guides (rolling median/mean, Savitzky–Golay if SciPy signal available)  
- Unit awareness for strain (fraction / percent) and stress (MPa / GPa / Pa)  
- Publication export presets (PNG/PDF sizing and DPI)

## Run

**Windows (recommended):** double-click

```text
start_stress_strain_mapper.bat
```

The launcher finds Python 3, installs `pandas numpy matplotlib scipy openpyxl` if needed, and starts:

```text
sxrd_stress_strain_mapper_gui_v3.py
```

From a shell:

```powershell
pip install pandas numpy matplotlib scipy openpyxl
python sxrd_stress_strain_mapper_gui_v3.py
```

Requires Python 3 with **tkinter** support.

## Workflow (GUI)

1. Load **reference** stress–strain curve.  
2. Load **station** table (one row per frame).  
3. Choose mode: strain-only / stress-only / both.  
4. Confirm units and interpolation method.  
5. Map, inspect plot, export table + figures.  

## Tests

```powershell
python -m unittest tests/test_stress_strain_mapper.py -v
```

## Limits

- Interpolation quality tracks the **reference curve** quality and coverage.  
- Not a constitutive model or DIC/strain-mapping solver — table alignment only.  
- Always check units (fraction vs percent strain) before publishing.  

## License

MIT — see [LICENSE](LICENSE).
