---
layout: default
title: Overview
parent: WFDB Format Specification
nav_order: 1
---

# Overview of the WFDB File Structure

{: .important }
> A WFDB (Waveform Database) record typically consists of **multiple related files** that together define a physiologic signal recording and its annotations.

The key file types are:

| File Type | Typical Extension | Description |
|:----------|:------------------|:------------|
| Header file | `.hea` | Describes the overall recording and each signal’s properties. |
| Signal file | `.dat`, `.bin`, `.16`, etc. | Contains the actual waveform sample data. |
| Annotation file (optional) | `.atr`, `.ann`, etc. | Contains event markers, labels, or comments aligned to the signal timeline. |

---

## How the Files Work Together

- The **header file** (`.hea`) is the starting point. It specifies the record’s name, sampling frequency, signal files, gain settings, and other metadata.
- The **signal files** store the waveform data, often in a binary-encoded format. Each signal may have its own file, or multiple signals may share a file.
- **Annotation files** are optional and provide time-stamped events, such as heartbeat labels, rhythm changes, or clinical comments.

These files **share a common record name**, and are usually kept together in the same directory.

For example, for a record named `100`, the typical files might be:

```
100.hea    (header file)
100.dat    (signal data file)
100.atr    (annotation file)
```

---

## Multi-Segment Records

Some WFDB records are **multi-segment**. In this case, the main header file references a sequence of segments, each with its own associated files.  

Multi-segment records allow for efficient storage of long recordings and variable signal structures.

---

## Summary

To fully read or analyze a WFDB recording, you need:

- The **header file** (`.hea`),
- The associated **signal files** (e.g., `.dat`),
- And optionally, any **annotation files** (e.g., `.atr`).

Each file provides a piece of the complete information needed to reconstruct the signals and their clinical context.
