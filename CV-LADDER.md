# Kiln — the CV ladder

Settled in a grilling session on 2026-11-12. This file is the CV ladder. When something changes, change it here. It runs beside the Go ladder in `LADDER.md`, which is unchanged.

## The idea

**QS is the textbook.** QS is our real product: a quality-inspection station for a food factory's line, sold with my friend. AI keeps building QS fast. I learn from it, one module at a time, from the basics up.

**Goal:** become an applied industrial CV engineer. That means someone who can build, measure and deploy inspection, measurement and anomaly detection on a real line, on hardware we can actually buy, and debug it on site alone.

**Each level is one QS module.** Every level runs the same loop:

1. **Study.** The picks for the level in `CV-RESOURCES.md`: chapters, one video series, a paper or tutorial. One book at a time, and only the parts the level needs.
2. **Explain.** Read the QS module named in the "QS module" column. Write `notes/<level>.md` in `cv-lab`: what it does, why this method, and what would break it on the line. If I can't explain it, I go back to step 1.
3. **Rebuild.** Write a small version by hand in my public repo `cv-lab`, one folder per level. Run it on QS images, compare it with QS's version and report **one measured number**.

**Stack:** Python, NumPy, OpenCV first. I add PyTorch, scikit-image and other libraries only when a level needs them.

## CV milestones ("I can do applied CV" means these)

1. From an empty folder, with no AI, I load an image, change color spaces, threshold, find contours and measure them, with tests.
2. I find a known shape (a cup rim) on real line frames with edges plus fitting or Hough, and I report its hit rate on frames I labeled.
3. I measure a part in millimetres from a calibrated camera and state the error.
4. I build an anomaly detector and evaluate it honestly: AUROC on MVTec AD, plus recall at a chosen threshold on QS frames, with a confidence bound.
5. I train a detector on a dataset I collected and labeled, and report mAP plus my own error analysis.
6. I run a model on CPU through ONNX or OpenVINO at a measured FPS, on a live stream with tracking.

## The levels

| # | Folder | What I learn and rebuild | Milestones | QS module | Read first |
|---|---|---|---|---|---|
| 1 | `color` | Images as arrays, color spaces, histograms, thresholding. Rebuild the warmth verdict (median R−B inside the rim) on QS frames. | M1 | `inspector/cup.py`, warmth in `inspector/line.py` | Nayar: Image Formation, Image Sensing |
| 2 | `rims` | Filtering, gradients, Canny, contours, ellipse fitting, Hough. Rebuild the rim finder and measure its hit rate on sharp vs blurred frames. | M1, M2 | `inspector/cup.py` (`find_rims`, `find_cup`) | Nayar: Image Processing I, Edge Detection, Boundary Detection |
| 3 | `geometry` | Binary images, moments, area, axis ratio, solidity, camera calibration. Rebuild the geometry check, then calibrate my C920 with a checkerboard and measure in mm. | M1, M3 | `inspector/localize.py`, `inspector/geometry.py`, `inspector/tolerances.py` | Nayar: Binary Images, Camera Calibration |
| 4 | `patchcore` | Pretrained CNN features, patch embeddings, nearest-neighbour memory bank, coreset. Rebuild PatchCore: MVTec AD first, then QS frames. | M4 | `inspector/patchcore.py`, `inspector/appearance.py`, `inspector/heatmap.py` | PatchCore paper; CS231n lectures 1–9 |
| 5 | `evaluate` | ROC, AUROC, precision/recall, choosing a threshold, binomial confidence bounds, what "95%" means in a contract. Rebuild the threshold choice and the bound. | M4 | `eval/threshold.py`, `eval/stats.py`, `eval/scoring.py`, `cmd/evaluate.py` | Google ML Crash Course: Classification |
| 6 | `detector` | Collecting and labeling a dataset, splits without leakage, training a YOLO detector, mAP, error analysis. | M5 | `cmd/label.py`, `eval/line_split.py`, `cmd/train.py` | Johnson EECS 498: detection lectures; Ultralytics docs |
| 7 | `edge` | Export to ONNX, OpenVINO on Intel CPU, quantization, measuring latency and FPS honestly. QS has no export yet, so this level becomes the plan for QS's box. | M6 | `cmd/latency.py` (and the QS box when it exists) | OpenVINO notebooks; ONNX Runtime docs |
| 8 | `linestream` | Camera stream → frame sampling → inference → multi-frame verdict → tracking → alarms. Rebuild a mini station that replays a line video. | M6 | `pipeline.py`, `cup_trigger.py`, `inspector/line.py`, `cmd/line_alarms.py` | Nayar: Object Tracking; ByteTrack paper; supervision docs |

**Marking/OCR** becomes its own level when QS builds the marking station. It goes in the right place in this table then.

## Rules for every level

1. **A one-page design note first** (`cv-lab/<folder>/design.md`): what I'm rebuilding, how I'll measure it, and the data. The mentor reviews it before any code.
2. **Slice only on the day I start.** Later levels stay at table level until then. Every slice: branch → PR → review → merge.
3. **6-week cap.** At the cap I ship what works, write a "what's missing" section and move on.
4. **Definition of done:**
   - the explain note for the QS module, in my words
   - the rebuild, with tests (`pytest`), green in CI
   - **one measured number**, compared with QS's version on the same images
   - a short "where this breaks on the real line" section
5. **I type all the CV code in `cv-lab`.** AI explains and reviews, under `MENTOR.md`. AI keeps writing QS.
6. **Mentor fade:** levels 1–2 walked step by step, 3–5 reviewed, 6–8 reviewed afterwards.
7. **QS images stay private.** `cv-lab` commits code, numbers and synthetic or public images (MVTec AD) only, never factory frames (QS rule: no image leaves the building).

## The QS learning rule

From whichever comes first, **QS's line gate passing** (0 misses in ≥300 empty cups at home, advisory at the customer) or **2027-01-15**: before any QS vision PR merges, I write 3–5 lines saying what it does, why this method, and what would break it. Until then QS runs at full AI speed and I learn from it through this ladder.

## Milestones proven

---

## Rung 1 — `color` (status: not started)

**Design doc:** *(I write `cv-lab/color/design.md` at the first sitting, walked through by the mentor, before slice 1.)*

**Slices:**
- [ ] 1. **Walking skeleton:** an empty `cv-lab` repo, then a script that loads one QS frame, prints its shape and dtype, and saves its B, G, R channels as three images.
- [ ] 2. **Color spaces:** convert to HSV and Lab, plot the histograms of a full cup and an empty cup side by side, and write what separates them.
- [ ] 3. **Explain:** read QS's warmth verdict and write `notes/1-color.md`.
- [ ] 4. **Rebuild:** median R−B inside a given rim mask, over ≥3 frames, with table tests on synthetic images.
- [ ] 5. **Measure:** run mine and QS's on the same labeled frames and report agreement, plus a "where it breaks" note (glare, starch, white balance).
