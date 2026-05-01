# TraceForge — Mic Calibration Compensator

**Current version:** V2.0.03  
**Author:** DoDo7  
**Copyright:** © 2026 Edoardo Montagnoli. All rights reserved.

TraceForge is a browser-based magnitude compensation tool for transfer function measurements through RF systems or other non-transparent measurement paths.

It is designed to help measurement engineers compensate the magnitude response of a wireless/RF measurement path, so measurements made through a cable and measurements made through an RF system can line up more accurately.

The main intended workflow is:

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

TraceForge V2.0.03 includes a default export mode:

```text
Mic Correction Mode — Smaart Compatible
```

This mode is intended for Smaart microphone correction curves.

Smaart microphone correction curves appear to be magnitude-only and are internally subtracted by Smaart. For this reason, TraceForge writes the response curve itself, not an inverted EQ curve.

For software that expects a directly applied EQ-style correction curve, TraceForge also includes:

```text
EQ Mode — Inverted Compensation
```

EQ Mode is hidden under the advanced export mode section and requires confirmation before use.

TraceForge is not affiliated with, endorsed by, or sponsored by Rational Acoustics or Smaart.

---

## Features

- Runs fully in the browser
- No installation required
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
- Smaart-compatible mic correction mode
- Advanced EQ-style inverted compensation mode
- Export to `.txt`
- Responsive layout for desktop, tablet, and mobile
- Donationware support button

---

## How to Use

### 1. Accept the License

When opening TraceForge, a license popup is shown.

Read the license, check the acceptance box, and press:

```text
Accept and Continue
```

The app cannot be used unless the license is accepted.

---

### 2. Load a Mic / Flat Calibration Curve

In the first section:

```text
Mic / Flat Calibration Curve
```

You can either:

- drag and drop a microphone calibration file;
- click the loading area and choose a file;
- or enable:

```text
Use flat 0 dB calibration curve
```

The flat calibration option generates an internal 0 dB curve from 10 Hz to 20 kHz.

If a real calibration file is loaded, the flat calibration mode is automatically disabled.

---

### 3. Load an RF / Path Response

In the second section:

```text
RF / Path Response
```

Load an ASCII transfer function export of the measurement path you want to compensate.

Typical example:

```text
Wireless system measured against a cable/reference path
```

Only magnitude data is used. Phase and coherence columns are ignored.

Alternatively, you can enable:

```text
Demo RF / path response
```

This generates a smooth random demo curve from 10 Hz to 20 kHz with approximately ±6 dB variation.

The demo mode is useful for testing the app without real files.

If a real RF/path response file is loaded, demo mode is automatically disabled.

---

### 4. Set Names

TraceForge lets you define:

- mic / calibration name;
- RF / path name;
- custom name.

The generated output title and filename are automatically built from these fields.

Example:

```text
Isemcon EMX-7150 + Gaodimic RF System compensated - Test 01.txt
```

---

### 5. Choose Normalization

By default, TraceForge normalizes both curves at 1 kHz:

```text
Normalize microphone calibration at 1 kHz
Normalize RF / path response at 1 kHz
```

This removes global level offsets and keeps the compensation focused on the shape of the magnitude response.

Both options can be disabled.

---

### 6. Generate the Compensation Curve

Press:

```text
Generate Compensation Curve
```

TraceForge will:

- parse the calibration file;
- parse the RF/path response;
- normalize curves if enabled;
- interpolate the RF/path response over the calibration frequencies;
- generate the compensated output curve;
- show a graph preview;
- show a table preview;
- prepare the `.txt` export.

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

Advanced mode.

Formula:

```text
Output = Mic Calibration - RF / Path Response
```

Use this only when the target software expects a directly applied EQ-style inverted correction curve.

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

---

## Current Limitations

- Magnitude-only compensation
- No phase compensation
- `.trf` files are not supported in V2.0.03
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

