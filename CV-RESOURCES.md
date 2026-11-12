# CV resources

The study library for `CV-LADDER.md`. Everything here is free. Every link was checked on 2026-11-12.

**How to use it:** don't read this top to bottom. Each level has its picks below. The rule from `PLAN.md` still holds: one book at a time, only the chapters the level needs, and a ≤10-min lesson from the mentor when I'm stuck on my own code.

## The core library

### Video courses (watch these)

| Course | What it is | Link |
|---|---|---|
| **First Principles of Computer Vision** (Shree Nayar, Columbia) | The best free classical-CV course. Short videos (5–15 min) from image formation to tracking. **My main classical-CV course.** | [site with modules](https://fpcv.cs.columbia.edu/) · [YouTube channel](https://www.youtube.com/@firstprinciplesofcomputerv3258) |
| **CS231n** (Stanford) | Deep learning for vision: CNNs, training, detection. Course notes are excellent. | [course site + notes](https://cs231n.stanford.edu/) · [2017 lectures on YouTube](https://www.youtube.com/playlist?list=PL3FW7Lu3i5JvHM8ljYj-zLfQRF3EO8sYv) |
| **Deep Learning for Computer Vision** (Justin Johnson, Michigan EECS 498) | A newer CS231n, by one of its authors. Clearer on detection and segmentation. | [YouTube playlist (Michigan Online)](https://www.youtube.com/playlist?list=PL5-TkQAfAZFbzxjBHtzdVCWE0Zbhomg7r) |
| **Neural Networks: Zero to Hero** (Andrej Karpathy) | Build backprop and networks from scratch in Python. The best way to really get *how* training works. | [karpathy.ai/zero-to-hero](https://karpathy.ai/zero-to-hero.html) |
| **Practical Deep Learning for Coders** (fast.ai) | Top-down: train working models in lesson 1, theory later. Good when I need results fast. | [course.fast.ai](https://course.fast.ai/) |
| **Cyrill Stachniss** (Bonn) | Photogrammetry and camera geometry: calibration, projection, the math behind measuring in mm. | [YouTube channel](https://www.youtube.com/@CyrillStachniss) |
| **Deep Learning School** (МФТИ, in Russian) | Free Russian-language DL course with CV parts, for when English lectures are tiring. | [dls.samcs.ru](https://dls.samcs.ru/) |
| **3Blue1Brown: Essence of Linear Algebra** | Vectors, matrices and transforms as pictures. Watch as needed for levels 3–4. | [3blue1brown.com](https://www.3blue1brown.com/topics/linear-algebra) |

### Books (read chapters, not books)

| Book | Use it for | Link |
|---|---|---|
| **Szeliski, *Computer Vision: Algorithms and Applications*, 2nd ed.** | The reference textbook, free PDF. Read the chapter a level needs: image formation, image processing, feature detection (edges, lines), deep learning, recognition. | [szeliski.org/Book](https://szeliski.org/Book/) |
| **Dive into Deep Learning** (d2l.ai) | Runnable PyTorch book. Chapters on CNNs, modern CNNs (ResNet), computer vision and optimization. | [d2l.ai](https://d2l.ai/) |

### Hands-on tutorials and docs

| Source | Use it for | Link |
|---|---|---|
| **OpenCV-Python tutorials** | The working API for every classical level. | [tutorial root](https://docs.opencv.org/4.x/d6/d00/tutorial_py_root.html) |
| **scikit-image gallery** | Clear examples of segmentation, morphology, region properties. | [examples](https://scikit-image.org/docs/stable/auto_examples/) |
| **PyTorch tutorials** | Datasets, models, training loops. | [pytorch.org/tutorials](https://pytorch.org/tutorials/) |
| **Kaggle Learn: Computer Vision** | A short free hands-on course (CNNs, transfer learning) in notebooks. | [kaggle.com/learn/computer-vision](https://www.kaggle.com/learn/computer-vision) |
| **Google ML Crash Course: Classification** | Thresholds, ROC, AUC, precision and recall, with interactive widgets. | [module](https://developers.google.com/machine-learning/crash-course/classification) |
| **Edmund Optics imaging application notes** | Industrial imaging: lenses, lighting, resolution, field of view. This is the "machine vision" side that CV courses skip and the factory needs. | [application notes](https://www.edmundoptics.com/knowledge-center/application-notes/imaging/) |

### Papers (industrial anomaly detection and tracking)

| Paper | Why | Link |
|---|---|---|
| **PatchCore**: *Towards Total Recall in Industrial Anomaly Detection* (Roth et al., 2021) | The method QS uses for the appearance station. | [arXiv 2106.08265](https://arxiv.org/abs/2106.08265) |
| **SPADE**: *Sub-Image Anomaly Detection with Deep Pyramid Correspondences* (2020) | PatchCore's ancestor: nearest neighbours on pretrained features. Read first, it's simpler. | [arXiv 2005.02357](https://arxiv.org/abs/2005.02357) |
| **PaDiM** (2020) | The alternative: a Gaussian per patch position instead of a memory bank. Good for the "why this method" note. | [arXiv 2011.08785](https://arxiv.org/abs/2011.08785) |
| **ByteTrack** (2021) | Simple, strong multi-object tracking. | [arXiv 2110.06864](https://arxiv.org/abs/2110.06864) |

### Codebases and tools

| Repo / tool | Why | Link |
|---|---|---|
| **anomalib** | The standard anomaly-detection library (PatchCore, PaDiM and others). Read its PatchCore to compare with mine. | [open-edge-platform/anomalib](https://github.com/open-edge-platform/anomalib) |
| **patchcore-inspection** | The paper authors' own PatchCore code. | [amazon-science/patchcore-inspection](https://github.com/amazon-science/patchcore-inspection) |
| **MVTec AD** | The public industrial-defect dataset (15 categories). Free for non-commercial use. | [mvtec.com](https://www.mvtec.com/company/research/datasets/mvtec-ad) |
| **Ultralytics** | YOLO training and export, level 6. | [docs.ultralytics.com](https://docs.ultralytics.com/) |
| **Label Studio** / **CVAT** | Labeling tools for level 6, self-hosted, so factory images stay local. | [labelstud.io](https://labelstud.io/) · [cvat-ai/cvat](https://github.com/cvat-ai/cvat) |
| **OpenVINO** + notebooks | Running models fast on Intel CPUs (the QS box). | [docs](https://docs.openvino.ai/) · [notebooks](https://github.com/openvinotoolkit/openvino_notebooks) |
| **ONNX Runtime** | The portable way to run an exported model. | [docs](https://onnxruntime.ai/docs/) |
| **supervision** (Roboflow) | Zones, ByteTrack and annotators for video pipelines, level 8. | [docs](https://supervision.roboflow.com/latest/) |

## Picks per level

Watch and read these, in this order, when the level starts. "Nayar: X" means module X on the [FPCV site](https://fpcv.cs.columbia.edu/).

### Level 1 — `color`
- **Watch:** Nayar: *Image Formation* (pinhole, lenses) and *Image Sensing* (sensors, *Sensing Color*, camera response). Then *Radiometry and Reflectance* for the glare on steel.
- **Read:** Szeliski, the image formation chapter (photometric image formation, the digital camera).
- **Do:** OpenCV tutorial [Changing Colorspaces](https://docs.opencv.org/4.x/df/d9d/tutorial_py_colorspaces.html), then the histograms and thresholding tutorials from the root page.

### Level 2 — `rims`
- **Watch:** Nayar: *Image Processing I* (convolution, linear and non-linear filters), *Edge Detection* (gradients, Laplacian, Canny), *Boundary Detection* (fitting lines and curves, Hough transform).
- **Read:** Szeliski, the image processing chapter (linear filtering), and the feature detection chapter's sections on edges and lines.
- **Do:** OpenCV [Canny](https://docs.opencv.org/4.x/da/d22/tutorial_py_canny.html), [Contours](https://docs.opencv.org/4.x/d3/d05/tutorial_py_table_of_contents_contours.html) (including `fitEllipse`), [Hough circles](https://docs.opencv.org/4.x/da/d53/tutorial_py_houghcircles.html).

### Level 3 — `geometry`
- **Watch:** Nayar: *Binary Images* (geometric properties, segmenting) and *Camera Calibration*. Then Stachniss's camera-calibration lectures if the math is fuzzy.
- **Read:** Szeliski, the image formation chapter's geometric part (3D to 2D projection, lens distortion).
- **Do:** OpenCV [Camera Calibration](https://docs.opencv.org/4.x/dc/dbb/tutorial_py_calibration.html) with a printed checkerboard and my C920; scikit-image `regionprops` from the gallery.
- **Machine vision:** Edmund Optics notes on resolution and field of view. They answer "how many pixels per mm do we need".

### Level 4 — `patchcore`
- **Watch:** CS231n 2017 lectures 1–9, or the first third of Johnson's EECS 498 (image classification up to CNN architectures). If backprop feels like magic, first do Karpathy's first two videos.
- **Read:** d2l.ai chapters on CNNs and modern CNNs (ResNet). Then SPADE → PaDiM → **PatchCore**, in that order.
- **Do:** download MVTec AD. Run anomalib's PatchCore once as the reference number. Then write mine (pretrained WideResNet features, memory bank, kNN, coreset) and compare.

### Level 5 — `evaluate`
- **Do first:** Google ML Crash Course: *Classification* (thresholds, confusion matrix, ROC and AUC).
- **Read:** CS231n notes on evaluation; the PatchCore paper's evaluation section (image vs pixel AUROC).
- **Then:** read QS's `eval/stats.py` binomial bounds and work out by hand what "95% with 300 units" really promises.

### Level 6 — `detector`
- **Watch:** Johnson EECS 498, the object detection lectures (single-stage, two-stage, mAP).
- **Read:** Ultralytics docs: train, val, predict, the dataset format.
- **Do:** label in Label Studio or CVAT locally, split by session (not by frame) so the test set doesn't leak, train, then an error analysis by hand on the misses.
- **Alternative if stuck:** fast.ai lessons 1–3 for the "just make training work" path.

### Level 7 — `edge`
- **Do:** OpenVINO notebooks: model conversion, the benchmark tool, INT8 quantization. ONNX Runtime docs: export from PyTorch, then run.
- **Read:** QS's `cmd/latency.py` for how we measure latency today. Then measure mine the same way: warm-up runs, p50/p99, not a single timing.

### Level 8 — `linestream`
- **Watch:** Nayar: *Object Tracking*.
- **Read:** the ByteTrack paper; supervision docs (ByteTrack, zones).
- **Do:** replay a recorded line video through my mini station: sample frames, find the cup, verdict over ≥3 frames, count units, raise an alarm. Compare its counts with QS's on the same video.

## Codebase reading (30 min per level, guided)

The QS module in each level's table is the main reading. For a second, outside view:
- Levels 1–3: OpenCV's own Python samples in the [opencv repo](https://github.com/opencv/opencv) (`samples/python`).
- Level 4: anomalib's PatchCore model folder vs `amazon-science/patchcore-inspection`.
- Level 8: supervision's ByteTrack implementation.
