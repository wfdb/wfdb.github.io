---
layout: default
title: MATLAB Toolbox
parent: WFDB Software
nav_order: 2
---

# WFDB MATLAB Toolbox

The **WFDB Toolbox for MATLAB and Octave** provides access to PhysioNet's waveform and annotation databases from within MATLAB or Octave environments.  
It wraps functions from the WFDB C library and command-line tools, providing MATLAB-friendly interfaces for loading, processing, and visualizing physiologic signals.

{: .warning }
> This toolbox is no longer actively maintained.  It remains available for legacy use but is not being updated with new features or database compatibility improvements.

---

## Installation

You can download the WFDB Toolbox for MATLAB from PhysioNet:

- [WFDB Toolbox for MATLAB and Octave v0.10.0](https://physionet.org/content/wfdb-matlab/0.10.0/)

Installation steps:

1. Download and unzip the toolbox.
2. Add the toolbox folder to your MATLAB or Octave path:

```matlab
addpath(genpath('path_to_unzipped_folder'));
savepath;
```

Dependencies:

- Java (for system calls and web access)
- WFDB Software Package (C library) installed locally (optional but recommended for full functionality)

---

## Repository and Contributions

- **Documentation and Download**: [WFDB Toolbox for MATLAB on PhysioNet](https://physionet.org/content/wfdb-matlab/0.10.0/)
- **Original Contributors**: Ikaro Silva, Benjamin Moody, George Moody

Since active development has ceased, contributions are not currently being accepted.

---

## Basic Usage Example

Reading a waveform record:

```matlab
[signal, fs, tm] = rdsamp('mitdb/100', [], 10);
plot(tm, signal);
xlabel('Time (s)');
ylabel('Amplitude');
title('Record 100 from MIT-BIH Arrhythmia Database');
```

Reading annotations:

```matlab
[ann, anntype, subtype, chan, num, comments] = rdann('mitdb/100', 'atr');
disp([ann, anntype]);
```

---

## Features

- Load signal data (`rdsamp`)
- Load annotation data (`rdann`)
- Fetch PhysioNet data automatically via HTTP
- Basic processing tools (e.g., QRS detection, heart rate variability analysis)

The toolbox provides a simple, integrated way to work with PhysioNet databases in MATLAB but is dependent on system-level WFDB utilities for full functionality.

---

## Citing

If you use the WFDB Toolbox for MATLAB in your research, please cite:

{: .citation }
> Silva, I., Moody, B., & Moody, G. (2021). Waveform Database Software Package (WFDB) for MATLAB and Octave (version 0.10.0). PhysioNet. [https://doi.org/10.13026/6zcz-e163](https://doi.org/10.13026/6zcz-e163)
