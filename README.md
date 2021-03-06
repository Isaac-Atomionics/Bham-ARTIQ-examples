# Bham-ARTIQ-examples
This repository, along with the associated wiki, was produced in August 2019 by Camron Nourshargh and Rustin Nourshargh while working in the Atom Interferometry Group at Birmingham University. It was produced as a summer project, the main goals of which were to gain a better understanding of how to use ARTIQ, and to produce example code and documentation to introduce beginners to the Sinara Device.


For further details, see [wiki](https://github.com/cnourshargh/Bham-ARTIQ-examples/wiki)

## Examples
#### LED_OnOffPulse.py
Code demonstrating basic use of an LED on the Kasli Board
- Switch LED on
- Switch LED off
- Pulse LED

#### LED_Parallel.py
Code demonstrating "with parallel" and "with sequential" statements by pulsing LEDs on Kasli Board
- Two parallel threads
- One of the parallel threads has sequential code within it

#### TTLout_OnOffPulse.py
Code demonstrating basic use of a TTL output channel 
- Switch TTL output on
- Switch TTL output off
- Pulse TTL output

#### TTLin_SingleRead.py
Code demonstrating basic reading of a TTL input channel
- Reads TTL input (1 or 0)
- Prints TTL input

#### TTLin_Trigger.py
Code demonstrating basic use of TTL input channel as Trigger
- Scans TTL input for rising edges for fixed interval
- Gives TTL output if rising edge is detected in time interval
  - Timing is deterministic between input and output

#### Sampler_SingleSample.py
Code demonstrating basic use of sampler to read voltage on up to 8 channels
- Initialises and sets gains on all sampler channels
- Creates list for sample data
- Saves samples to list
- Prints list

#### Zotino_SingleWrite.py
Code demonstrating basic use of Zotino to output voltage
- Writes voltage to DAC
- Loads voltage to output channel

#### Urukul_SingleOutput.py
Code demonstrating basic use of Urukul to output fixed frequency and amplitude waveform
- Sets frequency, amplitude, and channel attenuation as variables
- Switches channel on
- Writes  amplitude and frequency to urukul
- Switches channel off

#### Urukul_GUI_Frequency_Input.py
Code demostrating basic use of management system for taking inputs from user, by allowing user to input frequency
- Takes frequency input (in MHz) in build and saves it as an attribute
- Sets amplitude and channel attenuation as variables
- Switches channel on
- Writes  amplitude and frequency to urukul
- Switches channel off

#### Urukul_GUI_AmpAttFreqInput.py
Code demonstrating how to take multiple inputs from the user in a single experiment
- User inputs:
  - Frequency (in MHz)
  - Amplitude (as amplitude scale factor, so between 0 and 1)
  - Attenuation (in dB, between 0 and 31.5)
  - Pulse duration (in seconds)
- Sets above as attributes
- Writes attenuation to channel
- Switches Channel on
- Writes amplitude and frequency to urukul
- Waits specified duration
- Switches channel off

#### Zotino_RampOutput.py
Code demonstrating how to output a ramp function on a Zotino channel. 
This code produces a ramp between -10V and 10V in steps of 0.2V with a frequency of 1.28kHz.
- Defines list of voltages (in machine units) for ramp
- Loops the following until manually stopped (closing bash terminal or deleting experiment from queue in management system)
  - Loops the following for all voltages in voltage list
    - Writes voltage to DAC
    - Loads voltage to output channel

#### Sampler_MultipleSamples.py
Code demonstrating how to take multiple samples from the sampler in rapid succession. This code was sampling at 10.1kS/s when tested. 
This was the fastest samling rate achievable without getting underflow errors.
- Initialises sampler
- Generates dataset to be written to
- Sets gains on all channels
- Creates list for sample data
- Loops the following 2000 times 
  - Saves samples (in machine units) to list
  - Adds 0th element of list to dataset

From management system, dataset can be plotted with following applet
- ${artiq_applet}plot_xy samples

#### Urukul_RAM_Amplitude.py
Code demonstrating use of RAM on Urukul. We had hoped to be able to use RAM for frequency scans and it appeared that this was not possible so we only have code demonstrating an amplitude scan. The doccumentation for using RAM mode was limitted which is why the comments are not as clear as on some other code
- Produces list of amplitudes to be output
- Initialises CPLD and Urukul Channel
- Sets RAM Profile
- Writes to the CFR(control function register)
- Sets channel frequency and attenuation
- Switches channel on
- Loops following until manually broken
  - In Parallel:
    - Pulses TTL channel
    - Starts ramping up through list
  - In Parallel:
    - Pulses TTL channel
    - Starts ramping down through list
