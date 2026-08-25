# PTH650Driver for macOS



A **personal, headless** Swift driver for exactly one device: **Wacom Intuos5 touch M (PTH-650)** over USB (`056a:0027`). This repository is a private fork of Trifa Studio's Wacom driver and is not a pull request or contribution to the upstream project.



## Scope



The driver keeps the original Trifa Studio HID mode-switch and proven pen path intact. It supports the PTH-650 pen, pressure, tilt, eraser, pen buttons, eight ExpressKeys and the Touch Ring with four hardware-selected modes.



It intentionally contains no menu-bar interface, OLED handling, LED output, profiles, radial menu, Bluetooth support or support for other Wacom models. Multi-touch gestures are not included in the first safe release.



| PTH-650 control | Default direct action |

|---|---|

| ExpressKey 1 | Undo (`Cmd+Z`) |

| ExpressKey 2 | Redo (`Cmd+Shift+Z`) |

| ExpressKey 3 / 4 | Brush size down / up (`[` / `]`) |

| ExpressKey 5 | Hand / Pan (`Space`) |

| ExpressKey 6 | Eyedropper (`Option`) |

| ExpressKey 7 / 8 | Zoom out / in (`Cmd+-` / `Cmd+=`) |

| Touch Ring centre | Cycles the four ring modes |

| Touch Ring | Scroll/zoom, layer cycling, brush size or rotation based on the selected mode |



## Build on macOS



The driver requires macOS 14 or later and Xcode Command Line Tools.



```bash

xcode-select --install

cd IntuosDriver

swift run pth650-tests

swift build -c release

.build/release/pth650-driver --verbose

```



At first run, allow the executable under **System Settings → Privacy & Security → Accessibility**. The process stays in the foreground; keep the Terminal window open while using the tablet. Press `Ctrl+C` to stop it cleanly.



> Do not run the original Wacom driver or another tablet driver that seizes the same HID device at the same time.
> 


## Diagnostic mode



Run without seizing the HID device only for diagnostics:



```bash

.build/release/pth650-driver --no-seize --verbose

```



## Technical references



The PTH-650 identification and panel report layout are documented by [libwacom](https://github.com/linuxwacom/libwacom/blob/master/data/wacom-intuos5-touch-m.tablet) and the [Linux Wacom HID driver](https://github.com/torvalds/linux/blob/master/drivers/hid/wacom_wac.c). See `PTH650_PROTOCOL_NOTES.md` for the intentionally narrow protocol boundary.



## License



The upstream project is MIT-licensed. Retain the upstream licence and attribution when using or redistributing this fork.


