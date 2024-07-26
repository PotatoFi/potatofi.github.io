---
title: Cellular Failover with Android and a Raspberry Pi
date: 2018-12-27 10:00:00
categories: [Technology, Linux]
tags: [Wi-Fi, Android, Raspberry Pi]
image:
  path: assets/cellular-failover/cellular-failover.jpg
---

The great CenturyLink outage of late 2018 is under way. At the time of this writing, we're 16.5 hours in, and I'm tired of using my Android phone as a Wi-Fi hotspot. I want my network back up.

Fortunately, I have some tools to work with. I have a spare Android phone complete with an unlimited data plan (T-mobile ran a 3rd line for free promo a couple years ago) and a spare Raspberry Pi (seriously who doesn't have several of those kicking around). The idea here is that we can use the Raspberry Pi to turn that USB cell phone tether into ethernet, so our router can treat it basically like a modem.

In my setup, I have a `WAN2` port on my Ubiquiti UniFi Secure Gateway. If WAN1 goes down, the USG will automatically flop over to WAN2.

# Guide

> Infosec is a huge blind spot of mine. I'm nowhere close to competent with Linux. Exposing a Pi to the internet is scary to me. Proceed with caution.
{: .prompt-danger }

## Set up Rasbian

1. Download [Raspbian Lite](https://www.raspberrypi.org/downloads/raspbian/).
2. Write it to an SD card with a tool like [Etcher](https://www.balena.io/etcher/).
3. Once it's done, eject and reattach the SD card so your OS will mount `/boot`.
4. [Grab this zip](https://drive.google.com/uc?export=download&id=1RfVpMc1d7-6Ud_UB6Z3AV31xXhqXCdeG), and unzip the two files.
4. From the .zip, drop ssh into `/boot`, which wil enable SSH on the Raspberry Pi.
5. Optionally, you can also drop `wpa_supplicant.conf` into `/boot`, and edit the file with your WPA2 SSID and passphrase (you can skip this step if you are just gunna configure it with Ethernet).

## Configure the Bridge

1. Plug everything in.
2. Enable USB tethering on your Android phone.
3. SSH into your Raspberry Pi.
4. Change the password:
```bash
passwd
```
5. If you want to check and ensure that the Raspberry Pi sees your phone, run:
```bash
dmesg | tail
```
6. If you want to be sure that `usb0` shows up, run:
```bash
ifconfig
```
7. Install `brctl` (hilariously, this should work because you have WAN via `usb0`):
```bash
sudo apt-get install bridge-utils
```
8. Create the bridge:
```bash
sudo brctl addbr bridge0
```
9. Add `usb0` and `eth0` to the bridge:
```bash
sudo brctl addif bridge0 eth0
sudo brctl addif bridge0 usb0
```
10. Enable the bridge:
```bash
sudo brctl stp bridge0 on
```
11. Configure the `WAN2` interface on your router or firewall to DHCP. You may also want to set DHCP to use Google or Cloudflare.
