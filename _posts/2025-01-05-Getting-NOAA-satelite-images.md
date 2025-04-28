---
layout: post
title: Tuning into Space - Capturing NOAA Weather Satellites with WebSDR
categories: [Miscellaneous, Jekyll]
---


The goal of this project is to capture weather satellite images. In the first part, I will outline the initial requirements for receiving satellite images and demonstrate how to do it using WebSDRs. In the second part, I will build an antenna and attempt to capture the signals myself.

## NOAA Satellite Signals

NOAA weather satellites transmit images in the 137 MHz band using FM modulation with a bandwidth of 30–40 kHz. The most relevant satellites for Automatic Picture Transmission (APT) are:

- **NOAA-15**: 137.6200 MHz  
- **NOAA-18**: 137.9125 MHz  
- **NOAA-19**: 137.1000 MHz  

These are the only NOAA satellites still transmitting APT signals. Older satellites (e.g., NOAA-12, NOAA-14) have been decommissioned, while newer ones (e.g., NOAA-20) use advanced digital formats like HRPT, which require more complex equipment.

### Finding Satellite Passes  

To successfully receive signals, you need to track satellite passes over your location. You can check real-time satellite orbits here:  
🔗 [N2YO Satellite Tracker](https://www.n2yo.com/satellites/?c=4)  

Additionally, the **HeavensAbove** mobile app provides a visual representation of satellite paths.

## Capturing and Decoding with WebSDR  

To get started without hardware, I found a WebSDR equipped with a V-dipole antenna for weather satellite reception:  

🔗 [WebSDR in Netherlands](http://websdr.camras.nl:8901/)  

This SDR covers the NOAA APT frequencies, allowing me to tune in remotely.

![](/images/noaa/image-9.png)

### Tracking the Pass  
To capture a good signal, I need to calculate when a satellite will pass over the SDR’s location. This can be done with:  

- [N2YO Satellite Pass Calculator](https://www.n2yo.com/satellites/?c=4) – Provides azimuth and elevation data  
- **HeavensAbove** app – Visualizes satellite passes  

### Recording and Decoding  

During a satellite pass, I record the audio signal, which can then be decoded into an image. There are several tools available for this:  

- [NOAA-APT](https://noaa-apt.mbernardi.com.ar/how-it-works.html) – A simple decoder  
- **SatDump** – More advanced offline processing  

![](/images/noaa/image-12.png)

#### Converting the WAV File to an Image  

Using **NOAA-APT**, I process the recorded audio file and obtain black-and-white images like this:  

![](/images/noaa/image-1212.png)

If the satellite’s signal is weak, the image may be incomplete. To enhance it, I use:  `noaa-apt -m -F -s`.

This command adds **false color** and **map overlays**, making the image clearer and easier to interpret.  

![](/images/noaa/image-1213.png) 

## Next Steps  

In the next part, I will build my own antenna and attempt to capture NOAA signals directly.