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

---

## Record Line

The first non-comment line is the **record line**, which provides metadata about the overall record. It includes:

| Field | Description |
|:------|:------------|
| Record name | Identifier for the record (letters, digits, underscores only). |
| Number of segments (optional) | If present, appended as `/n`. Indicates a multi-segment record. |
| Number of signals | Number of signals described in the header. |
| Sampling frequency (optional) | Samples per second per signal. Defaults to 250 if omitted. |
| Counter frequency (optional) | Secondary clock frequency, separated from sampling frequency by a `/`. |
| Base counter value (optional) | Offset value for counter, enclosed in parentheses. |
| Number of samples (optional) | Total samples per signal. |
| Base time (optional) | Start time of the recording (`HH:MM:SS`). |
| Base date (optional) | Start date (`DD/MM/YYYY`). |

**Example:**
```text
100 2 360 650000 12:00:00 01/01/2000
```

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

**Example:**
```text
100.dat 212 200 11 1024 995 0 MLII
100.dat 212 200 11 1024 995 0 V5
```

---

## Comments and Info Strings

- Any line beginning with `#` is a comment.
- Comments after the last signal line are preserved and may provide additional metadata ("info strings").
- Earlier comments are ignored by programs reading the header.

---

## Notes

- A header file may describe signals stored in multiple files or multiple signals in a single file.
- Fields like sampling frequency, counter frequency, and base time/date improve time-aligned analysis but are optional.
- Multi-segment records use a slightly different structure (described separately).
