---
title: Interactive Spectrum Chart
date: 2025-02-20 18:25:00
categories: [Wi-Fi, Tools]
tags: [Wi-Fi, Development]
image:
  path: assets/spectrum-viewer/spectrum-chart-preview.png
---

The radio spectrum is a complicated place, with many overlapping technologies and bands that vary depending on the regulatory domain. The radio spectrum is much too complicated to represent on a static chart, so I've always wanted to create something interactive to represent it.

Additionally, I've always loved graphical Wi-Fi scanners and spectrum analysis tools, and figured that an interactive spectrum chart tool could build on the graphical Wi-Fi scanner concept.

_Side note: As far as I know, credit for the first graphical Wi-Fi scanner goes to Ryan Woodings (and probably also Brian Tuttle), who pioneered the idea with inSSIDer 2 at MetaGeek, building on their experience with low-cost spectrum analyzers in the 2.4 GHz band._

So, over the past couple of months, I built something! What I've come up with is a little web application that allows you to pan across the spectrum, zoom in and out, and turn various technologies on and off.

[https://spectrum.potatofi.com](https://spectrum.potatofi.com)

# Fun things to do in it

1. Turn off Bluetooth, and zoom into some 20 MHz channels. Check out those subcarriers! ![](assets/spectrum-viewer/subcarriers.png)
2. Turn on 20 MHz channels, 2.4 GHz overlapping channels, Bluetooth, _and_ Zigbee. Check out how crazy the 2.4 GHz band is! ![](assets/spectrum-viewer/busy-2-GHz.png)
3. Visit the 900 MHz band, turn off the Japanese regulatory domain, and all of the 802.11ah channel widths. As far as I know, this is the very first 802.11ah channel chart out there, and I'm pretty proud of that. 🙂 ![](assets/spectrum-viewer/900-mhz.png)
4. In the 900 MHz band, turn the Japanese regulatory domain back on. Check out how the channel centers are off by 500 KHz! It's so unsatisfying! Sorry that I just ruined your day.
5. Redeem the day by using the **Entire spectrum** shortcut. Check out how much unlicensed room we have for activities!
6. If you have an iPhone, use the **Share** > **Add to Home Screen** button to create a shortcut. I spent some extra time making it feel good on iPhone, complete with a nice icon. ![](assets/spectrum-viewer/iphone.png)

# How to use it

## Panning

Pan across the spectrum by:
* Two-finger swiping left and right on a trackpad
* Left-clicking and dragging with a mouse pointer
* Swiping horizontally on a touchscreen

## Zooming

Zoom in and out of the spectrum by:
* Two-finger scrolling on a trackpad
* Rolling the scroll wheel on a mouse
* Pinching on a touchscreen

### Options

Use the **hamburger menu 🍔** in the upper left to hide and show different technologies, channel widths, and modes. You can also change the height of the signatures/masks with the slider.

### Regulatory Domains

In the **Regulatory Domains 🌍** menu, you can turn a few regulatory domains on and off. IF a channel is included in one or more selected regulatory domains, it will be displayed. **Worldwide** includes all channels that are generally available (or *harmonized*) everywhere. Note that accuracy here is on a best-effort basis; the world is a complicated place. 🙂

### Shortcuts

To jump to a specific part of the band, use the **Shortcuts ⭐** menu.

### Download

Use the **Download 📥** button to take a snapshot of the canvas, and download it.

# What can I use it for?

Feel free to use this chart for:

* A reference, whenever you want to look something up.
* Entertainment.
* Teaching classes about radio technologies such as Wi-Fi, both in a paid and unpaid setting.

Please don't copy my code and redistribute it, or host it anywhere else. I might add a more permissive license in the future, but not right now.

# Challenges

## "Technology Stack"

Pretty early on, I made the descision to build it in vanilla HTML, CSS, and JavaScript. I was hoping to use CSS divs for the channel labels, so I could use CSS for mouseovers, sorting, and other interactivity, the the performance was abysmal. Because of that, I fell back to pure JavaScript. While it's pretty performant (even with my spaghetti code), the downside is that interactivity is much more difficult. But hey, it techically works on my Windows XP netbook!

## 802.11ah Channel Charts

I had to dig around in the 802.11-2020 spec quite a bit to figure out the channel charts. The spec is _just_ cryptic enough that I fed some of it into Claude.ai to make sure we agreed on how the channels work. The result is what I am pretty sure is the very first 802.11ah chart that is openly available on the internet. I'm pretty proud of that.

![](assets/spectrum-viewer/80211ah-900-mhz-channels.png)

# Future Plans

For now, I've worked on this project alone to learn HTML, CSS, and JavaScript, and to have something creative to work on. There has been some interest by my employer ([Hamina Wireless](https://www.hamina.com/)) to put some real development effort behind the idea, and make an official "Hamina Spectrum Chart". Maybe that will happen.

## Planned Features

I might add some of these features, but I am a novice developer. We'll see what I can get done.

* Overhaul the band label system, as there are tons of band labels out there that I'd like to apply but the system isn't flexible enough.
* Figure out how to add technologies without having to write tons of bespoke and repeat code for them. This is mentally blocking me from adding CBRS/private celluar right now, for example.
* Use system resources more efficiently, e.g. don't constantly redraw the screen if the user isn't doing anything.
* Add more technologies, such as cellular bands (I have a pretty extensive list from Keith at Wireless LAN Pros).
* Show subcarriers for 40, 80, and 160 MHz Wi-Fi channels.
* Add 320 MHz Wi-Fi channels. 🤪
* Show 802.11ax subcarriers.
* Mouseover inspector that draws a vertical line and shows the current frequency.
* Add an option to display the center frequency on each channel label.
* Store settings (such as frequency, zoom level, and selected options) in a cookie.
* Put all of the labels for a particular technology on the same row (I had this in the past but the code was mind-bogglingly complicated and hard to work with).
* Limit panning to the viewable spectrum.
* Expand the spectrum beyond 8 GHz.
* Let the user zoom in more to look at technologies below VHF.

## Feature Requests

If you have a feature request, feel free to [open an issue in GitHub](https://github.com/PotatoFi/spectrum/issues). Just temper your expectations - I am a novice developer, and am already running into the edges of my capabilities a bit.

Thanks for checking out the thing that I made, I hope you like it!
