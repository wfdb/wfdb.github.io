---
layout: default
title: Annotation Files
parent: WFDB Format Specification
nav_order: 4
---

# WFDB Annotation Files

Annotation files contain **time-stamped event markers** aligned to the signal data.  
These files provide critical context, such as heartbeat labels, arrhythmias, rhythm changes, and comments.

WFDB supports two annotation file formats:

- **MIT format** (compact, preferred)
- **AHA format** (legacy, mainly for interoperability)

---

## MIT Annotation Format

The MIT format is the **standard** for WFDB annotations.  
It is binary, compact (averaging slightly over two bytes per annotation), and extensible.

Each annotation in the MIT format consists of:

- A **time difference** (`I`) from the previous annotation, measured in sample intervals.
- An **annotation type code** (`A`), describing the event.

The first byte of each annotation pair is the **least significant byte**.  
The six most significant bits across the pair encode the annotation type, and the remaining ten bits encode the time difference.

---

### Special Cases in MIT Format

If the annotation type (`A`) has a special value, the annotation may also contain:

| Code | Meaning | Notes |
|:-----|:--------|:------|
| `SKIP (59)` | Large skip | A 4-byte absolute time follows. |
| `NUM (60)` | Set `num` field | Applies to current and following annotations. |
| `SUB (61)` | Set `subtyp` field | Applies to current annotation only. |
| `CHN (62)` | Set `chan` field | Applies to current and following annotations. |
| `AUX (63)` | Auxiliary data | I bytes of extra text follow (e.g., rhythm labels). |
| `A = 0, I = 0` | End of file | No more annotations. |

Auxiliary fields such as `subtyp`, `chan`, `num`, and `aux` provide additional metadata for selected annotations.

---

## AHA Annotation Format

The AHA format is a **fixed-length** (16 bytes per annotation) legacy format.

- Originally designed for 9-track tape transfer.
- Used mainly for interoperability, **not recommended** for modern datasets.

Each 16-byte AHA annotation includes:

- An **ASCII annotation code** (AHA-specific).
- A **timestamp** (in sample intervals or milliseconds).
- Optional fields for rhythm descriptions or comments.

WFDB software can automatically distinguish between MIT and AHA formats when reading annotation files.

---

## Summary

| Format | Use Case |
|:-------|:---------|
| MIT format | Default for WFDB records; compact, extensible. |
| AHA format | Legacy support; rarely used except for archival data. |

Annotations are essential for interpreting WFDB signals, supporting applications like heartbeat detection, arrhythmia analysis, and rhythm classification.
