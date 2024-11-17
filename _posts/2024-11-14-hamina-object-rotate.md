---
title: Rotating Objects in Hamina Network Planner
date: 2024-11-17 20:55:00
categories: [Wi-Fi, Tools]
tags: [Wi-Fi, Hamina]
image:
  path: assets/hamina-object-rotate/hamina-object-rotate-preview.png
---

In [Hamina Network Planner](https://www.hamina.com/planner), Attenuating Objects are used to represent solid objects such as warehouse shelves. They can be drawn either as [rectangles of free-form shapes](https://docs.hamina.com/planner/basics/attenuating-objects), and can have a custom lower height and upper height, making it possible to model just about anything, including things like office furniture.

Duplicating objects is straightforward with `Command` + `C` and `Command` + `V`, but what if you need to rotate an attenuating object or group of objects? At the time of this writing, Hamina Network Planner doesn't support that, so I used [Claude.ai](https://claude.ai/) to write a small web app that does it for us.

You can find the tool at [www.potatofi.com/rotate](https://www.potatofi.com/rotate/).

# Usage

1. In Hamina Network Planner, use the **Edit** tool to select one or more Attenuating Objects. You can either `Shift` + click each object, or drag a box around everything that you want to select. ![](assets/hamina-object-rotate/copy-objects.png)
2. Press `Command` + `C` to put the Attenuating Objects on your clipboard. They're copy out of Hamina as JSON text that you can paste into any text field.
3. In the [Hamina Object Rotate tool](https://www.potatofi.com/rotate/), click the **Clear Objects** button.
4. Paste the Attenuating Objects into the **Input Objects** field.
5. When you're done rotating the objects, click the **Copy to Clipboard** button to put them back on your clipboard. ![](assets/hamina-object-rotate/copy-to-clipboard.png)
6. Paste the objects back into Hamina Network Planner with `Command` + `V`.
7. Using the **Edit** tool, click and drag *on the edge* of one of the attenuating objects to move them around as a group. ![](assets/hamina-object-rotate/move-objects.png)
