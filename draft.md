# Quality control and batch testing for STAR-EPD Readout Module

## Abstract

Event Plane, centrality, and trigger Detector(EPD) is a plastic scintillation detector designed to be installed on RHIC-STAR.
SiPM arrays are used to collect photons produced by scintillators, while FEE boards and RX boards are used to amplify and receive signals from SiPMs.
The mass production of 60 SiPM readout modules has been procured.
A detailed quality control procedure has been carried out on each SiPM for the determination of operating voltage, noise and signal performance.
The batch test system is made up of a pulse generator, LED, digitizer, PC with control panel and power supply, which is described in this paper as well as part of the result.

---

## Introduction

Relativistic Heavy Ion Collider (RHIC), locates at Brookhaven National Lab (BNL), is determined to collide heavy ions.
The Solenoidal Tracker at RHIC (STAR) tracks particles produced by RHIC.

### STAR BESII

The Beam Energy Scan program (BES) at RHIC has shown hints of a critical point and first-order phase transition at the BES energies.
Key measurements for locating the critical point and determining the first order phase transition are limited by poor event plane resolution, limited statistics, and a TPC-only centrality determination.
Therefore, phase II of the BES program was proposed to take data with upgraded detectors and increased statistics for the further investigation.
A new event plane and collision centrality detector is planned to replace the existing detector, the BBC, with higher granularity and acceptance. [1][2]

### EPD

The design of the EPD consists of two scintillator discs at z= ± 3.75m from the center of STAR, covering 2.2 <η< 5.1, the same as the BBC.
The detector will be read out by silicon photomultipliers - an inexpensive and magnetic field insensitive replacement for the traditional photo-multiplication tube.
A prototype of the detector, consisting of a single sector was integrated into STAR during the 2016 run.
The optimized segmentation, size, and shape of the final design were decided in order to maximize event plane resolution, centrality estimation and flow harmonic measurements. [1][2]

In the proposal of EPD [3], USTC was assigned to undertake the production and quality assurance of readout module, which is comprised of SiPM board, front-end electronics (FEE) board, and receiver(RX) board.
We developed a dedicated system for the quality control and batch test, including test platform, GUI controller, and web database.

---

## System Design & Setup

* Test Items & Test Methods

Before any performance test executed, all device’s mechanical integrity should be ensured.
For instance, we should check whether there exists any obvious damage or foreign matters and then measure the distance between SiPM surface and PCB by microscope.

Second, UI curve of a SiPM can help us judge its basic electric properties, e.g., dark current and break down(BD) voltage.
Under good dark conditions, we change bias voltage on SiPMs from 50V to 65V, with 0.5V step size.
This interval covers all the points that we are interested in.
We can control FEE board and acquire U/I information through USB protocol.

Third, since electronic noise significantly impacts electronic performance, rib or strange peaks should not appear in noise frequency spectrum.
Thus, we set bias voltage on SiPM at 46.5V, which is below its breakdown voltage, output the signal from RX board to oscilloscope or digitizer to record waveforms, and finally get frequency spectrum by fast Fourier transformation.

Last, several characteristic signals of SiPM was measured.
The shape of waveforms should be normal, and pedestal should be changed when adjusting DAC.
In addition, we need check spectrum of signal charge integral in order to judge the quality of single photon signal’s resolution.
We first set bias voltage below breakdown voltage (46.5V) to obtain pedestal. And then, set bias voltage at operating voltage (60V)
for integral signal spectrum, meanwhile, illuminate SiPMs with light from a LED, which is driven by a waveform generator.
Output all signal into oscilloscope/digitizer, which is triggered in the same frequency as LED.
After collecting enough waveforms and offline data processing, we get hold of the integral spectrum of SiPM signal.

* System Chart

System chart is as shown in Figure [].

* Instrument Selection

It’s easy to choose LED, whose luminous wavelength range should cover peak of scintillators’ luminescence spectrum, i.e., 475nm.
However, choosing oscilloscope or digitizer is a tough decision.
The oscilloscope can be helpful to acquire more accurate results but only have 4 input channels.
While there are 16 channels in digitizer front panel but with less precision.
Besides, calibration is necessary for digitizer before it has been employed.

---

## SiPM Characterization

### UI Curve

Typical UI curve of SiPM is like figure 2, which shows UI curves of all 16 SiPMs in one FEE board.

Due to low accuracy of an onboard current monitor, the precision of current measurement is less than 0.01µA.
Thus, we can only get dark current quite roughly. Despite all this, an inflection point is observed clearly when bias voltage increase.
This curve is fitted with a third order polynomial for the purpose of simplification.
At last, the point that is nearest to 0.10 $\mu A$ is appointed as operating voltage.

### Noise

Figure [] demonstrate the comparison between oscilloscope and digitizer.

It seems that results from oscilloscope are more accuracy, while results from digitizer only have a resolution of 1 MHz.
There still exist several ribs in oscilloscope noise spectrum when
no signal input.
We believe it’s blame to oscilloscope itself. Considering our tight schedule, we decided to use the digitizer to set up the batch test system.

### Signal

Different patterns of signal samples are as shown in Figure [].

### Pedestal

As is illustrated in Figure [], pedestals of signals from digitizer are sloping.
With intensive study, this slope changes slightly when the pedestal was manipulated.
While the variance of slopes is too small to influence pedestal value, it’s a reasonable convention that average value of pedestal is its measurement result.

From Figure [] we can see the range of pedestal for adjusting.

### Charge Intergral of Signal

WMore than 5000 signals were collected from oscilloscope/digitizer and then integrate time and amplitude. Subsequently, its spectrum was produced like Figure [].

There’s a little trick when processing waveforms from the digitizer. 
Assuming the signal interval that contains whole SiPM signals activated by photons from LED is 550ns to 650ns.
430ns to 530ns was selected as our first reference interval and 670ns to 770ns as second reference interval.
Average of this two reference intervals can be regarded as pedestal value of signal interval’s midpoint.
Minusing the average value when integrating can totally get rid of the influence of pedestal slope, and improving the resolution of photon spectrum.

Furthermore, waveforms that contain the signal in reference intervals should be rejected.
It’s easy to do that if we compare the slope, which is calculated by two average value of two intervals, with the distribution of slope.
If a calculated slope is far away from the mean value of pedestal
distribution, this waveform should be dumped as well.

---

## Batch Test

The new Event Plane Detector will consist of 24 azimuthal segments, spanning an angle of $15\degree$ which we give the label "sector".
A super-sector will contain two sectors.
There are 16 segments in $\eta$, with the innermost tile spanning the entire supersector, and the other tiles dividing it in two for better $\phi$ resolution.
This results in a total of 744 channels for the two EPD disks.[3]
Furthermore, there are extra 4 super sectors to be constructed as a failsafe.
So we prepared 60 individual readout modules with 16 SiPM channel each.
In view of a large number of measurement to perform, a custom semi-automatized system controlled by computer has been developed.

### Workflow

At the beginning of batch testing, we labeled all the components with serial number and created tracking sheets to record following operations and results.
Then the SiPM boards were sent to a clean room for visual inspection.
Under a microscope, SiPM with dust or defect can be found easily.
The Kapton was employed to protect SiPM from dust and scratch, while defective ones should be picked up and rejected for further steps.
Next, the SiPM board would be installed with an FEE board and fiber connector in our dark box.
After power restarted, we could control this system and perform remaining test items in a controller panel.
All of the data was collected and saved as ROOT file automatically, while a simple check procedure performed at the end of running.
The configuration of each item is listed in the table below.

Item|Parameter|Unit|Description|
-|-|-|-|
UI Curve|53, 63, 0.5|V, Volt|[Start, Stop, Step]|
Pedestal|-127, 0, 127|-|DAC input digits|
Noise||V, Volt||
Signal||V, Volt||

Once all the tests are successfully performed, these components will be separated from the system, packed with antistatic bags and stored.

### Control panel

The controller is a C++ script program, which is based on ROOT framework [].
It was developed to encapsulate drivers of FEE board and digitizer and provide a graphic interface for efficient operations.
As shown in Fig[], there are five parts in the panel, which contains user interface of test information, hardware settings, and action buttons.
Before main procedure starts, operators should check the connection of FEE and digitizer with a click of "Check" button.
Then if they work well, you will get the serial number of FEE board and type of digitizer.
Later click "UI Curve" button to run a voltage scan for SiPMs and record their current.
At last, "START" a sequence waveform sampling and wait for data processing.

### Data processing & result

The result of 60 modules displays a good consistency of qualities.
As a key parameter, we focused attention on the distribution of operating voltage and compared it with the distribution of breakdown voltage measured by the manufacturer (Fig. []).
Figure [] presents the signal histogram of all SiPM in one plot, in which we can point out at least 3 peaks for most channels.

### Database

In order to organize data in a manner which allow us and our collaborators to store, query, sort and manipulate in various ways, a simple database, which is called DetectorDB or detdb, was developed and launched on our website.

DetectorDB provides a web viewer to show records and test results of our detectors.
It is comprised of the main table (bootstrap-table), an image viewer (baguetteBox.js) and a ROOT file browser (jsroot).
For more details about the implementation, you can have a look at the corresponding repository on GitHub.

---

## Summary

In this paper, we introduced a dedicated system and comprehensive procedure for qualtiy control of STAR-EPD readout modules.
Our result shows the system was satisfied with the requirements and preforming very well during batch testing.
About 48 modules have been installed and running in STAR.
This system included the web database will also play an important role in the successive collaboration and further R&D programs.

---

## Acknowledgment

---

## Reference

1. Justin Ewigleben, and STAR Collaboration. "An Improved Event Plane Detector for the STAR Experiment" [Link](http://meetings.aps.org/link/BAPS.2017.APR.M13.4)

2. Yang, Chi, and STAR Collaboration. "The STAR beam energy scan phase II physics and upgrades." Nuclear Physics A 967 (2017): 800-803.

3. STAR Collaboration. "An Event Plane Detector for STAR" [Construction Proposal](https://drupal.star.bnl.gov/STAR/files/Construction_Proposal_0.pdf), May 2016