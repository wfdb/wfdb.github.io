---
layout: default
title: C Implementation
parent: WFDB Software
nav_order: 2
---

# WFDB C Software Package

The **WFDB Software Package in C** is the original, highly portable implementation of the WFDB standards for reading, writing, and analyzing physiological waveform data.

It was initially developed by **George B. Moody** in the late 1980s at MIT and continues to be actively maintained.

The C package provides both:

- A **core library** (`libwfdb`) for reading and writing waveform and annotation data.
- A **suite of command-line applications** for signal processing, visualization, and automated analysis.

---

## Installation

### Requirements

- C compiler (e.g., `gcc`)
- Recommended libraries:
  - [`libcurl`](https://curl.se/libcurl/) (for reading remote files directly from PhysioNet)
  - [`libFLAC`](https://xiph.org/flac/) (for reading/writing compressed signal files)

### Install via package managers (Linux)

You can install precompiled binaries via `apt` (Debian/Ubuntu systems):

```bash
sudo apt-get install wfdb-tools
```

Or, to compile from source:

### Build from Source

```bash
git clone https://github.com/MIT-LCP/wfdb-app-toolbox.git
cd wfdb-app-toolbox
./configure
make
sudo make install
```

This will build the `libwfdb` library and install over 70 command-line tools.

---

## Repository and Contributions

- **Source code**: [MIT-LCP/wfdb-app-toolbox](https://github.com/MIT-LCP/wfdb-app-toolbox)
- **Documentation**:
  - [WFDB Programmer's Guide](https://physionet.org/physiotools/wpg/)
  - [WFDB Applications Guide](https://physionet.org/physiotools/wag/)

Contributions are welcome! Please refer to the GitHub repository for issue tracking and pull requests.

---

## Basic Usage Example

After installing, you can read a waveform record using one of the command-line tools, such as `rdsamp`:

```bash
rdsamp -r mitdb/100 -p
```

This command downloads and prints samples from record `100` of the MIT-BIH Arrhythmia Database hosted on PhysioNet.

Or you can compile a C program that uses the WFDB library:

```c
#include <wfdb/wfdb.h>

int main(void) {
    WFDB_Sample v;
    WFDB_Anninfo ai;
    WFDB_Annotation annot;
    ai.name = "atr";
    ai.stat = WFDB_READ;

    if (annopen("mitdb/100", &ai, 1) < 0)
        return 1;

    while (getann(0, &annot) == 0) {
        printf("Annotation at sample %ld: type %d\n", annot.time, annot.anntyp);
    }
    return 0;
}
```

---

## Features

- Read and write WFDB-formatted signals and annotations
- Support for compressed (`.dat`, `.dat.gz`, `.dat.flac`) and remote records
- Extensive command-line tools (e.g., `rdsamp`, `rdann`, `xform`, `snip`, `psd`)
- ANSI/ISO C compliance for cross-platform portability
- C, C++, and Fortran compatibility

---

## Citing

If you use the WFDB Software Package in your research, please cite:

{: .citation }
> Moody, G., Pollard, T., & Moody, B. (2022). WFDB Software Package (version 10.7.0). PhysioNet. [https://doi.org/10.13026/gjvw-1m31](https://doi.org/10.13026/gjvw-1m31)

