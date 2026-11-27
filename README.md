# Echo-EF: Verified Evaluation and Reliability Analysis of Video Deep Learning for Ejection Fraction Estimation

**Academic Project Submission — Bennett University (SCSET)**  
- **Team No. 15:** Aqdas Yunus (`E23CSEU2107`) & Anisha Kumari (`E23CSEU2327`)  
- **Project Mentor:** Mr. Sarthak Mishra  
- **Based on Research Study:** *Echo-EF: Verified Evaluation and Reliability Analysis of Video Deep Learning for Ejection Fraction Estimation on EchoNet-Dynamic* (Dr. Priyanka Gupta, Manohith Sai, Rudra Kumar, Abhishek)

> **Disclaimer:** Research prototype only. Not a clinically validated diagnostic system. Not intended for medical diagnosis, clinical decision-making, or patient triage.

---

## Live Demo Walkthrough

Watch the walkthrough of the local Gradio application (`Analyze`, `Model influence`, `Model results`, and `Research` tabs):

<video src="Demo/Demo_video.mp4" controls="controls" style="max-width: 100%;">
  Your browser does not support the video tag. View the demo directly at <a href="Demo/Demo_video.mp4">Demo/Demo_video.mp4</a>.
</video>

*(If GitHub does not render inline playback on your browser, click **[Demo/Demo_video.mp4](Demo/Demo_video.mp4)** and select **View raw** to watch or download.)*

---

## Project Submission Documents

All project documentation and presentation slides are located inside **[`submission_docs/`](submission_docs/)**:
- **Project Report:** `submission_docs/Echo-EF_Project_Report.docx`
- **Presentation Slides:** `submission_docs/` (`.pptx`)

---

## Overview

**Echo-EF** estimates left ventricular **Ejection Fraction (EF)**, **End-Diastolic Volume (EDV)**, and **End-Systolic Volume (ESV)** from apical four-chamber echocardiogram videos in the **EchoNet-Dynamic** dataset (10,030 videos). Rather than reporting only a single headline error, this project evaluates **where the model fails across EF subgroups**, tests **uncertainty quantification methods** for selective deferral, and audits **Grad-CAM visual explanations**:

- **Main Predictor:** Multitask **R3D-18** (3D ResNet-18 pretrained on Kinetics-400) predicting EF, EDV, and ESV from 32-frame clips (stride 2, `112 × 112`), deriving three clinical reporting groups: **Reduced (`< 40%`)**, **Mildly reduced (`40% to < 50%`)**, and **Normal (`≥ 50%`)**.
- **Supporting Research:** Pre-registered 3-seed auxiliary ordinal head experiment, 5-arm video augmentation study (`MixUp`, `CutMix`, `Temporal`, `Geometric`, `None`), `Video Swin-T` & 2D `Frame-CNN` comparisons, head-to-head uncertainty evaluation (`MC Dropout`, `Heteroscedastic`, `Residual Uncertainty`), and `Grad-CAM` masking & cardiac-phase alignment validation.

---

## Repository Structure

```text
Echo-EF/
├── Demo/
│   └── Demo_video.mp4           # Local Gradio web interface walkthrough
├── submission_docs/             # Project report (.docx) and presentation (.pptx)
├── app/
│   └── app.py                   # Local Gradio application (4-tab interface)
├── src/
│   ├── data/                    # Dataset loading, caching, and 32-frame clip preparation
│   ├── models/                  # Multitask R3D-18, Video Swin-T, and Frame-CNN models
│   ├── train/                   # Training pipeline (warmup + FP32 fine-tuning)
│   ├── eval/                    # Metrics, per-group confusion matrices, bootstrap & uncertainty
│   ├── infer/                   # Single-video inference & SHA-256 identity verification
│   └── xai/                     # Grad-CAM attribution & masking/alignment validation
├── configs/
│   └── base.yaml                # Shared dataset paths and training hyperparameters
├── docs/                        # Pre-registration records and graph guide
├── scripts/                     # Dataset cache builder and evaluation scripts
├── tests/                       # Unit and pipeline verification tests
├── analyze_main_reliability.py  # Subgroup error and reliability analysis script
├── group_correctness_estimate.json # Experimental group-correctness estimator parameters
└── requirements.txt             # Python dependencies