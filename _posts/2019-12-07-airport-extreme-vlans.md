---
title: Does the Apple Airport Extreme use VLANs?
date: 2019-12-07 10:00:00
categories: [Wi-Fi, Infrastructure]
tags: [Wi-Fi, Apple]     # TAG names should always be lowercase
image:
  path: assets/airport-extreme-vlans/airport-extremes.jpg
---

The short answer: yes!

It's not secret that [I'm a huge fan of the Apple AirPort Extreme](https://twitter.com/Potato_Fi/status/1203456043058991104). Whenever friends and family have Wi-Fi problems at home, I get on Craigslist and buy a used Apple AirPort Extreme for them. I love their high-quality 3x3 radios, simplicity, and reliability.

![](assets/airport-extreme-vlans/airport-extremes.jpg)

In a few cases, I've set up more than one at a time. If we're lucky enough to have some Ethernet in the house, I might use two or even three AirPort Extremes to provide coverage everywhere. One as a router, and the other one or two as just "access points". Apple calls this "extending with Ethernet" in the AirPort Utility.

One thing I've always wondered about: how does the AirPort Extreme separate guest network and "internal" network traffic? I figured that it was likely to be VLANs, but without a PCAP, I couldn't be sure.

I picked up a couple of A1354's (that's the 4th-generation, 2009 version with 3 spatial streams) to deploy for my relatives, and took the opportunity to do a quick test. I leveraged my [old 10 mbps ethernet hub](https://twitter.com/Potato_Fi/status/1203528003067596800) (yep, I have one of those) between the AirPort Extremes with my MacBook and a USB ethernet adapter as a PCAP device. Of course, I used Wireshark.

![](assets/airport-extreme-vlans/packet-capture-diagram.png)

I created a unique guest SSID on the second AirPort Extreme to ensure my client would associate to the right one. Next, I started a PCAP in Wireshark on the correct interface, and then I finally ran a throughput test from the client device, just to generate some traffic. After seeing a few TCP frames from the the client fly by, I stopped the PCAP to investigate.

In the packet, we can see the Destination, Source, and Type, which is **802.1Q Virtual LAN**. The ID is **1003**, indicating that this Ethernet frame is tagged for **VLAN 1003**.

![](assets/airport-extreme-vlans/guest.png)

Doing the same PCAP with the client associated on the non-guest side shows **untagged** Ethernet frames.

![](assets/airport-extreme-vlans/non-guest.png)

The conclusion: guest network traffic is tagged VLAN 1003, while "internal" traffic is simply untagged. Whether or not AirPort Extremes always use VLAN 1003 is unknown, but now you know how to look and see in your own setup... if you wanted to do that. Okay, I realize that I am probably literally the only person out there who wanted to do that.

With an old Ethernet hub, a USB ethernet adapter, and Wireshark, I was able to satisfy my curiosity, and learn a little bit more about packet captures on the Ethernet side.
