---
title: Reading Mileage from a 1997 Volvo 850
date: 2018-08-16 10:00:00
categories: [Wi-Fi, Tools]
tags: [Wi-Fi, Wireshark]
image:
  assets/volvo-850-mileage/volvo-850-mileage-preview.jpg
---

I'm a huge fan of Volvo 850's (especially the 850R), but they aren't without a few flaws. One of them is the odometer: the mechanical odometer is driven by a small electric motor in the gauge cluster, and it has a tiny nylon gear that loses a tooth, causing it to stop counting miles.

Fixing it costs a couple of bucks, but it's a pain. The dash has to come out, which takes a couple of hours, and comes with the inherent risk of breaking things. As a result, there are many 850's on the road with inaccurate odometers.

Pre-OBDII Volvo 850's (1993-1995) provide the ability to plug in a fly wire under the hood, press a special button pattern, and then watch an LED blink back the mileage, which is stored digitally in the gauge cluster. Then, you can fix the odometer gear, and roll up the mileage to the correct number in the process.

Sadly, OBDII Volvo 850's (1996-1997) lack the fly wire, button, and LED. Fortunately, [there's a way to read the mileage through the OBDII port](http://jonesrh.info/volvo850/elm327_reads_volvo_850_mileage.html) with an ELM 237 Bluetooth OBDII reader, and an Android phone. This might be possible with iOS or with a terminal emulator in Windows, but I have an Android device, so that's the route I took.

# Reading the Mileage

1. Plug in the ELM 237 ODBII reader, and get it paired to your phone.
2. Get a terminal emulator app. I used [Elm Basic](https://play.google.com/store/apps/details?id=com.drively.elmterminal).
2. Turn the Volvo 850 key to the "on" position.
3. Type in the following commands, one at a time, pressing `Enter` after each one. A couple of commands will reply with a short bus initialization message after a short pause.
```
ATZ
ATL1
ATE1
ATSP 3
ATH1
ATAL
ATKW0
ATTA 13
ATRA 13
ATIIA 51
ATWM 82 51 13 A1
ATSI
ATSH 84 51 13
B90300
```
4. When you're done, the car should reply with `B90300`, followed by a hexidecimal value.
![](assets/volvo-850-mileage/volvo-850-output.png)
5. Use [my calculator](https://docs.google.com/spreadsheets/d/1DvlAkPIAIJQpVLLwoA7Juo6sBYhdpeV95bKz1DFA-qc/edit?usp=sharing) to convert the hexidecimal value to miles or kilometers.

> After all of these years, the history in the calculator (which is a Google Sheet) shows that people have been using it! If you successfully retrieve your mileage, feel free to sign the "Guest Book" section.
{: .prompt-tip }

# Alternate Method

On July 23, 2019 reader "jonesrh" left this comment:

> The following sequence is more general purpose and works for both '96-'97 850 and '97-'98 S70/V70/C70/XC70, *and* it works for ELM327 v1.2 (and above):

```
ATZ
ATL1 # some terminal emulators might need ATL0 instead
ATE1 # some terminal emulators might need ATE0 instead
ATSP 3
ATH1
ATAL
ATKW0 # this is a zero, not a capital "O"
ATSR 13
ATIIA 51
ATWM 82 51 13 A1
ATSH 83 51 13
B903
```

Thanks for the advice, jonesrh!
