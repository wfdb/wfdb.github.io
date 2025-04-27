---
layout: default
title: Glossary
nav_order: 5
---

# Glossary

This glossary defines key terms used throughout the WFDB specification, software, and associated documentation.

---

### WFDB (Waveform Database)
A general term that refers to a set of open standards, file formats, and software for representing, storing, and analyzing physiologic waveform and annotation data. Originally developed at MIT by George B. Moody in 1989.

### WFDB Specification
The formal definition of the WFDB file formats: headers (`.hea`), signal files (`.dat`), and annotation files (`.atr`, `.ann`, etc.).  

The specification describes how physiologic data and event annotations should be encoded, independent of any software implementation.

### WFDB Software
The collection of software tools, libraries, and applications that read, write, visualize, and process WFDB-formatted data.  

This includes the original WFDB C library, Python packages, MATLAB toolboxes, and command-line utilities.

---

### AC-coupled Signal

A signal (e.g., ECG) for which only variations in level are significant. Baseline (DC offset) is removed prior to digitization.

### ADC (Analog-to-Digital Converter)

A device that converts continuous analog signals into discrete digital samples.

### ADC Resolution

The number of significant bits per sample produced by the ADC, determining the granularity of the digital representation.

### ADC Zero
The digital output value corresponding to a 0-volt input. For unipolar ADCs, this is typically 1024.

### ADU (Analog-to-Digital Unit)
The native unit of a digital sample before conversion to physical units. Values are in integers corresponding to ADC output.

### AHA Format
A legacy annotation format originating from the American Heart Association (AHA) database standard.  
It uses fixed-length annotation records (16 bytes each).

### Annotation
A marker associated with a specific sample, identifying events like heartbeats, arrhythmias, or comments.

### Annotation File
A binary file (e.g., `.atr`, `.ann`) containing annotations linked to a signal record.

### Base Counter Value
A value corresponding to the counter (e.g., tape counter) at sample 0, used for mapping counter ticks to time.

### Base Date
The date at which the record begins, specified in `DD/MM/YYYY` format.

### Base Time
The time of day when the recording starts, in `HH:MM:SS` format (24-hour clock).

### Channel
A single data stream within a record, such as an ECG lead or arterial blood pressure waveform. Typically a record will include multiple channels.

### Counter Frequency
The number of counter ticks per second, used for records originally stored on analog media.

### Digital Signal
A signal after analog-to-digital conversion, consisting of discrete numerical samples.

### Frame
A set of simultaneous samples from all signals at a single time point.

### Gain
A scaling factor to convert from ADUs (digital units) to physical measurement units like millivolts or mmHg.

### Header File
A text file (`.hea`) that defines the metadata for a WFDB record, including signal specifications.

### Multi-segment Record
A record composed of multiple segments, allowing variable signal types or gaps in recording.

### Physical Signal
The reconstructed analog signal after scaling the digital samples by gain and baseline correction.

### Record
A named collection of files (header, signal, annotation) representing a single physiologic recording.

### Record Line
The first non-comment line of a header file, summarizing basic properties like number of signals and sampling rate.

### Sampling Frequency (fs)
The number of samples acquired per second, specified in Hertz (Hz).

### Signal File
A binary file (e.g., `.dat`) containing waveform samples for one or more channels.

### Signal Specification Line
A line in the header file that describes a specific signal’s properties, including format, gain, units, and file name.

### Units
The physical measurement units (e.g., millivolts, mmHg) associated with a signal, specified in the header file.

---

This glossary is intended to serve as a quick reference when working with WFDB-formatted data.  
For full technical specifications, please refer to the [WFDB Programmer's Guide](https://physionet.org/physiotools/wpg/) and [WFDB Applications Guide](https://physionet.org/physiotools/wag/).

