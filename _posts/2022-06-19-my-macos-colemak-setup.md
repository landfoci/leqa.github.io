---
layout: post
title: My macOS Colemak setup
---

[Colemak](https://colemak.com/) is an alternative to the default QWERTY keyboard layout. It claims to be superior, but what makes a layout better than another? Here are what I believe to be the three main metrics.

- The most obvious metric would be easy reach of the most frequent letters. QWERTY only has a single vowel on the home row, while Colemak has four. QWERTY does terribly here because it was designed to separate the most common English digraphs, as pressing keys next to each other too fast would jam typewriters. (Fun fact: did you know "typewriter" can be typed all on QWERTY's top row? It is said that this was to help early typewriter sales demos.)
- Minimizes successive letters being hit by the same finger. For example, try typing "mummy" on QWERTY.
- Balances load between left and right hands. On QWERTY you can type "sweaterdresses" just with one hand.

![Colemak layout](https://upload.wikimedia.org/wikipedia/commons/8/84/KB_US-Colemak.svg)
<p align="center"><em>A map of Colemak from <a href="https://commons.wikimedia.org/wiki/File:KB_US-Colemak.svg">Wikipedia</a></em></p>

Colemak is supposed to be an improvement on [Dvorak](https://en.wikipedia.org/wiki/Dvorak_keyboard_layout), the oldest and most popular alternative keyboard. The main difference is that Dvorak was designed with an emphasis on hand alternation while Colemak optimizes for "roll combos" or sequences of keys next to each other. To see what I mean, try typing "fhlsdf" on QWERTY, which is "thirst" in Colemak. The s-d-f or r-s-t sequence can be very quickly and comfortably executed in a single motion, which is what is meant by rolls. Another plus is that the positions of Z/X/C/V for the common undo, cut, copy, and paste shortcuts are preserved so you can continue using those with your left hand with the mouse in your right hand. That being said, both are such an improvement over QWERTY that either will be fine.

So, should you switch to Colemak? Despite all the benefits I've been raving about, I would say only switch if you're currently slower than 60 WPM or have never learned to touch type properly with eight fingers on the home row. If you haven't mastered touch typing, then might as well start with a better layout. But the chances of successfully grinding through the month-or-longer drop in productivity as you learn a new layout drop the more you are over 60 WPM. Besides, just improving your posture would likely do much more for ergonomics than your keyboard layout.

If you do switch, here's a tip I consider indispensible: keep your phone on QWERTY. The properties that make QWERTY bad for touch typing make it great for thumb typing, and it keeps your QWERTY skills in shape for when you need to use other people's computers. Even Colemak's creator agrees that it is not optimal for phones.

If you don't switch, here's another recommendation: at least map your caps lock key to something else. I choose backspace, which frees up my actual backspace key to be remapped to delete forward. This makes for a greatly improved text editing experience with barely any disruption to productivity. Caps lock to control for PC and Emacs users and escape for Vim users are common alternatives. (macOS uses the command key instead of control, which is hit by the thumb and thus in a better position than the control and caps lock keys anyways, and I use ^C to escape in Vim.)

I use [Karabiner Elements](https://karabiner-elements.pqrs.org) to customize my keyboard beyond the predefined layouts included with the operating system. On Windows, [AutoHotKey](https://www.autohotkey.com) seems to be the dominant choice. If you're on Linux, you can probably figure it out yourself. Karabiner includes a simple modifications GUI where you can change caps lock to backspace and so on. This is what I used to do, but if somebody else wanted to use my computer, I would have to change the input source back to QWERTY and quit Karabiner. I recently found out that Karabiner supports complex modifications that trigger on certain conditions. This lets me automatically disable all my customizations whenever I switch the input source to QWERTY, so I don't have to manually quit Karabiner every time I pair program.

You can import my rule through the [complex modifications user repository](https://ke-complex-modifications.pqrs.org/#colemak-caps-lock-backspace-delete-swap) or by copying the following JSON into a file at `~/.config/karabiner/assets/complex_modifications`. Note that this only enables the mapping if the current input source is set to Colemak. Maybe you type in multiple languages and only want to disable everything for one layout. In that case, replace `input_source_if` to `input_source_unless` and edit the `input_source_id` value accordingly. See the [documentation](https://karabiner-elements.pqrs.org/docs/json/) for more details.

```json
{
  "title": "Caps lock to backspace and backspace to delete forward, but only on Colemak",
  "rules": [
    {
      "description": "Caps lock to backspace, but only on Colemak",
      "manipulators": [
        {
          "type": "basic",
          "from": {
            "key_code": "caps_lock",
            "modifiers": {
              "optional": [
                "any"
              ]
            }
          },
          "to": [
            {
              "key_code": "delete_or_backspace",
              "lazy": false,
              "repeat": true
            }
          ],
          "conditions": [
            {
              "type": "input_source_if",
              "description": "Colemak",
              "input_sources": [
                {
                  "input_source_id": "^com\\.apple\\.keylayout\\.Colemak$"
                }
              ]
            }
          ]
        }
      ]
    },
    {
      "description": "Backspace to delete forward, but only on Colemak",
      "manipulators": [
        {
          "type": "basic",
          "from": {
            "key_code": "delete_or_backspace",
            "modifiers": {
              "optional": [
                "any"
              ]
            }
          },
          "to": [
            {
              "key_code": "delete_forward",
              "lazy": false,
              "repeat": true
            }
          ],
          "conditions": [
            {
              "type": "input_source_if",
              "description": "Colemak",
              "input_sources": [
                {
                  "input_source_id": "^com\\.apple\\.keylayout\\.Colemak$"
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

There are a ton of user-submitted configs to explore. I also recommend [left control + hjkl to arrow keys](https://ke-complex-modifications.pqrs.org/#vi_mode_arrow). The possibilities are endless!
