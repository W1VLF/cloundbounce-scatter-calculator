# Cloud Bounce Scatter Calculator

A link-budget calculator for 940 nm optical "cloud bounce" paths. These are non-line-of-sight links where an IR LED transmitter lights the base of a cloud deck and a distant receiver picks up the scattered light. It was built for W1VLF's 34.73-mile JohnnyCake–JMH path in Connecticut, and it works for any path.

<p align="center">
  <a href="https://raw.githack.com/W1VLF/cloundbounce-scatter-calculator/main/index.html"><img src="https://img.shields.io/badge/%E2%96%B6%20Open%20calculator-in%20your%20browser-b3245c?style=for-the-badge" alt="Open calculator in your browser"></a>
  &nbsp;
  <a href="https://github.com/W1VLF/cloundbounce-scatter-calculator/archive/refs/heads/main.zip"><img src="https://img.shields.io/badge/%E2%AC%87%20Download-ZIP-1b6f8a?style=for-the-badge" alt="Download ZIP"></a>
</p>

**Open calculator** runs it straight away in your browser, with nothing to install. **Download ZIP** gets you a copy to keep. Unzip it and double-click `index.html` to open it offline.

The calculator compares two geometries:

- **Forward** — the bounce spot sits between the two stations. The light glances off the cloud base at a shallow angle, turning only a few degrees.
- **Backscatter** — both stations face the same direction, like two people in the back and front rows of a theater. The spot sits past the receiver, and the light scatters almost straight back (~175–180°).

```
 FORWARD                              BACKSCATTER
 ~~~~~~~~~~~*~~~~~~~~~~~ cloud        ~~~~~~~~~~~~~~~~~~~~*~~ cloud
           / \                                       __-- /
          /   \                               __--    /
         /     \                        __--      /
     [TX A]   [RX B]               [TX A]  ...  [RX B]
  spot between stations           spot past RX, both face the same way
```

## How to use it

1. Click **Open calculator** above, or download the ZIP and open `index.html` in any modern browser. It works offline apart from the web fonts.
2. Enter your path and equipment in the left-hand panel: path distance, station heights, cloud base (METAR ceiling), haze, TX optical power and beamwidth, RX aperture, field of view, optics loss, detector NEP, and decode threshold.
3. Pick a **path geometry** (Forward / Backscatter) and a **cloud model** (Matte surface / Droplet scatter).
4. Drag the slider to move the bounce spot, or click **Best SNR** to jump to the best position.
5. Read the results:
   - **Aim elevation** for the TX and RX, plus received power, SNR in 2.5 kHz, and margin over the decode threshold.
   - **Forward vs backscatter** finds each geometry's best spot under both cloud models and shows the dB advantage, plus a chart of best SNR against path distance.
   - **Link budget** and **Geometry** tables, and SNR plotted against bounce position, cloud base, and distance.

Inputs are remembered in your browser between visits. **Reset defaults** restores the starting values.

**Same-site test:** set the path distance to 0 in backscatter mode, with both units side by side and pointing up. This is the easiest way to measure your real cloud return and calibrate the model.

## Model in brief

- Spherical Earth (R = 6371 km), no refraction.
- Height-dependent haze extinction, integrated along each slant leg.
- **Matte surface:** Lambertian reflection, ρ·cosθ/π. It ignores the scatter angle and probably reads low for forward paths.
- **Droplet scatter:** single scattering using an approximate water-droplet phase function at 940 nm, with a strong forward peak and a small glory near 180°. It probably reads high at grazing angles.
- Receiver FOV vs TX spot overlap, and a detector-NEP-only noise floor (night operation assumed).

## Accuracy

Treat the absolute SNR as good to roughly **±15 dB**. Trends such as the best spot position, the benefit of a higher ceiling, and the fall-off with distance are more reliable than the absolute level. The real answer usually falls between the matte and droplet results. If one geometry wins under both models, it will very likely win in the field. Calibrate with a test on a real overcast night.

## Files

- `index.html` — the complete calculator in a single self-contained file
- `README.md` — this file

---
W1VLF · Connecticut
