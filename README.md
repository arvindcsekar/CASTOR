# CASTOR

Modelling early-time (shock breakout) emission of Type IIP supernovae in the target uv, u, and g bands of the [CASTOR](https://www.castormission.org/) (Cosmological Advanced Survey Telescope for Optical and ultraviolet Research) space telescope, and how detectability varies with progenitor radius, explosion energy, and mass.

## Overview

This project models the bolometric and band-specific luminosity of Type IIP supernovae at the instant of shock breakout, using an analytic luminosity relation (Arnett 1980) combined with a blackbody (Planck function) treatment to determine spectral flux density in CASTOR's three target bands:

| Band | Wavelength range |
|------|-------------------|
| uv   | 150–300 nm |
| u    | 300–400 nm |
| g    | 400–500 nm |

Progenitor radius, thermal explosion energy, and ejecta mass are each varied in turn (and jointly, via contour plots) to determine which progenitor configurations are most detectable by CASTOR at shock breakout.

Full methodology, results, and discussion are in [`docs/progenitor-parameters-paper.pdf`](docs/progenitor-parameters-paper.pdf).

## Installation

```bash
git clone https://github.com/arvindcsekar/CASTOR.git
cd CASTOR
pip install -r requirements.txt
```

## Usage

```bash
python src/castor.py
```

Running the script reproduces the blackbody spectra, luminosity tables, and contour plots described in the paper for the default progenitor case (and parameter variations), as summarized below.

## Default Model

Baseline progenitor parameters:

| Parameter | Value |
|---|---|
| Radius | 10¹³ cm |
| Explosion energy | 10⁵¹ erg |
| Ejecta mass | 10 M☉ |

| Quantity | Value |
|---|---|
| Bolometric luminosity | 5.2 × 10³⁴ W |
| Bolometric flux | 4.138 × 10¹¹ W/m² |
| Temperature | 51,976 K |
| Peak wavelength | 55.76 nm |
| UV % of bolometric | 12.41% |

**Luminosity by band:**

| Band | Flux (W/m²) | Luminosity (W) | % of L_bol |
|---|---|---|---|
| uv | 5.137 × 10¹⁰ | 6.455 × 10³³ | 12.41% |
| u  | 6.238 × 10⁹  | 7.839 × 10³² | 1.51% |
| g  | 2.471 × 10⁹  | 3.105 × 10³² | 0.60% |

## Parameter Variations

| Variation | Temperature | Peak λ | Luminosity | UV % of L_bol |
|---|---|---|---|---|
| Radius 10¹² cm | 92,428 K | 31.35 nm | 5.2 × 10³³ W | 3.22% |
| Radius 10¹⁴ cm | 29,228 K | 99.15 nm | 5.2 × 10³⁵ W | 33.67% |
| Mass 5 M☉  | 61,810 K | — | 1.04 × 10³⁵ W | 8.50% |
| Mass 20 M☉ | 43,706 K | — | 2.6 × 10³⁴ W | 17.59% |
| Energy 10⁵⁰ erg | 29,228 K | — | 5.2 × 10³³ W | 33.67% |
| Energy 10⁵² erg | 92,428 K | — | 5.2 × 10³⁵ W | 3.22% |

Full data: [`docs/castor-default-data.md`](docs/castor-default-data.md).

## Key Result

Larger radii and higher explosion energies increase both total and band-specific luminosity, and shift peak emission closer to CASTOR's bands — improving detectability. Higher progenitor mass has the opposite effect, lowering both luminosity and band-specific detectability. As temperature rises, emission shifts toward the extreme-UV/soft X-ray, moving outside CASTOR's UV band even as total flux increases — so **large radius, low mass, and high explosion energy** together maximize early-time detectability in CASTOR's target bands.

## Repository Structure

```
CASTOR/
├── src/
│   └── castor.py                  # main script: computes spectra, luminosities, generates plots
├── docs/
│   ├── progenitor-parameters-paper.pdf   # full writeup
│   └── castor-default-data.md            # full parameter-variation data tables
├── figures/                        # generated plots
├── requirements.txt
└── README.md
```

## Assumptions and Limitations

- Constant photospheric opacity of 0.4 cm²/g, assuming ideal blackbody emission — may not hold under non-LTE or line-dominated atmospheres.
- Ideal bandpass efficiencies assumed; real observations will differ.

## References

1. Kasen, D., & Woosley, S. E. 2009, ApJ, 703, 2205. [arXiv:0910.1590](https://arxiv.org/pdf/0910.1590)
2. Nakar, E., & Sari, R. 2010, ApJ, 725, 904. [arXiv:1002.3414](https://arxiv.org/pdf/1002.3414)
3. Arnett, W. D. 1980, ApJ, 237, 541.
4. Gomez, S., et al. 2024. [arXiv:2402.08137](https://arxiv.org/abs/2402.08137)
5. Chandrasekhar, S. 1967, NASA Technical Report, NASA-TN-D-4025.

## Author

Arvind Chandrasekar
