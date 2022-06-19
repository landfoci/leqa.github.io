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

If you don't switch, here's another recommendation: at least map your caps lock key to something else. Colemak changes it to backspace and so do I, but control for PC users and escape for Vim users are common alternatives. (macOS uses the command key instead of control, which is hit by the thumb and thus in a better position than the control and caps lock keys anyways, and I use ^C to escape in Vim.) That frees up the actual backspace key to be remapped to delete forward. Combined with binding control+hjkl to the arrow keys, this makes for a greatly improved text editing experience with barely any disruption to your productivity.

Below are my [Karabiner](https://karabiner-elements.pqrs.org/) configs for the above. Put them in a JSON file at `~/.config/karabiner/assets/complex_modifications` to install them.

## Control-HJKL to arrow keys

```json
{
  "title": "Vi Mode, left_control + hjkl. shift/option/command + arrow working.",
  "rules": [
    {
      "description": "Vi Mode [left_control + hjkl]",
      "manipulators": [
        {
          "from": {
            "key_code": "h",
            "modifiers": {
              "mandatory": [
                "control"
              ],
              "optional": [
                "caps_lock",
                "command",
                "option",
                "shift",
                "fn"
              ]
            }
          },
          "to": [
            {
              "key_code": "left_arrow"
            }
          ],
          "type": "basic"
        },
        {
          "from": {
            "key_code": "j",
            "modifiers": {
              "mandatory": [
                "control"
              ],
              "optional": [
                "caps_lock",
                "command",
                "option",
                "shift",
                "fn"
              ]
            }
          },
          "to": [
            {
              "key_code": "down_arrow"
            }
          ],
          "type": "basic"
        },
        {
          "from": {
            "key_code": "k",
            "modifiers": {
              "mandatory": [
                "control"
              ],
              "optional": [
                "caps_lock",
                "command",
                "option",
                "shift",
                "fn"
              ]
            }
          },
          "to": [
            {
              "key_code": "up_arrow"
            }
          ],
          "type": "basic"
        },
        {
          "from": {
            "key_code": "l",
            "modifiers": {
              "mandatory": [
                "control"
              ],
              "optional": [
                "caps_lock",
                "command",
                "option",
                "shift",
                "fn"
              ]
            }
          },
          "to": [
            {
              "key_code": "right_arrow"
            }
          ],
          "type": "basic"
        }
      ]
    }
  ]
}
```

## Caps lock to backspace and backspace to delete forward

...but only if Colemak is the current input source so it's automatically disabled if I switch to QWERTY for other people to use my computer. If you don't need this functionality you can just do it through Karabiner's simple modifications GUI.

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
