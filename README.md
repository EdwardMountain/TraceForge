# TraceForge — Mic Calibration Compensator

**Current version:** V3.02  
**Author:** DoDo7  
**Copyright:** © 2026 Edoardo Montagnoli. All rights reserved.

A magnitude compensation tool for transfer function measurements through RF systems or other non-transparent measurement paths.

It helps measurement engineers compensate the magnitude response of a wireless/RF measurement path, so measurements made through a cable and measurements made through an RF system line up more accurately.

The main workflow is:

```text
Microphone calibration curve
+
Measured RF / path response
=
New compensated calibration curve
```

The generated file can then be loaded as a microphone correction / calibration curve in compatible measurement software.

---

## Main Use Case

TraceForge is especially useful when a measurement microphone is used through a wireless system instead of a direct cable connection.

For example:

- You have a microphone calibration file for your measurement microphone.
- You measure the transfer function of a wireless microphone system against a cable/reference path.
- The wireless path is not perfectly flat.
- TraceForge combines the microphone calibration curve with the measured RF/path response.
- The result is a new compensated calibration file.

The goal is to make cabled and wireless measurement paths behave more similarly in magnitude.

---

## Important Note About Smaart

TraceForge includes a default export mode:

```text
Mic Correction Mode — Smaart Compatible
```

This mode is intended for Smaart microphone correction curves.

Smaart microphone correction curves appear to be magnitude-only and are internally subtracted by Smaart. For this reason, TraceForge writes the response curve itself, not an inverted EQ curve.

For software that expects a directly applied EQ-style correction curve, TraceForge also includes:

```text
EQ Mode — Inverted Compensation
```

EQ Mode is hidden under the advanced export mode option and requires confirmation before use.

TraceForge is not affiliated with, endorsed by, or sponsored by Rational Acoustics or Smaart.

---

## Features

- Runs fully in the browser, no installation required
- Local file parsing: files are not uploaded by this page
- Supports microphone calibration files in `.txt`, `.crv`, `.csv`, `.tsv`, and ASCII-like text formats
- Supports RF/path response files exported as ASCII `.txt`
- Automatically ignores many common comments, headers, and metadata lines
- Magnitude-only compensation
- 10 Hz – 20 kHz export range
- Log-frequency interpolation
- Optional normalization at 1 kHz
- Built-in flat 0 dB calibration curve
- Built-in demo RF/path response generator
- Live compensation: the output curve is calculated as soon as both curves are loaded and follows every change
- Magnitude graph with cursor readout of all three curves
- Status box with the largest deviation of the output curve from 0 dB
- Smaart-compatible mic correction mode
- Advanced EQ-style inverted compensation mode
- Export to `.txt`
- Dark mode and Daylight mode
- Responsive layout for desktop, tablet, and mobile
- Donationware support button

---

## How to Use

### 1. Accept the License

When opening a new version of TraceForge for the first time, a license popup is shown.

Read the license and press:

```text
Accept
```

The app cannot be used unless the license is accepted. The license is asked again once for every new version. It can be read again at any time from Help → License.

---

### 2. Load a Mic / Flat Calibration Curve

At the top of the page, in the box:

```text
Mic calibration
```

You can either:

- drag and drop a microphone calibration file onto the box;
- press `Load` and choose a file;
- or press:

```text
Flat 0 dB
```

Flat 0 dB generates an internal 0 dB curve from 10 Hz to 20 kHz.

If a real calibration file is loaded, Flat 0 dB is automatically switched off.

---

### 3. Load an RF / Path Response

In the box:

```text
RF / path response
```

Load an ASCII transfer function export of the measurement path you want to compensate, by drag and drop or with `Load`.

Typical example:

```text
Wireless system measured against a cable/reference path
```

Only magnitude data is used. Phase and coherence columns are ignored.

Alternatively, press:

```text
Demo
```

This generates a smooth random demo curve from 10 Hz to 20 kHz with approximately ±6 dB variation. Press `↻` to generate a new demo curve.

The demo mode is useful for testing the app without real files.

If a real RF/path response file is loaded, demo mode is automatically switched off.

The sign between the two boxes shows the operation in use: `+` in Mic Correction Mode, `−` in EQ Mode.

---

### 4. Check the Compensation Curve

As soon as both curves are loaded, TraceForge:

- normalizes the curves if enabled;
- interpolates the RF/path response over the calibration frequencies;
- calculates the compensated output curve;
- shows it on the graph;
- fills the Output data table;
- prepares the `.txt` export.

There is no Generate button. Loading a new curve or changing any option updates the output right away.

On the graph, the mic calibration is drawn in blue, the RF/path response in orange, and the compensated output as a dashed violet line. When the output coincides with the RF/path response (for example with a flat calibration curve), the orange line stays visible inside the dashes.

The status box shows the largest deviation of the output curve from 0 dB, the number of points of each curve, and the operation in use.

The Output data table and the Parser log are collapsible panels below the graph, closed by default.

---

### 5. Set Names

In the Names section, TraceForge lets you define:

- mic / calibration name;
- RF / path name;
- custom name.

The curve title and the file name are built automatically from these fields.

Example:

```text
Isemcon EMX-7150 + Gaodimic RF System compensated - Test 01.txt
```

---

### 6. Choose Normalization

By default, TraceForge normalizes both curves at 1 kHz:

```text
Normalize mic calibration at 1 kHz
Normalize RF / path response at 1 kHz
```

This removes global level offsets and keeps the compensation focused on the shape of the magnitude response.

Both options can be disabled. When normalization is on, a `Ref 1 kHz` marker is shown on the graph.

---

### 7. Download the Output

Press:

```text
Download .txt
```

The generated file can then be imported into compatible measurement software as a magnitude correction / calibration curve.

---

## Export Modes

### Mic Correction Mode — Smaart Compatible

Default mode.

Formula:

```text
Output = Mic Calibration + RF / Path Response
```

Use this mode for Smaart microphone correction curves.

This is the default and recommended mode for the intended TraceForge workflow.

---

### EQ Mode — Inverted Compensation

Advanced mode. Enable `Show advanced export mode` to see it.

Formula:

```text
Output = Mic Calibration - RF / Path Response
```

Use this only when the target software expects a directly applied EQ-style inverted correction curve.

TraceForge asks for confirmation before switching to EQ Mode. Hiding the advanced export mode switches back to Mic Correction Mode.

Do not use EQ Mode for Smaart microphone correction curves unless you are absolutely sure that is what you need.

---

## Input File Notes

TraceForge tries to intelligently extract useful frequency and magnitude data from different text-based formats.

Expected useful data is generally:

```text
Frequency    Magnitude
```

Example:

```text
10      -0.42
12.5    -0.38
16      -0.31
20      -0.25
```

The parser attempts to ignore:

- empty lines;
- comments;
- headers;
- metadata;
- sensitivity notes;
- model information;
- non-numeric lines;
- duplicate frequency entries.

For RF/path response files, only magnitude is used. Phase and coherence data are ignored in the current version.

If a file cannot be read, a message appears at the bottom of the page. The Parser log shows what was read from each file and one summary line for each update of the output.

---

## Settings Kept Between Sessions

Every time TraceForge opens, curves, names and options start from their defaults. Only the colour mode (Dark or Daylight) is remembered.

---

## Current Limitations

- Magnitude-only compensation
- No phase compensation
- `.trf` files are not supported yet
- RF/path response input should be ASCII/text-based
- Output is `.txt`
- Smaart behavior is based on practical testing and expected microphone correction behavior

If Rational Acoustics ever adds phase support to microphone correction curves, phase compensation could be added to TraceForge in a future version.

---

## Privacy

TraceForge runs locally in the browser.

The files are parsed by the browser page and are not uploaded by this page.

---

## Donation

TraceForge is distributed as freeware/donationware.

A donation is optional and does not grant ownership of the software, source code, intellectual property, branding, or any additional rights beyond the permission to use the software under the license.

Donation link:

```text
https://paypal.me/edoardomontagnoli
```

---

## License

TraceForge is proprietary freeware/donationware.

Copyright © 2026 Edoardo Montagnoli.  
All rights reserved.

Permission is granted to access and use the official version of the software for personal, evaluation, testing, demonstration, and non-commercial use only.

Redistribution, resale, mirroring, re-hosting, modification, deobfuscation, reverse engineering, extraction, reuse, republication, or creation of derivative works is not allowed without prior written permission from the copyright holder.

See the full license included in this repository and shown inside the app before use.

---

## Warranty Disclaimer

TraceForge is provided “as is”, without warranty of any kind.

The author is not responsible for any damage, data loss, malfunction, interruption, measurement error, financial loss, or any other consequence arising from the use or inability to use this software.

---

## Version History

### V3.02

- The compensation curve is calculated automatically as soon as both curves are loaded and follows every change
- Removed the Generate button; Download .txt is now the main action
- Parser log: one summary line for each update of the output

### V3.01

- Compensated output drawn as a dashed line, so it no longer hides the RF/path response when the two coincide
- New anvil logo
- Header on two rows, with the full product description next to the name

### V3.00

- New interface, shared with the other DoDo7 tools: Dark mode and Daylight mode, Barlow typeface, one-screen layout on desktop
- Mic calibration and RF/path response boxes at the top, with drag and drop, Flat 0 dB and Demo buttons
- Magnitude graph with cursor readout and 1 kHz reference marker
- Status box with the largest output deviation from 0 dB
- Output data table and Parser log as collapsible panels
- EQ Mode confirmation in an in-app window
- License accepted once per version; Help panel with the user guide
- Export format and calculation unchanged from V2.0.03

### V2.0.03

- Removed `public` from exported `.txt` filenames
- Added public license acceptance popup
- Added freeware/donationware legal notice
- Added donation link
- Includes Smaart-compatible mic correction mode
- Includes advanced EQ Mode
- Includes demo RF/path response generator
- Includes flat 0 dB calibration curve
- Exports magnitude-only `.txt` files from 10 Hz to 20 kHz

---

## Author

**DoDo7**  
Copyright © 2026 Edoardo Montagnoli.  
All rights reserved.
