---
title: Enabling Cisco SE-Connect With the GUI
date: 2016-11-08 10:00:00
categories: [Wi-Fi, Infrastructure]
tags: [Wi-Fi, Cisco]     # TAG names should always be lowercase
image:
  path: assets/enabling-se-connect/Chanalyzer.png
---

There are plenty of guides out there that explain how to put a Cisco AP in SE-Connect mode via SSH, but what about the GUI?

# Pre-Requisites

For this guide, you'll need to first convert your Cisco AP to autonomous mode. To convert my AP, I used an [excellent guide by Rasika Nayanajith](https://mrncciew.com/2013/12/13/ap-conversion-using-mode-button/){:target="_blank"}.

# Guide

1. Log into the Cisco AP. If you haven't changed the password, the username is `cisco`, and the password is `Cisco`.

2. On the `**Home** page, click the **2.4 GHz** link next to **Radio0-802.11N**.

![](assets/enabling-se-connect/step-2.png)

3. Click on the **Settings** tab.

![](assets/enabling-se-connect/step-3.png)

4. At **Enable Radio**, select **Enable**. At **Role** in **Radio Network**, select **Spectrum**, and click **Apply** at the bottom.

![](assets/enabling-se-connect/step-4a.png)

![](assets/enabling-se-connect/step-4b.png)

5. Go back to the Home screen, and do the same process for the 5 GHz radio (enabling it, setting the role to Spectrum, and applying the settings).

7. Click on the **Spectrum Information** link.

8. After a moment, the **NSI Key** field will populate.

![](assets/enabling-se-connect/step-8.png)

That's it! Now you can grab the NSI key and IP address, and take it to either Chanalyzer + Cisco CleanAir or Cisco Spectrum Expert to perform remote spectrum analysis.

![](assets/enabling-se-connect/Chanalyzer.png)
