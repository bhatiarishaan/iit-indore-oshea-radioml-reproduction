# RadioML 2018 O'Shea Reproduction with Polar Feature Extension

This repository contains a PyTorch reproduction and extension of the ResNet-based automatic modulation classification experiment from:

**T. J. O'Shea, T. Roy, and T. C. Clancy, "Over-the-Air Deep Learning Based Radio Signal Classification," IEEE Journal of Selected Topics in Signal Processing, 2018.**

Paper DOI: [10.1109/JSTSP.2018.2797022](https://doi.org/10.1109/JSTSP.2018.2797022)

I built this as the first implementation task during my IIT Indore internship. The first goal was to reproduce the paper's raw I/Q ResNet pipeline on the RadioML 2018-style dataset. After that, I extended the experiment by testing a polar amplitude/phase input representation, which the paper identifies as an interesting direction for further study.

## What I Added Beyond Reproduction

The O'Shea paper primarily uses Cartesian I/Q samples as the neural network input. In the discussion, the authors note that the choice of input representation may affect classification performance and mention polar representation as a possible direction to explore.

This repository includes a direct controlled comparison between:

- Cartesian I/Q input: `(I, Q)`
- Polar input: `(amplitude, phase)`

Both models use the same ResNet architecture, the same balanced dataset subset, the same train/test split, and the same training schedule. This makes the comparison focused on the input representation rather than changes in model design or data selection.

## What Is Included

- Reproduction of the O'Shea ResNet workflow for raw I/Q modulation classification.
- Balanced loading of the 24-class RadioML difficult modulation set.
- Accuracy versus SNR evaluation for the Cartesian I/Q baseline.
- High-SNR confusion matrix analysis.
- Constellation visualizations for all modulation classes.
- A polar amplitude/phase experiment motivated by the paper's future-work discussion.
- A final Cartesian versus polar comparison plot.

## Repository Layout

```text
.
|-- notebooks/
|   `-- oshea_radioml_reproduction.ipynb
|-- figures/
|   |-- accuracy_vs_snr.png
|   |-- confusion_matrix.png
|   |-- constellation_diagrams.png
|   `-- polar_vs_cartesian.png
|-- data/
|   `-- README.md
|-- .gitattributes
|-- .gitignore
|-- README.md
|-- REFERENCES.md
`-- requirements.txt
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

The polar amplitude/phase model reached about **78.2% average accuracy at SNR >= 10 dB** in this run.

This result suggests that polar representation can be a useful feature transformation for this reduced-data RadioML setting. I treat it as an experimental finding rather than a final claim, because a stronger conclusion would require more random seeds, larger training subsets, and closer matching to the full training scale used in the paper.

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

This is a reproduction and extension project, not a bit-for-bit clone of the paper. The ResNet used here is smaller than the parameter count reported in the paper, and the experiment uses a reduced balanced subset instead of the full million-scale setup. The main value of the project is the end-to-end reproduction workflow, the SNR and confusion analysis, and the added polar-coordinate comparison inspired by the paper's discussion.