---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : Karabiner complex rules # 제목
excerpt             : Karabiner complex rules # 썸네일 한줄 요약
categories          : ETC
tags                : ETC
---

출처 : 본인

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

본인이 아주 행복하게 잘 사용중인 Karabiner complex rules 목록

## 목록

```json
// ~/.config/karabiner/karabiner.json

{
  "global": {
    "check_for_updates_on_startup": false,
    "show_in_menu_bar": false,
    "show_profile_name_in_menu_bar": false,
    "unsafe_ui": false
  },
  "profiles": [
    {
      "complex_modifications": {
        "parameters": {
          "basic.simultaneous_threshold_milliseconds": 50,
          "basic.to_delayed_action_delay_milliseconds": 500,
          "basic.to_if_alone_timeout_milliseconds": 1000,
          "basic.to_if_held_down_threshold_milliseconds": 500,
          "mouse_motion_to_scroll.speed": 100
        },
        "rules": [
          {
            "description": "fn + o to [",
            "manipulators": [
              {
                "from": {
                  "key_code": "o",
                  "modifiers": {
                    "mandatory": ["fn"]
                  }
                },
                "to": [
                  {
                    "key_code": "open_bracket"
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + shift + o to {",
            "manipulators": [
              {
                "from": {
                  "key_code": "o",
                  "modifiers": {
                    "mandatory": ["fn", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "open_bracket",
                    "modifiers": ["left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + p to ]",
            "manipulators": [
              {
                "from": {
                  "key_code": "p",
                  "modifiers": {
                    "mandatory": ["fn"]
                  }
                },
                "to": [
                  {
                    "key_code": "close_bracket"
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + shift + p to }",
            "manipulators": [
              {
                "from": {
                  "key_code": "p",
                  "modifiers": {
                    "mandatory": ["fn", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "close_bracket",
                    "modifiers": ["left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + 9 to [",
            "manipulators": [
              {
                "from": {
                  "key_code": "9",
                  "modifiers": {
                    "mandatory": ["fn"]
                  }
                },
                "to": [
                  {
                    "key_code": "hyphen"
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + shift + 9 to _",
            "manipulators": [
              {
                "from": {
                  "key_code": "9",
                  "modifiers": {
                    "mandatory": ["fn", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "hyphen",
                    "modifiers": ["left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + 0 to =",
            "manipulators": [
              {
                "from": {
                  "key_code": "0",
                  "modifiers": {
                    "mandatory": ["fn"]
                  }
                },
                "to": [
                  {
                    "key_code": "equal_sign"
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + shift + 0 to +",
            "manipulators": [
              {
                "from": {
                  "key_code": "0",
                  "modifiers": {
                    "mandatory": ["fn", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "equal_sign",
                    "modifiers": ["left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + i to up_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["fn"]
                  }
                },
                "to": [
                  {
                    "key_code": "up_arrow"
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + control + i to control + up_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["fn", "left_control"]
                  }
                },
                "to": [
                  {
                    "key_code": "up_arrow",
                    "modifiers": ["left_control"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + option + i to option + up_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["fn", "left_option"]
                  }
                },
                "to": [
                  {
                    "key_code": "up_arrow",
                    "modifiers": ["left_option"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + command + i to command + up_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["fn", "left_command"]
                  }
                },
                "to": [
                  {
                    "key_code": "up_arrow",
                    "modifiers": ["left_command"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + shift + i to shift + up_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["fn", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "up_arrow",
                    "modifiers": ["left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + control + shift + i to control + shift + up_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["fn", "left_control", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "up_arrow",
                    "modifiers": ["left_control", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + option + shift + i to option + shift + up_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["fn", "left_option", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "up_arrow",
                    "modifiers": ["left_option", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + command + shift + i to command + shift + up_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["fn", "left_command", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "up_arrow",
                    "modifiers": ["left_command", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "right command + i to mouse cursor up",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "y": -1600
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "command + right command + i to mouse cursor up slow",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["left_command", "right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "y": -800
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "shift + right command + i to mouse cursor up fast",
            "manipulators": [
              {
                "from": {
                  "key_code": "i",
                  "modifiers": {
                    "mandatory": ["left_shift", "right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "y": -3200
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + j to left_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["fn"]
                  }
                },
                "to": [
                  {
                    "key_code": "left_arrow"
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + control + j to control + left_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["fn", "left_control"]
                  }
                },
                "to": [
                  {
                    "key_code": "left_arrow",
                    "modifiers": ["left_control"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + option + j to option + left_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["fn", "left_option"]
                  }
                },
                "to": [
                  {
                    "key_code": "left_arrow",
                    "modifiers": ["left_option"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + command + j to command + left_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["fn", "left_command"]
                  }
                },
                "to": [
                  {
                    "key_code": "left_arrow",
                    "modifiers": ["left_command"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + shift + j to shift + left_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["fn", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "left_arrow",
                    "modifiers": ["left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + control + shift + j to control + shift + left_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["fn", "left_control", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "left_arrow",
                    "modifiers": ["left_control", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + option + shift + j to option + shift + left_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["fn", "left_option", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "left_arrow",
                    "modifiers": ["left_option", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + command + shift + j to command + shift + left_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["fn", "left_command", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "left_arrow",
                    "modifiers": ["left_command", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "right command + j to mouse cursor left",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "x": -1600
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "command + right command + j to mouse cursor left slow",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["left_command", "right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "x": -800
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "shift + right command + j to mouse cursor left fast",
            "manipulators": [
              {
                "from": {
                  "key_code": "j",
                  "modifiers": {
                    "mandatory": ["left_shift", "right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "x": -3200
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + k to down_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["fn"]
                  }
                },
                "to": [
                  {
                    "key_code": "down_arrow"
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + control + k to control + down_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["fn", "left_control"]
                  }
                },
                "to": [
                  {
                    "key_code": "down_arrow",
                    "modifiers": ["left_control"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + option + k to option + down_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["fn", "left_option"]
                  }
                },
                "to": [
                  {
                    "key_code": "down_arrow",
                    "modifiers": ["left_option"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + command + k to command + down_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["fn", "left_command"]
                  }
                },
                "to": [
                  {
                    "key_code": "down_arrow",
                    "modifiers": ["left_command"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + shift + k to shift + down_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["fn", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "down_arrow",
                    "modifiers": ["left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + control + shift + k to control + shift + down_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["fn", "left_control", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "down_arrow",
                    "modifiers": ["left_control", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + option + shift + k to option + shift + down_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["fn", "left_option", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "down_arrow",
                    "modifiers": ["left_option", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + command + shift + k to command + shift + down_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["fn", "left_command", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "down_arrow",
                    "modifiers": ["left_command", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "right command + k to mouse cursor down",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "y": 1600
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "command + right command + k to mouse cursor down slow",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["left_command", "right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "y": 800
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "shift + right command + k to mouse cursor down fast",
            "manipulators": [
              {
                "from": {
                  "key_code": "k",
                  "modifiers": {
                    "mandatory": ["left_shift", "right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "y": 3200
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + l to right_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["fn"]
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
          },
          {
            "description": "fn + control + l to control + right_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["fn", "left_control"]
                  }
                },
                "to": [
                  {
                    "key_code": "right_arrow",
                    "modifiers": ["left_control"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + option + l to option + right_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["fn", "left_option"]
                  }
                },
                "to": [
                  {
                    "key_code": "right_arrow",
                    "modifiers": ["left_option"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + command + l to command + right_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["fn", "left_command"]
                  }
                },
                "to": [
                  {
                    "key_code": "right_arrow",
                    "modifiers": ["left_command"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + shift + l to shift + right_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["fn", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "right_arrow",
                    "modifiers": ["left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + control + shift + l to control + shift + right_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["fn", "left_control", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "right_arrow",
                    "modifiers": ["left_control", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + option + shift + l to option + shift + right_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["fn", "left_option", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "right_arrow",
                    "modifiers": ["left_option", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "fn + command + shift + l to command + shift + right_arrow",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["fn", "left_command", "left_shift"]
                  }
                },
                "to": [
                  {
                    "key_code": "right_arrow",
                    "modifiers": ["left_command", "left_shift"]
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "right command + l to mouse cursor right",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "x": 1600
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "command + right command + l to mouse cursor right slow",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["left_command", "right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "x": 800
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "shift + right command + l to mouse cursor right fast",
            "manipulators": [
              {
                "from": {
                  "key_code": "l",
                  "modifiers": {
                    "mandatory": ["left_shift", "right_command"]
                  }
                },
                "to": [
                  {
                    "mouse_key": {
                      "x": 3200
                    }
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "right command + z to mouse button1",
            "manipulators": [
              {
                "from": {
                  "key_code": "z",
                  "modifiers": {
                    "mandatory": ["right_command"]
                  }
                },
                "to": [
                  {
                    "pointing_button": "button1"
                  }
                ],
                "type": "basic"
              }
            ]
          },
          {
            "description": "right command + x to mouse button2",
            "manipulators": [
              {
                "from": {
                  "key_code": "x",
                  "modifiers": {
                    "mandatory": ["right_command"]
                  }
                },
                "to": [
                  {
                    "pointing_button": "button2"
                  }
                ],
                "type": "basic"
              }
            ]
          }
        ]
      },
      ...
```
