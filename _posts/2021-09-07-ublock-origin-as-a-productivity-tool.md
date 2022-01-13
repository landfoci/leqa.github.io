---
layout: post
title: uBlock Origin as a productivity tool
---

There are about a million bajillion articles already about maximizing
your productivity as part of your sigma male astrotrillionaire grindset.
A common suggestion is to block sites that are time sinks like Reddit
and YouTube. The problem with this approach is that these sites also
contain useful information. You might search for an error message and
come across a Reddit post, but a plain hostname filter can't distinguish
between helpful content and entertainment. What ended up happening to me
was that I would temporarily work around or disable the filter, but once
I did that, it became much easier to do the same for entertainment.

The truth about such websites is that they are designed to suck you in
for as long as possible. A large and possibly the most important factor
in this goal is an infinitely scrolling list of recommendations that
link to other content. If we can get rid of this, then we have
eliminated the biggest temptation to waste time while still allowing
one-time access. A blocker extension like uBlock Origin ([Chrome](https://chrome.google.com/webstore/detail/ublock-origin/cjpalhdlnbpafiamejdnhcphjbkeiagm?hl=en),
[Firefox](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/)),
widely recommended for its high performance and low resource usage
relative to competitors, allows you to block any element you choose.
Here's how:

**STEP ONE** Click on the extension icon that can be found next to the
address bar or under the Extensions button that looks like a puzzle
piece. Enter element picker mode by clicking on the eyedropper icon.

![uBlock Origin popup on YouTube video](/assets/popup.jpg)

**STEP TWO** Move and hover your cursor until the distracting element is
highlighted. Click to select it.

![Element picker with YouTube recommendation sidebar selected](/assets/picker.jpg)

**STEP THREE** If you made a mistake, click the pick button. Otherwise,
click create. You might have to adjust the sliders if too much or too
little is blocked.

![YouTube video with empty sidebar](/assets/after.jpg)

Now you can look up and watch individual videos without worrying about
getting sucked into mindlessly browsing.
