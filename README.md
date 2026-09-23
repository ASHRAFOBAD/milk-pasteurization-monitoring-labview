# Thermocouple-Based Milk Pasteurization Monitoring System (NI myRIO & LabVIEW)

An end-to-end electronic instrumentation and virtual telemetry system designed for laboratory-scale milk pasteurization monitoring across the critical 60 °C to 75 °C thermal band. The platform interfaces a Type-K thermocouple through an analog signal conditioning circuit into an NI myRIO data acquisition (DAQ) device, providing real-time data processing, process stability calculation, and automated stage classification in LabVIEW.

---

### System Architecture

The physical measurement pipeline converts low-level thermoelectric microvolt signals into an amplified 0–5 V analog signal compatible with the NI myRIO ADC:

```text
+-----------------------+     Thermoelectric     +-----------------------------------------+
|  Type-K Thermocouple  | ---------------------> |       Analog Signal Conditioning        |
| (Chromel-Alumel Probe)|     2.436 - 3.059 mV   | - Stage 1: TL081 Diff Amp (Gain = 100)  |
+-----------------------+                        | - Stage 2: TL081 Non-Inv (Gain = 80)    |
                                                 | - Ref Offset: Voltage Divider (2.436 mV)|
                                                 +--------------------+--------------------+
                                                                      |
                                                                      v 0 - 5 V Linear Output
+-----------------------+     USB / Shared Mem   +--------------------+--------------------+
|  LabVIEW Front Panel  | <--------------------- |              NI myRIO                   |
| - HMI Waveform Chart  |     Real-Time G-Code   | - Built-in Analog-to-Digital Converter  |
| - State Classification|                        | - Hardware LED Status Annunciation      |
| - Stability & Quality |                        +-----------------------------------------+
+-----------------------+
