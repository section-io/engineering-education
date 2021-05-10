---
layout: engineering-education
status: publish
published:true 
url: /engineering-education/introduction-to-wlan-frequency-bands/
title: Introduction to WLAN Frequency bands
description: This article will explain and distinguish between the two WLAN frequency bands 2.4GHz and 5GHz. It will define the WLAN standards supported by each of the frequency bands and further state the channels within the frequency bands.
author: ruth-mare
date: 2021-05-01T00:00:00-08:00
topics: [Networking]
excerpt_separator: <!--more-->
images:

  - url: /engineering-education/introduction-to-wlan-frequency-bands/hero.jpg
    alt: WLAN frequency bands cover image 
---

WLAN frequency bands are frequency ranges within which radio waves can be implemented to enable wireless communication. These frequency bands are implemented and given the various tasks suited for each and the countries that support each.
<!--more-->
The different WLAN frequency bands are also supported by different and, in some cases, similar WLAN standards.

### Overview
This article will cover:
- [Introduction to WLAN](#introduction-to-wlan)
- [WLAN standards](#wlan-standards)
- [5GHz frequency band](#5ghz-frequency-band)
- [2.4GHz frequency band](#2.4ghz-frequency-band)
- [Overlapping and non-overlapping channels](#overlapping-and-nonoverlapping-channels)

### Introduction to WLAN
- **WLAN**: This refers to the networking mode of connecting two or more devices via a wireless distribution method. They have high-frequency radio waves traveling through channels and an AP (Access Point) to the internet. These transmission channels are distinguished between overlapping and non-overlapping channels

- *A spectrum:* This is radio frequency over which wireless signals travel i.e., frequency distribution.

- *Frequency band:* This is the frequency range of a radio wave. A frequency band comprises several channels.
Higher frequency electromagnetic waves transmit more power and provide stronger direct radiation capability. However, they support a shorter transmission distance due to quick [attenuation](https://www.comptia.org/content/guides/what-is-attenuation) during transmission.

- *A radio wave:* This is also known as a radio, electric wave, or radiofrequency (RF) wave. It can be transmitted and received through an antenna and is normally generated by the alternating current of an oscillation circuit. These are the waves used by WLAN. Radio technology converts sound signals or other signals and transmits them by using radio electromagnetic waves. The frequency of these waves is between 3Hz and about 300GHz. WLAN technology transmits information in space by using radio waves on the 2.4GHz and 5GHz frequency bands.

- *The radio phase:* This is the distance between the point of origin of any given wave and its first zero crossing. The phase is expressed in degrees or radians and every cycle of a wave spans 360 degrees.

- *A channel:* This is a path used for information transmission, that is, each frequency range. Several channels from a frequency band.

- *A radio channel:* This refers to a channel used by radio waves for information transmission in space.

### WLAN standards
- ***IEEE 802.11*** - 1997 (802.11) - This standard supports transmission speed of up to 2Mbps on the 2.4GHz frequency band.
- ***IEEE 802.11a*** - 1999 (802.11a) - This standard supports transmission speed of up to 54Mbps on the 5GHz frequency band.
- ***IEEE 802.11b*** - 1999 (802.11b) - This standard supports transmission speed of up to 11Mbps on the 2.4GHz frequency band. It is also backward compatible.
- ***IEEE 802.11g*** - 2003(IEEE 802.11g) - This standard supports transmission speed of up to 54Mbps on the 2.4GHz frequency band. It covers a distance of 150 feet.
- ***IEEE 802.11n*** - 22009(IEEE 802.11n) - This Standard aims at improving the throughput of the frequency range between 2.4GHz and 5GHz with a transmission speed of up to 600Mbps. It uses several antennae, which in turn increases the data rates.
- ***IEEE 802.11ac wave 1*** - 2013 - This is a popular standard on the 5GHz frequency band that supports transmission speed of up to 3.47Gbps.
- ***IEEE 802.11ac wave 2*** - 2015 - This is a popular standard on the 5GHz frequency band that supports transmission speed of up to 6.9Gbps.
- ***IEEE 802.11ax-2018/19(IEEE 802.11ax)*** - This is a standard on both the 2.4GHz and 5GHz frequency bands that supports transmission speeds of up to 9.6Gbps.

### 5GHz frequency band
The 5GHz frequency band provides richer spectrum resources and contains non-overlapping channels. 5GHz transmission ranges from 5.15GHz to 5.35GHz and 5.725GHz to 5.85GHz. The available channels on the 5GHz band vary depending on countries and regions; for example, there are 13 available non-overlapping channels in china.
The 5GHz frequency band has channels numbered 36 to 165 channels. This frequency band is supported within the following standards: 802.11a, 802.11n, 802.11ax, 802.11 ac wave 1, and 802.11ac wave 2.

### 2.4GHz frequency band
The 2.4GHz frequency band is divided into 14 overlapping channels, each having a frequency bandwidth of 20MHz except in 802.11b, which has a frequency bandwidth of 22MHz. This frequency band ranges from 2.4GHz to 2.4835GHz and neighboring channels overlap. However, commonly, channels 1,5,9 and 13 are non-overlapping channels.
This frequency band is supported within the following standards: 802.11, 802.11b, 802.11g, 802.11n, and 802.11ax.

### Overlapping and non-overlapping channels
Given that radio waves are ubiquitous, random use of spectrum resources will cause endless interference problems. Therefore, in addition to defining the available frequency bands, wireless communication protocols must also divide precisely the frequency ranges. Every frequency range is a channel.

#### Overlapping channels
Overlapping channels are channels that interfere with each other during transmission. The most common interference occurs between adjacent channels such as channels 1 and 2.

#### Non-overlapping channels
Non-overlapping channels, on the other hand, do not interfere with each other. Traditionally, only channels 1, 6, and 11 are non-overlapping channels on the `2.4GHz` frequency band. When incompatibility is not considered, channels 1, 5, 9, and 13 are non-overlapping channels, given that the standard `802.11b` has a bandwidth of 22MHz and has faded out of WLANs.
Distributed among channels, in most countries, the non-overlapping channels on `2.4GHz` follow the respective standards: Channels 1, 6, 11, and 14 for the standard `802.11b` and channels 1, 5, 9, and 13 for the standard `802.11g/n.`
In addition, adjacent channels, such as channels 36 and 40 on the 5GHz frequency band, do not overlap.

In addition, adjacent channels, such as channels 36 and 40 on the `5GHz` frequency band, do not overlap.

### To wrap up
The two WLAN frequency bands support different transmission rates given the standard under which they are implemented. This eventually determines the effectiveness of the two frequency bands in different tasks suited for and the devices implemented by a user.

### Relevant resources
- [WLAN Frequency Bands & Channels](https://www.cablefree.net/wirelesstechnology/wireless-lan/wlan-frequency-bands-channels/#:~:text=WLAN%20Frequency%20Bands%3A%20The%20802.11,into%20a%20multitude%20of%20channels.)
- [Introduction to wireless networking](https://www.section.io/engineering-education/introduction-to-wireless-networking/)
- [Frequency Band and Channel - WLAN Network Planning Guide](https://support.huawei.com/enterprise/en/doc/EDOC1000113315/2d2a4a3c/frequency-band-and-channel)
- [What Is Attenuation](https://www.comptia.org/content/guides/what-is-attenuation)

---
Peer Review Contributions by: [Briana Nzivu](https://www.section.io/engineering-education/authors/briana-nzivu/)