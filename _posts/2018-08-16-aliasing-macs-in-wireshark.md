---
title: Aliasing MAC Addresses with Wireshark
date: 2018-08-16 10:00:00
categories: [Wi-Fi, Tools]
tags: [Wi-Fi, Wireshark]
image:
  assets/aliasing-wireshark/wireshark-aliases-preview.jpg
---

I love Wireshark, but one thing is for sure: tracking 802.11 conversations with my human brain is difficult. [Coloring rules help](https://github.com/PotatoFi/PotatoFrames), but I find it very difficult to remember which MAC address is which wireless station.

Fortunately, Wireshark has the ability to alias IP and MAC addresses! These are defined in the `ethers` file. You should be able to do nearly the same thing on Windows, but here's how to do it on macOS.

# Aliasing MAC Addresses

1. Open a terminal, and run:
```bash
nano ~/Users/your_username/.config/wireshark/ethers
```
![](assets/aliasing-wireshark/nano.jpg)
2. Define the MAC address and the desired alias in the file. Separate the MAC and alias with any number of spaces. Aliases themselves can't contain spaces.
```
ab:cd:ef:12:34:56 (AP)Aruba205H
12:34:56:ab:cd:ef (Client)Nokia6.1
ab:12:ef:cd:34:56 (Client)MacBookPro
```
![](assets/aliasing-wireshark/editing-in-nano.jpg)
3. Save the file by pressing `Ctrl` + `X`, then `Y` for yes, then `Enter`.
4. Restart Wireshark, and now friendly, readable aliases will appear in place of MAC addresses.
![](assets/aliasing-wireshark/wireshark-with-aliases.jpg)

> When defining names, I like to lead with either (AP) or (Client) so I can immediately tell which side is talking.
{: .prompt-tip }

# Appending the Ethers File

You can quickly add new MAC addresses to your file with **cat**.

> When appending with cat, be very careful to use `>>`. Using just one `>` will overwrite the entire file!
{: .prompt-warning }

1. In the terminal, run this line:
```bash
cat >> /Users/your_username/.config/wireshark/ethers
```
2. Press `Enter`, which will start a new line. Add any new hosts, line by line.
```
ab:cd:ef:12:34:56 (AP)Aruba205H
12:34:56:ab:cd:ef (Client)Nokia6.1
ab:12:ef:cd:34:56 (Client)MacBookPro
```
3. Press `Ctrl` + `D` to write the additions to the file.

# Copying MAC Addresses from Wireshark

It's fast and easy to copy MAC addresses out of Wireshark, and you can paste them into the terminal.

1. Find the transmitter, receiver, source, or destination frame in the **Packet Details** pane, and right-click it.
2. Select **Copy** > **Value** to copy out the MAC.
3. Paste into the terminal with `Command` + `V`.
![](assets/aliasing-wireshark/packet-details.png)
