---
layout: default
title: Signal Data Files
parent: WFDB Format Specification
nav_order: 3
---

# WFDB Signal Data Files

WFDB signal files contain the raw waveform data for one or more signals.  Each file is typically in a binary format optimized for efficient storage and processing.

Signal files are referenced in the corresponding **header file** (`.hea`), which specifies the format used for each signal.

---

## Overview of Formats

WFDB supports multiple signal encoding formats. These differ in how sample amplitudes are stored, and whether data is compressed or packed.

The key formats include:

| Format | Description |
|:-------|:------------|
| 8 | First differences stored as signed 8-bit integers. |
| 16 | 16-bit two’s complement integers (little-endian). |
| 24 | 24-bit two’s complement integers (little-endian). |
| 32 | 32-bit two’s complement integers (little-endian). |
| 61 | 16-bit two’s complement integers (big-endian). |
| 80 | 8-bit offset binary (unsigned 8-bit, subtract 128 to recover). |
| 160 | 16-bit offset binary (unsigned 16-bit, subtract 32,768 to recover). |
| 212 | Packed 12-bit two’s complement samples (compact format, common in PhysioBank). |
| 310 | Packed 10-bit two’s complement samples (legacy format). |
| 311 | Alternative packed 10-bit samples (different packing from 310). |
| 508, 516, 524 | Signals compressed with FLAC (8, 16, or 24 bits per sample). |

---

## Commonly Used Formats

- **Format 16** is a simple, widely supported format: each sample is stored as a 16-bit signed integer, little-endian.
- **Format 212** is highly space-efficient: two 12-bit samples are packed into three bytes. Many PhysioNet records use this format.
- **Formats 508/516/524** use **FLAC compression**, providing lossless compression for signals (with some restrictions).

---

## Multiplexed Signals

When multiple signals are stored in the same file (multiplexed format), samples are interleaved:

```
sample 1 of signal 0
sample 1 of signal 1
sample 2 of signal 0
sample 2 of signal 1
...
```

This multiplexing order ensures synchronized playback and analysis.

---

## Important Notes

- **Byte Order:**  
  - Formats 16, 24, 32 store data **little-endian** (least significant byte first).
  - Format 61 stores data **big-endian** (most significant byte first).

- **Scaling:**  
  The raw integer values are scaled to physical units (e.g., millivolts) using the gain and baseline values provided in the header file.

- **Compression:**  
  FLAC-compressed formats (508, 516, 524) require specialized handling.  
  They impose limits on the number of signals (maximum 8) and require synchronized sampling rates.

---

## Summary

To correctly interpret a WFDB signal file:

- Read the corresponding **header file** to determine the format.
- Parse the signal data according to the specified encoding.
- Apply scaling factors to convert sample values to physical units.
