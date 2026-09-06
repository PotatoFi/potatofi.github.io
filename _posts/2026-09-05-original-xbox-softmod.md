---
title: Softmodding an Original Xbox
date: 2026-09-05 15:41:50
categories: [Technology, Vintage]
tags: [Retro Gaming]
image:
  path: assets/original-xbox-softmod/orginal-xbox-softmod-preview.jpeg
---

Since leaving my two Original Xboxes in storage and moving to Finland, I got the itch to play some Xbox games, and picked up a console on Tori (basically Craigslist) for 40€ (about $45).

![](assets/original-xbox-softmod/original-xbox.jpeg)

I planned to softmod it so I could:

* Play games online with Insignia
* Run backups of my NTSC games, because PAL games usually can't run in 480p and stuff
* Swap the aging 8 GB hard drive for fresh storage hardware that isn't liable to fail at any time

Back in 2011 or so, when you could pick up an Xbox at a garage sale for $10, I softmodded a couple of them primarily so they could run XBMC. The tools were all over the place, and the documentation never seemed complete or centralized. 15 years later in 2026, it seems like the tools are better, but the knowledge is still scattered all over the internet.

![](assets/original-xbox-softmod/xbmc-in-2011.jpeg)

I didn't manage to take careful notes while softmodding my Xbox, as it took some trial and error. As a result, this doesn't read like a step-by-step guide, but is instead a collection of notes that I hope will help you softmod your Xbox. I also have some random notes along the way about things like thumbstick replacemenents.

![](assets/original-xbox-softmod/xbox-controllers.jpeg)

## First

Unless you have an Xbox version 1.6, get the clock capacitor out. If it hasn't destroyed your motherboard, it will. Get it out _right now_.

## Softmodding

Previously, it was nescessary to get a copy of Splinter Cell and use a save game exploit to launch the softmod. Today, this can be done with ENDGAME, which skips the game and exploits directly from the **Memory** menu in the stock dashboard. As a result, the only hardware you need is:

1. An Xbox to USB adapter. I used [this one from AliExpress](https://www.aliexpress.com/item/1005003440265548.html), but you can get these in a variety of places.
2. A compatible flash drive, which usually means that it's older, or small capacity, of both. I used [this one from AliExpress](https://www.aliexpress.com/item/1005008120319561.html) and it worked great, but you can check out a [compatibility list](https://consolemods.org/wiki/Xbox:USB_Device_Compatibility_List) to see if something rattling around in your desk drawer will work.

### Rocky5's Softmodding Tool

[Rocky5's Softmodding Tool](https://github.com/rocky5/xbox-softmodding-tool) seems to be the most popular one right now, and [this YouTube short](https://www.youtube.com/watch?v=8ZFpDoALtIk) shows the process with minimal fluff.

### Applications

Applications seem to always be called "default.xbe", but if you place each application in `F:\Applicatons\` inside it's own subfolder, then dashboards will pick up the application, naming it with the folder name.

For example, the Insignia Setup Assistant itself is a "default.xbe", so `F:\Applications\Insignia Setup\default.xbe` will appear as `Insignia Setup` in the *Applications* group in your dashboards.

_Note: In UIX-Lite, you'll need to go to **Settings** > **UIX Settings** > **General Settings** > **Rescan Partitions** to have it re-scan for Applications, Games, and Dashboards._

#### Insignia Setup Assistant

As the name suggests, this is used to set up Insignia.

[Insignia Setup Assistant](https://github.com/insignia-live/setup-assistant-release/releases/latest)

#### Dashloader Customizer

Changes which dashboard starts by default. I used this to change the default dashboard from UnleashX back to the stock Microsoft dashboard, after it was patched with UIX-Lite.

[Dashloader Customizer](https://github.com/Rocky5/Xbox-Softmodding-Tool/raw/master/Extras%20Disc/Softmod/applications/Dashloader%20Customizer.zip)

_Note: In the application, trying pressing **Left** on the d-pad if you can't figure out what to do._ 

#### Chimp

This tool clones the contents of the original hard drive to a new storage device, all on your Xbox without having to use a computer. The idea is to start up Chimp, unplug the DVD drive, and connect your new storage device in place of it. Chimp copies everything over, expands the partitions to fill the empty space, and locks the drive with your original hard drive key. 

Maybe I messed up, but Chimp only expanded my F drive to 127 GB, so I had to use another tool (XBPartitioner) to finish expanding the partition.

[Chimp](https://github.com/Rocky5/Chimp261812)

#### XBPartitioner

Rocky5's mod lists "XBPartitioner" as an app you can run from UnleashX, but it's not actually there; it's actually just a message saying that you don't need it. Well, Rocky5, as much as I appreciate you, I _did_ in fact need it to expand my F partition after using Chimp.

[XBPartitioner](https://consolemods.org/wiki/File:XBpartitioner-1_3.7z)

_Note: You'll need to use the correct block size, depending on how large your hard drive is. XBPartitioner does a good job of handling this automatically, but if you need to understand exactly why the block size matter, [check out this Reddit post](https://www.reddit.com/r/originalxbox/comments/6jnvdc/help_with_xbpartitioner_13/)._

#### Video Select 2

Since I'm in Finland, my Xbox is PAL, but I would much prefer to use NTSC video modes. This application writes a small change to the BIOS, changing the Xbox from PAL to NTSC video modes. After applying the change, the Xbox now has the exact same video options in the dashboard as my NTSC Xboxes back home. I've been using it with RetroTINK 2X-Classic and component cables at 480i, ending up with 480p on my European LG OLED TV.

[Video Select 2](https://digiex.net/threads/enigmahs-video-select-2-xbox-region-switcher-ntsc-pal.13817/)

## Dashboards

After running the exploit, running Rocky5's Softmodding Tool, you'll get dropped into UnleashX. The hard drive will have C, D, E, and F partitions.

### UIX-Lite

Rocky5's softmod installs UnleashX, which is very full-featured, but I prefer the look and feel of the stock Microsoft dashboard. I was thrilled to find out about UIX-Lite, which patches the stock Microsoft dashboard so it can launch games, applications, and other dashboards.

![](assets/original-xbox-softmod/uix-launcher.jpeg)

With the UIX-Lite patch, I'm able to use the patched Microsoft dashboard for day-to-day operation, and UnleashX for maintenance.

[UIX-Lite Github](https://github.com/OfficialTeamUIX/UIX-Lite)

### Switching to UIX-Lite

Follow the *How-to (Automagically)* instructions to restore the Microsoft Dash 5960, and then patch it. You'll end up with these two dashboards:

* Patched Microsoft Dash 5960: `C:\xboxdash.xbe - Patched 5960`
* UnleashX: `C:\Dashboard\default.xbe`, with files such as config.xml, items.xml, and a Skins folder.

### Making UIX-Lite the Default

1. Copy everything in `C:\Dashboard\` to `E:\Dashboards\UnleashX`
2. Use File Explorer in UnleashX to boot the patched Microsoft Dash 5960.
3. Make sure Microsoft Dash 5960 starts, and that you can run UnleashX from `E:\Dashboards\UnleashX` from it.
4. Use Dashloader Customizer to make the Patched Microsoft Dash 5960 boot by default, it's at `C:\xboxdash.xbe`
5. Test to make sure that Patched Microsoft Dash 5960 boots up by default.
6. Delete the old copy of UnleashX that's in `C:\Dashboard\` to clean it up.

Now, UIX-Lite (e.g. the Patched Microsoft Dash 5960) will boot by default, but you can go to **Launcher** > **Dashboards** > **UnleashX** to launch UnleashX if you need it.

![](assets/original-xbox-softmod/uix-dashboard.jpeg)

## Hard Drive Upgrade

I elected to upgrade my stock 8 GB hard drive to a 256 GB SSD, because:

1. The original hard drive is now 25 years old and is likely to fail any day now.
2. My collection of NTSC Xbox games is in storage in the US, so I'd like to run backups directly from storage.

### Hardware

1. A SATA hard drive or SSD. I went for a 256 GB Kingston SSD, as I can probably put 50 games on it (but I won't, it will be more like 15)
2. An IDE to SATA adapter, and some way to power two IDE devices at the same time (like a Y cable, if needed).
3. An 80-wire IDE cable, as the stock 40-wire cable doesn't let the IDE bus go fast enough for things to work. Remember that both of them have 40 _pins_, but the 80-wire cable has a dedicated ground wire for each signal wire, reducing noise and unlocking higher speeds.

#### IDE to SATA Adapter

##### AliExpress Adapter

Initially, I used [this inexpensive no-name from AliExpress](https://www.aliexpress.com/item/1005005922096341.html), which had reviews saying that it worked for the Original Xbox. I bought it along with a [Y cable](https://www.aliexpress.com/item/1005006026259742.html) to simultaneously power the old hard drive and new SSD. Unfortunately, the IDE controller seemed to struggle to enumerate the adapter, as the console hung on the "Xbox" logo for a long time on each boot. After awhile the console will either Error 07 (hard drive discovery timed out), or the "Microsoft" logo will appear and continue to boot.

![](assets/original-xbox-softmod/aliexpress-ide-to-sata-adapter.jpeg)

##### StarTech Adapter

I then ordered the famous red StarTech adapter, which is known to work (and is also known to work with [Todd Gill's 2.5" hard drive mounting bracket](https://www.printables.com/model/351702-xbox-25-inch-to-35-inch-adapter)). It also includes a pass-through power cable, so you don't need a Y adapter to power two drives.

![](assets/original-xbox-softmod/ide-to-sata-cable-front.jpeg)

At first, it wasn't plug-and-play. I got an instant "flubber" and Microsoft logo on boot, but then an intermittent black screen. But then, I noticed that pressing the Eject button always started my dashboard. The fix was to [use NKPatcher to install a specific Kernel Font](https://www.reddit.com/r/originalxbox/comments/1s2mnlz/softmod_black_screen_after_splash_screen/). As it turns out, the exploit is triggered with a literal text font, with different fonts available for different Xbox revisions.

To switch from a generic kernel font to a specific one:

1. Launch NKPatcher Settings.
2. Go to **Kernel Fonts** > **Advanced Features** > **Kernel Font Options** > **Install Kernel Font**.

#### 80-wire IDE Cable

This one has proven to be a real pain, as [the 37 cm one I could get on AliExpress](https://www.aliexpress.com/item/1005006919154090.html) is just plain too short.

[This folding guide](https://youtu.be/spHmkAfJ83c?si=D6BBwmYYv8QK2TUv) is extremely helpful, though. Combined with the StarTech adapter and Todd's mounting bracket, it ended up being barely long enough.

![](assets/original-xbox-softmod/ide-to-sata-cable-back.jpeg)

## Miscellaneous

### Replacement Thumbsticks

It turns out that Xbox 360 thumbsticks make drop-in replacement for the Original Xbox S controller (and The Duke as well). I [grabbed a package from AliExpress](https://www.aliexpress.com/item/1005006562962554.html) and while they aren't *quite* as soft as I remember Xbox 360 thumbsticks being, they are much better than the worn-out originals on my Xbox S controllers.

I also found [this Xbox Series X/S thumbstick adapter on Printables](https://www.printables.com/model/139382-thumbstick-adaptor-for-original-xbox-duke-s-contro), but I couldn't figure out how it is supposed to work with my Xbox S controllers or Series X/S thumbsticks from AliExpress.

![](assets/original-xbox-softmod/xbox-controller-closeup.jpeg)

When disasembling your controllers:

1. Look for white circles on the controller PCBs. Keep the wires out of those circles, as the controller plastics touch the PCB at those locations to keep things solid. It's easy to accidentally pinch wires there.
2. When putting screws back in, turn them backwards with a bit of pressure until you hear and feel the screw "click". Then, turn the screw the right way. This will align the threads.
3. Tighten the screw.

### Converting ISO or XISO

If your backups are in ISO or XISO format, you'll need to unpackage them and copy them to the Xbox with FTP. The easiest method I've found is with with [xdvdfs-web](https://github.com/antangelo/xdvdfs/tree/main/xdvdfs-web), which runs out of a browser.

1. Download and put it in a folder.
2. `cd` to the folder, and run `python3 -m http.server`
3. Navigate to [http://127.0.0.1:8000/](http://127.0.0.1:8000/).
4. Use the **Unpack** option.
