---
layout: default
title: Python Implementation
parent: WFDB Software
nav_order: 4
---

# WFDB Python Package

The **WFDB Python package** is a native Python library for reading, writing, processing, and visualizing physiologic signal and annotation data. It adheres to the WFDB format specification and is designed to be user-friendly for researchers and developers working with biomedical waveform data.

---

## Installation

You can install the latest stable release from PyPI:

```bash
pip install wfdb
```

For the development version or to contribute:

```bash
git clone https://github.com/MIT-LCP/wfdb-python.git
cd wfdb-python
pip install .
```

To install with development dependencies:

```bash
pip install ".[dev]"
```

---

## Repository and Contributions

- **Source code**: [MIT-LCP/wfdb-python](https://github.com/MIT-LCP/wfdb-python)
- **Documentation**: [wfdb.readthedocs.io](https://wfdb.readthedocs.io/)

Contributions are welcome! Please refer to the [DEVELOPING.md](https://github.com/MIT-LCP/wfdb-python/blob/main/DEVELOPING.md) guide for instructions on contributing, including code style, testing, and documentation requirements.

---

## Basic Usage Example

```python
import wfdb

# Download and read a WFDB record from PhysioNet
record = wfdb.rdrecord('100', pn_dir='mitdb')

# Plot the signal
wfdb.plot_wfdb(record=record, title='Record 100 from MIT-BIH Arrhythmia Database')
```

This example reads record `100` from the MIT-BIH Arrhythmia Database hosted on PhysioNet and plots the signal.

---

## Features

- Read and write WFDB signal (`.dat`) and header (`.hea`) files
- Read and write annotation files (`.atr`, `.ann`, etc.)
- Support for reading records directly from PhysioNet
- Signal visualization with customizable plots
- Integration with NumPy and Pandas for data analysis
- Support for various signal formats and compression methods

---

## Citing

If you use the WFDB Python package in your research, please cite the software publication available on [PhysioNet](https://physionet.org/content/wfdb-python/).
