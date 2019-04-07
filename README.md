# Quality control and batch testing for STAR-EPD Front-end Readout Module

## Abstract

Event Plane, centrality, and trigger Detector(EPD) is a plastic scintillation detector designed to be installed on RHIC-STAR.
SiPM arrays are used to collect photons produced by scintillators, while FEE boards and RX boards are used to amplify and receive signals from SiPMs.
The mass production of 60 SiPM readout modules has been procured.
A detailed quality control procedure has been carried out on each SiPM for the determination of operating voltage, noise and signal performance.
The batch test system is made up of a pulse generator, LED, digitizer, PC with control panel and power supply, which is described in this paper as well as part of the result.

---

## TODO list

> REWRITE in more professional style.

1. Section/paragraph for light source.
2. UI curve (log axis) errors and fitting for Vop.
3. Re-produce all plots with larger font size.
4. Oscilliscope vs digitizer.
5. Offiline correction for digitizer.
6. All results from batch testing.
7. More details on design of web database.

---

## Outline

### Introduction

* Physics of RHIC-STAR BESII program.
* EPD proposed objectives, requirements, design and project timeline.
* USTC task and importance. / Works in this paper.

### Front-end Readout Module

* EPD DAQ system within STAR experiment.
* SiPM/FEE/RX functions, features and performance requirements.
* Chanllenges during production, quality control, and transportation.

### Test platform

* Research on characterization of SiPM and other parts, which includes UI curve, Vbr/Vop, gain, temperatur compensation, noise spectrum, and signal performance.
* Test items and criteria.
* System design and development.

### Batch testing

* Work flow management and optimization. Quality control during testing, like operation rules and solution for specific problems.
* Results, web database and some issues.
* EPD performance in Run 2018.

### Summary

* Lookback the works and results, then emphasize the importance in EPD program.

## Figures

1. STAR-EPD and super-module geometry
2. DAQ system and electronic components (SiPM+connector/FEE/RX)