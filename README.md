# RadioML 2018 O'Shea Paper Reproduction

This repository contains a PyTorch reproduction of the ResNet-based automatic modulation classification experiment from:

**T. J. O'Shea, T. Roy, and T. C. Clancy, "Over-the-Air Deep Learning Based Radio Signal Classification," IEEE Journal of Selected Topics in Signal Processing, 2018.**

Paper DOI: [10.1109/JSTSP.2018.2797022](https://doi.org/10.1109/JSTSP.2018.2797022)

I built this as the first implementation task during my IIT Indore internship. The goal was to understand how raw I/Q radio samples can be classified directly with deep learning, reproduce the paper's key RadioML-style results, and explore the paper's open question about Cartesian I/Q versus polar amplitude/phase representations.

## What Is Included

- A cleaned Jupyter notebook reproduction of the O'Shea ResNet workflow.
- Balanced loading of the 24-class RadioML difficult modulation set.
- ResNet-style 1D convolutional classifier for raw I/Q samples.
- Accuracy versus SNR evaluation.
- High-SNR confusion matrix analysis.
- Constellation visualizations for all modulation classes.
- A polar representation experiment using amplitude and phase features.

## Repository Layout

```text
.
â”œâ”€â”€ notebooks/
â”‚   â””â”€â”€ oshea_radioml_reproduction.ipynb
â”œâ”€â”€ figures/
â”‚   â”œâ”€â”€ accuracy_vs_snr.png
â”‚   â”œâ”€â”€ confusion_matrix.png
â”‚   â”œâ”€â”€ constellation_diagrams.png
â”‚   â””â”€â”€ polar_vs_cartesian.png
â”œâ”€â”€ data/
â”‚   â””â”€â”€ README.md
â”œâ”€â”€ requirements.txt
â”œâ”€â”€ .gitignore
â””â”€â”€ README.md
```

## Dataset

The notebook expects the RadioML HDF5 file here:

```text
data/GOLD_XYZ_OSC.0001_1024.hdf5
```

The dataset file is intentionally ignored by Git because it is very large. Keep it locally in `data/` before running the notebook.

The paper PDF is also not included in the repository. See [REFERENCES.md](REFERENCES.md) for the formal citation, DOI link, and dataset note.

## Main Result Snapshot

Using a reduced balanced subset of the dataset:

- 24 modulation classes
- 4,000 examples per class
- 96,000 examples total
- 80/20 train/test split
- 30 training epochs

The reproduced Cartesian I/Q ResNet reached about **66.9% average accuracy at SNR >= 10 dB**.

The polar amplitude/phase experiment reached about **78.2% average accuracy at SNR >= 10 dB** in this run. This is an exploratory result and should be validated with more random seeds and larger training subsets before making a strong claim.

## How To Run

Create an environment and install dependencies:

```bash
pip install -r requirements.txt
```

Place the dataset at:

```text
data/GOLD_XYZ_OSC.0001_1024.hdf5
```

Then run:

```bash
jupyter notebook notebooks/oshea_radioml_reproduction.ipynb
```

Run the notebook from the repository root so that the relative `data/` and `figures/` paths resolve correctly.

## Notes

This is a reproduction and learning implementation, not a bit-for-bit clone of the paper. The model is smaller than the paper's reported ResNet parameter count and uses a reduced training subset instead of the full million-scale setup. The reproduced trends, confusion patterns, and SNR behavior are the important comparison points.
