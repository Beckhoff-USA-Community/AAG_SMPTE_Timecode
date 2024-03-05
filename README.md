# About This Repository

This repository is an example of how to implement both a SMPTE Timecode Receiver and SMPTE Timecode Sender. SMPTE (Society of Motion Picture and Television Engineers) Timecode is use throughout the entertainment industry for synchronizing video, audio, lights, motion, and much more. With TwinCAT PLC and the power of XFC Oversampling terminals, we can both send and receive the SMPTE Timecode signal.

### Receiver

For the receiver project, the cycle time requirement is 1ms and the terminal oversampling factor is set to 100. There is an easy to use Function Block for processing the signals and managing the receiver.





### Sender

For the SMPTE Sender, there are two Function Blocks required. The first is a FB_SMPTE_TimeController block that is used as a time source for the SMPTE Sender, and can be controlled via simple Play, Stop, Pause, and Reset commands. The second block is FB_SMPTE_Sender that is responsible for taking the time stamp provided by FB_SMPTE_TimeController  and processing it as a SMPTE signal for analog output. 

A requirement of the SMPTE Sender code is a PLC cycle time of 20ms, and an oversampling rate of 80. Currently, the only framerate supported is **25 FPS** due to the maximum filter speed of oversampling terminals.

First, configure the Time Controller:
<p align="left">
  <img src="https://github.com/Beckhoff-USA-Community/AAG_SMPTE_Timecode/blob/main/Images/SMPTE_Sender_TimeControllerVar.PNG">
</p>  

The time controller can operate based on three different sources. NT source uses the Windows NT Time of the controller, DC uses the DC clock value, and External allows you to supply your own external ULINT signal from the TwinCAT External Time Provider (NTP, or DC):

<p align="left">
<img src="https://github.com/Beckhoff-USA-Community/AAG_SMPTE_Timecode/blob/main/Images/TimeMode.PNG">
<img src="https://github.com/Beckhoff-USA-Community/AAG_SMPTE_Timecode/blob/main/Images/ExternalTime.PNG">
</p>  

If using the external time provider, you need to assign it before use; like in the example below:

<p align="left">
<img src="https://github.com/Beckhoff-USA-Community/AAG_SMPTE_Timecode/blob/main/Images/SMPTE_Sender_TimeControllerPOU.PNG">
</p>  

Second, you need to configure the SMPTE Sender and attach the time controller:

<p align="left">
<img src="https://github.com/Beckhoff-USA-Community/AAG_SMPTE_Timecode/blob/main/Images/SMPTE_Sender_Var.PNG">
<img src="https://github.com/Beckhoff-USA-Community/AAG_SMPTE_Timecode/blob/main/Images/SMPTE_Sender_POU.PNG">
</p> 




This sample is created by [Beckhoff Automation LLC.](https://www.beckhoff.com/en-us/), and is provided as-is under the Zero-Clause BSD license.

# How to get support

Should you have any questions regarding the provided sample code, please contact your local Beckhoff support team. Contact information can be found on the official Beckhoff website at https://www.beckhoff.com/en-us/support/.

# Further Information

Further Information on SMPTE Timecode with TwinCAT can be found in the [Application Note.](https://www.beckhoff.com/media/downloads/application-reports-downloads/2013/dk9222-0213-0063-2.pdf)

## Requirements

The following components must be installed to run sample code:

- [TE1000 TwinCAT 3 Engineering](https://www.beckhoff.com/en-en/products/automation/twincat/te1xxx-twincat-3-engineering/te1000.html) version 3.1.4024.0 or higher
- EL3702 for SMPTE Timecode Receiving
- EL4732 for SMPTE Timecode Sending
