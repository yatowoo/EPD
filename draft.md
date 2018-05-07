# Quality control and batch testing for STAR-EPD Readout Module

## Abstract

Event Plane, centrality, and trigger Detector(EPD) is a plastic scintillation detector
designed to be installed on RHIC-STAR. SiPMs are used to collect photons produced by scintillators,
while FEE boards and RX boards are used to amplify and receive signals from SiPMs. We care about
their performances before installing, e.g., UI curve, noise frequency spectrum, signal characters.
Thus, we setup a batch test system, which is made up of pulse generator, LED, digitizer, etc.

---

## Introduction

Relativistic Heavy Ion Collider(RHIC), locates at Brookhaven National Lab(BNL), is determined
to collide heavy ions. The Solenoidal Tracker at RHIC(STAR) tracks particles produced by RHIC.

### STAR BESII

The BES program at RHIC has shown hints of a critical point and first order phase transition at the BES energies. Key measurements for locating the critical point and determining the first order phase transition are limited by poor event plane resolution, limited statistics and a TPC-only centrality determination. Therefore, phase II of the BES program was proposed to take data with upgraded detectors and increased statistics for the further investigation. A new event plane and collision centrality detector is planned to replace the existing detector, the BBC, with higher granularity and acceptance. [1]

### EPD

The design of the EPD consists of two scintillator discs at z= ± 3.75m from the center of STAR, covering 2.2 <η< 5.1, the same as the BBC. The detector will be read out by silicon photomultipliers - an inexpensive and magnetic field insensitive replacement for the traditional phototube. A prototype of the detector, consisting of a single sector was integrated into STAR during the 2016 run, which will be shown. The optimized segmentation, size and shape of the final design was decided in order to maximize event plane resolution, , centrality estimation and flow harmonic measurements. We will discuss the plans to install one quarter of a disc into STAR for the 2017 run. [1]

In the proposal of EPD, USTC was assigned to undertake the production and quality assurance of readout module, which is comprised of SiPM board, front-end electronic (FEE) board and receiver(RX) board. We developed a completely system for batch test, including test platform, gui controller and web database.

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

The new Event Plane Detector will consist of 24 azimuthal segments, spanning an angle of $15\degree$ which we give the label "sector". A super sector will contain two sectors. There are 16 segments in $\eta$, with the innermost tile spanning the entire super-sector, and the other tiles dividing it in two for better $\phi$ resolution. This is resulted in a total of 744 channels for the two EPD disks.[3] Furthermore, there is an extra 4 super sectors to be constructed as a failsafe. So we prepared 60 individual readout modules with 16 SiPM channel each.

### Workflow

As for such a number of channels, an important step before testing is to establish a proper and strict workflow, which would ensure a consistent testing conditions and increase our cooperation efficiency.

In the beginning of batch testing, we labelled all the components with series number and created tracking sheets to record following operations and results. Then the SiPM boards were sent to a clean room for visual inspection. Under a microscope, SiPM with dust or defect can be found easily. The kapton was employed to protect SiPM from dust and scratch, while defective ones should be picked up and rejected for further steps. Next, the SiPM board would be installed with a FEE borad and fiber connector in our dark box. After power restarted, we could control this system and perform remaining test items in a controller panel. All of data was collected and saved as ROOT file automatically, while a simple check procedure performed at the end of running. Configuration of each item is listed in the table below.

Item|Parameter|Unit|Description|
-|-|-|-|
UI Curve||V, Volt|[Start, Stop, Step]|
Pedestal|-127, 0, 127|-|DAC input digits|
Noise||V, Volt||
Signal||V, Volt||

Once all the tests are successfully performed, these components will be seperated from the system, packed with antistatic bags and stored.

### Control panel

The controller is a GUI script, which is based on ROOT framework. It was developed to encapsulate drivers of FEE board and digitizer and provide graphic interface for efficient operations.

### Data processing & result

### Database

DetectorDB provides a web viewer to show records and test results of our detectors. It is comprised of a main table (bootstrap-table), an image viewer (baguetteBox.js) and a ROOT file browser (jsroot). For more details about the implementation, you can have a look at the corresponding repository on GitHub.

---

## Summary

---

## Acknowlegment

---

## Reference

1. Justin Ewigleben, and STAR Collaboration. "An Improved Event Plane Detector for the STAR Experiment" [Link](http://meetings.aps.org/link/BAPS.2017.APR.M13.4)

2. Yang, Chi, and STAR Collaboration. "The STAR beam energy scan phase II physics and upgrades." Nuclear Physics A 967 (2017): 800-803.

3. STAR Collaboration. "An Event Plane Detector for STAR" [Construction Proposal](https://drupal.star.bnl.gov/STAR/files/Construction_Proposal_0.pdf), May 2016