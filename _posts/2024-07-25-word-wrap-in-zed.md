---
title: Enabling Word Wrap in Zed
date: 2024-07-25 16:32:00
categories: [Technology, Development]
tags: [development, zed]     # TAG names should always be lowercase
---

Ever since Atom was retired, I've been using Zed as my go-to simple text editor. While editing Markdown for this blog, I was annoyed that Zed didn't seem to do word wrap, even though it understood that the file was Markdown format. Here's how I was able to enable it at the /project/ level.

1. Press `Command` + `Shift` + `P`
2. Type `local` and select `zed: open local settings`
3. Add this to `settings.json`:

```
{
  "soft_wrap": "editor_width"
}
```

4. Press `Command` + `S` to save the file.

Zed should now wrap within the project.

![Zed, with proper word wrapping.](/assets/zed-wrapping.png)
