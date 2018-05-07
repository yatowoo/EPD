# Quanlity control and batch testing for STAR-EPD Readout Module

## Abstract

Event Plane, centrality, and trigger Detector(EPD) is a plastic scintillation detector
designedtobeinstalledonRHIC-STAR.SiPMs are used to collect photons produced by scintillators,
while FEE boards and RX boards are used to amplify and recieve signals from SiPMs. We care about
their performances before installing, e.g., UI curve, noise frequency spectrum, signal characters.
Thus, we setup a batch test system, which is made up of pulse generator, LED, digitizer, etc.

---

## Introduction

Relativistic Heavy Ion Collider(RHIC), locates at Brookhaven National Lab(BNL), is determined
to collide heavy ions. The Solenoidal Tracker at RHIC(STAR) tracks particles produced by RHIC.

### STAR BESII

### EPD

---

## System Design & Setup

* Test Items & Test Methods

First, all device’s mechanical integrity should be ensured and SiPMs’
thickness should be measured, i.e., we should first check whether there exists any obvious damage
and than measure thickness of SiPM by microscope.

Second, UI curve of a SiPM can help us judge its basic electric properties, e.g., dark current
and break down(BD) voltage. Under good dark conditions, we change bias voltage on SiPMs from
50V to 65V, with 0.5V step size. This range covers all what we are interested in. We can control
FEE board and acquire U/I information through computer.

Third, electronic noise can reflect electronic performances. Rib or strange peaks shouldn’t
appear in noise frequency spectrum. Thus, we set bias voltage on SiPM at 46.5V, which is below
its BD voltage, and output RX board signal into oscilloscope or digitizer to collect waveforms, and
finally get frequency spectrum.

Last, several characters of SiPM’s signal should be tested. Shape of signal should be normal,
and pedestal should be changed when adjusting DAC. In addition, we need check spectrum of signal
charge integral in order to judge the quality of single photon signal’s resolution. We first set bias
voltage below BD voltage(46.5V) to check pedestal. And then, set bias voltage at OP voltage(60V)
to check integral spectrum, meanwhile, illuminate SiPMs with light from a LED, which is driven by wavefrom generator. Output all signal into oscilloscope/digitizer, which is triggered in the same
frequency as LED. After collecting enough waveforms and a little further processing, we get integral spectrum.

* System Chart

System chart is as shown in figure 1.

* Instrument Selection

It’s easy to choose LED, whose luminous wavelength range should cover peak of scintillators’ luminescence spectrum, i.e., 475nm. However, choosing oscilloscope or
digitizer is a tough decision. Oscilloscope can help to get more accurate result, but only have 4
input channels. While digitizer have 16 channels but has less precision. Besides, digitizer should
be calibrated before using.

---

## SiPM Characterization

### UI Curve

Typical UI curve of SiPM is like figure 2, which shows UI curves of all 16 SiPMs in one FEE board.

Due to low accuracy of current monitor, current measurement is less precise than 0.01µA.
Thus, we can only get dark current quite roughly. Anyway, we can see a sudden increase when bias
voltage increase. We choose the point, whose current is closest to 0.1 µA as break point, for the
purpose of simplifing. At last, we can get distribution of "break down voltage".

### Noise

Comparison between oscilloscope and digitizer is showed in figure 3

It seems that results from oscilloscope are more accuracy, while results from digitizer only have
resolution of 1 MHz. Strangely, there still exist several ribs in oscilloscope noise spectrum when
no signal input at all. We believe it’s blame to oscilloscope itself. Considering of tight schedule,
we deside to use digitizer to setup batch test system.

### Signal

Signal examples are as shown in figure 4.

### Pedestal

As is shown in figure 4b, pedestals of signals from digitizer are sloping. With
further disicussion, we find that different pedestals have different slope. However, differece of
slopes are too small to influnce pedestal value. Thus, it’s a reasonable convention that average value
of pedestal is its measurement result.

From figure 5 we can see adjusting range of pedestal.

### Charge Intergral of Signal

We collect more than 5000 signals from oscilloscope/digitizer
and then integrate time and amplitude. Finally, we get its spectrum like figure 6.

There’s a little trick when analysing waveforms from digitizer. Assuming the signal interval
that contains whole SiPM signals activated by photons from LED is 550ns to 650ns. We choose
430ns and 530ns as our first reference interval, and 670ns to 770ns as second reference interval.
Average of this two reference intervals can be regard as pedestal value of signal interval’s midpoint.
Minusing the average value when integrating can totally get rid of influnce of pedestal slope, and
increase resolution of photon spectrum.

Furthermore, we need to abandon waveforms which contain signal in reference intervals. It’s
easy to do that if we compare the slope, which is calculated by two average value of two intervals,
with the distribution of slope. If the calculated slope is far away from mean value of pedestal
distribution, this waveform should be dump.

---

## Batch Test

### Workflow

### Control panel

### Data processing & result

### Database

---

## Summary

---

## Acknowlegment

---

## Reference
