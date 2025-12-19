---
layout: default
title: Header Files
parent: WFDB Format Specification
nav_order: 2
---

# WFDB Header Files

Each WFDB record includes one or more **header files** (`.hea`) that specify the associated signal files and their attributes. Header files are plain ASCII text and are critical for interpreting the associated signal and annotation files.

---

## Structure of a Header File

A header file contains:

- A **record line** (first non-comment line), specifying metadata about the entire record.
- One or more **signal specification lines**, detailing each signal.
- Optionally, **comment lines** (beginning with `#`).

Each line must be under 255 characters, and fields are separated by spaces or tabs (except where otherwise noted).

Detailed documentation on header files can be found at: [https://physionet.org/physiotools/wag/header-5.htm](https://physionet.org/physiotools/wag/header-5.htm)

---

## Record Line

The first non-comment line is the **record line**, which provides metadata about the overall record. It includes:

| Field | Description |
|:------|:-----------|
| Record name | Identifier for the record (letters, digits, underscores only). |
| Number of segments (optional) | If present, appended as `/n`. Indicates a multi-segment record. |
| Number of signals | Number of signals described in the header. |
| Sampling frequency (optional) | Samples per second per signal. Defaults to 250 if omitted. |
| Counter frequency (optional) | Secondary clock frequency, separated from sampling frequency by a `/`. |
| Base counter value (optional) | Offset value for counter, enclosed in parentheses. |
| Number of samples (optional) | Total samples per signal when `samps_per_frame`=1; total frames otherwise. |
| Base time (optional) | Start time of the recording (`HH:MM:SS`). |
| Base date (optional) | Start date (`DD/MM/YYYY`). |

### Examples

#### Basic header (uniform sampling frequency)(record 100 from the [MIT-BIH database](https://www.physionet.org/content/mitdb)):

```text
100 2 360 650000
```
- `100`: Record name (must match the filename prefix).
- `2`: Number of signals in the record.
- `360`: Sampling frequency in Hz.
- `650000`: Total samples for each signal.

#### Multi-frequency header (unique sampling rates per channel):

```text
12345 3 62.5 625 12:00:00 30/01/1989
```
- `12345`: Record name (must match the filename prefix).
- `3`: Number of signals in the record.
- `62.5`: Sampling frequency in Hz.
- `625`: Total frames for each signal. When `samps_per_frame` =  1 (default), this will be the total samples.
- `12:00:00`: The time (`base_time`).
- `30/01/1989`: The date (`base_date`).

---

## Signal Specification Lines

Each signal has its own line immediately following the record line (for single-segment records). Fields are:

| Field | Description |
|:------|:------------|
| File name | Name of the file containing signal data. |
| Format | Integer code describing how signal data is encoded (e.g., `16` for 16-bit integers). |
| Samples per frame (optional) | Number of samples per frame (if not 1), separated by `x`. |
| Skew (optional) | Signal-specific time offset (number of samples), separated by `:`. |
| Byte offset (optional) | Byte position to start reading the signal file, separated by `+`. |
| ADC gain (optional) | Scaling factor to convert integers to physical units (e.g., millivolts). |
| Baseline (optional) | Integer value representing 0 physical units. |
| Units (optional) | Label for signal units (e.g., `mV`). |
| ADC resolution (optional) | Bits per sample (defaults to format’s resolution if omitted). |
| ADC zero (optional) | Sample value corresponding to physical zero. |
| Initial value (optional) | First sample value (used for checksums). |
| Checksum (optional) | Sum of sample values (modulo 65536) for verification. |
| Block size (optional) | Number of samples per block (for formats supporting block I/O). |
| Description (optional) | Free-text description of the signal (e.g., lead name `ECG Lead II`). |

### Examples

#### Basic header (uniform sampling frequency)(record 100 from the [MIT-BIH database](https://www.physionet.org/content/mitdb)):
```text
100.dat 212 200 11 1024 995 -22131 0 MLII
100.dat 212 200 11 1024 1011 20052 0 V5
```
- `100.dat`: Filename of the signal file.
- `212`: Storage format (12-bit two's complement).
- `200`: ADC gain (i.e. number of digital values per physical unit). 
- `11`: ADC resolution (bits).
- `1024`: ADC zero value.
- `995`, `1011`: Initial value.
- `-22131`, `20052`: Checksum (sum of all signal samples modulo 2^16).
- `0`: Block size.
- `MLII`, `V5`: Signal labels (e.g., lead names).

#### Multi-frequency header (unique sampling rates per channel):
```text
12345.dat 16x4 200/μV 12 0 0 2178 0 ECG
12345.dat 16x2 16/mmHg 12 0 0 3497 0 ICP
12345.dat 16x1 2500/Ohm 12 0 0 1366 0 RESP
```
- `12345.dat`: Filename of the signal file.
- `16`: Storage format (16-bit integers).
- `x4`,`x2`,`x1`:  4, 2, and 1 samples per frame, respectively. This indicates that the ECG signal has `157 * 4 = 628` samples while the ICP signal has 314 samples and the RESP signal has 157 samples. 
- `200/μV`, `16/mmHg`, `2500/Ohm`: ADC gain (i.e., number of digital values per physical unit).
- `12`: ADC resolution (bits).
- `0`: ADC zero value.
- `0`: Initial value.
- `2178 `, `3497`, `1366`: Checksum (sum of all signal samples modulo 2^16).
- `0`: Block size.
- `ECG`, `ICP`, `RESP`: Signal labels (e.g., lead names).

---

## Comments and Info Strings

- Any line beginning with `#` is a comment.
- Comments after the last signal line are preserved and may provide additional metadata ("info strings").
- Earlier comments are ignored by programs reading the header.

---

## Notes

- A header file may describe signals stored in multiple files or multiple signals in a single file.
- Fields like sampling frequency, counter frequency, and base time/date improve time-aligned analysis but are optional.
- Storage format options and details can be found at: [https://physionet.org/physiotools/wag/signal-5.htm](https://physionet.org/physiotools/wag/signal-5.htm)
- Multi-segment records use a slightly different structure (described separately).
