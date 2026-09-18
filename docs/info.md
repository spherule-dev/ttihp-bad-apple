<!---

This file is used to generate your project datasheet. Please fill in the information below and delete any unused
sections.

You can also include images in this folder and reference them in the markdown. Each image must be less than
512 kb in size, and the combined size of all images must be less than 1 MB.
-->

## How it works

This project generates a standard 640×480 @ 60 Hz monochrome VGA video stream that plays a 60-frame, low-resolution animation of **Bad Apple!!** over a 10-second loop:

* **VGA Signal Generation**: The `hvsync_generator` module produces 640×480 timing pulses (`hsync` and `vsync`) and outputs pixel coordinates (`pix_x`, `pix_y`).
* **Frame Storage & Scaling**: The 32×16 monochrome frames of the "Bad Apple!!" animation are stored in an on-chip ROM (`video_rom`) across 960 32-bit words. A centered 512×256 window on the display scales each internal pixel up by 16×16 screen pixels.
* **Frame Playback**: The design divides the 60 Hz vertical refresh rate by 10, stepping through the 60 animation frames at 6 FPS for an exact 10-second playback cycle before looping.
* **Synchronous Pipelining**: A 2-cycle pipeline aligns the sync and window signals with the synchronous ROM latency to ensure stable pixel presentation.
* **Pin Mapping**: The outputs are assigned directly to match the standard Tiny Tapeout digital VGA Pmod DAC pinout `{hsync, B0, G0, R0, vsync, B1, G1, R1}` on `uo_out`.

## How to test

1. Connect a Tiny Tapeout digital VGA Pmod (R-2R DAC) to the project output header (`uo_out`).
2. Attach a VGA monitor capable of displaying 640×480 resolution.
3. Observe the screen: a centered window will display the low-resolution 32×16 monochrome **Bad Apple!!** music video animation running at 6 FPS, smoothly looping every 10 seconds.

## External hardware

List external hardware used in your project (e.g. PMOD, LED display, etc), if any
