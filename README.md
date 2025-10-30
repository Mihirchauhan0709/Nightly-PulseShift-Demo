
# Nightly Mini‑Challenge: PulseShift Crowd Energy Demo

**Author:** Mihir Chauhan  
**Date:** 2025-10-30

This lightweight demo analyzes a 30–60 second crowd video and produces:
1. An **energy-over-time** curve from visual motion and audio loudness.  
2. **Show-cue suggestions** at detected low-energy moments.  
3. A **10-second highlight clip** from the highest-energy window.

It is built to be simple, transparent, and easy to run in **Google Colab**.

---

## Approach

**Energy metric**
- **Motion energy**: frame-to-frame difference or optical-flow magnitude using OpenCV on downsampled grayscale frames.
- **Audio energy**: RMS loudness from the video’s audio track using `librosa`.
- **Fusion**: normalized motion and audio energies are averaged (weights configurable) and smoothed with a short moving average.
- **Low-energy moments**: troughs below a quantile threshold with a minimum spacing to avoid duplicates.
- **Highlight**: sliding-window sum over 10 seconds to find the maximum-energy segment.

**Cue generator**
- For each low-energy moment, output one simple, actionable idea such as:
  - Scoreboard prompt: MAKE SOME NOISE
  - Chant start: OLE OLE OLE
  - Ribbon-board ripple in team colors
  - Clap pattern on PA: clap-clap-clap
  - Wave cue: sections light up front-to-back
  - Fan-cam on diehards + lower-bowl lights up
  - Stadium beat build, then whoosh SFX
  - Spotlight sweep across stands
  - Drumline hit on 1 and 3 for 8 bars
  - Call and response: LEFT SIDE vs RIGHT SIDE

Cues are intentionally generic so they fit concerts, sports, or festivals without assuming specific stage gear.

---

## Run in Google Colab

1. Open the notebook: **`Nightly_PulseShift_Demo.ipynb`** in Colab.  
2. Run the first cell to install dependencies.  
3. Upload your 30–60 second crowd video when prompted (MP4 recommended).  
4. Click **Run All**.  
5. Outputs:
   - `energy_plot.png` showing the energy curve, cue markers, and the highlight window.
   - `cues.json` with timestamps and cue text.
   - `energy.csv` with per-second energy values.
   - `highlight_clip.mp4` with the top 10-second moment.

---

## Files

- **Nightly_PulseShift_Demo.ipynb**: Colab-ready notebook.
- **README.md**: This document.

---
