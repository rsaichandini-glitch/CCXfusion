# CC-XFusion: Clinical Dashboard Prototype

**Clinically Explainable Multimodal AI with Cross-Modal Consistency for Early Colorectal Cancer Diagnosis**

A clickable, front-end prototype of a clinician-facing decision-support dashboard. It accompanies the research paper on **CC-XFusion** (Consistency-Constrained Explainable Fusion).

> **Important:** This is a demonstration prototype. It does **not** run the trained model. All scores, heatmaps, gene rankings and patient records are illustrative demonstration data. It is not a medical device and must not be used for diagnosis.

## About the project

Colorectal cancer (CRC) diagnosis relies on two complementary sources: tissue morphology (histopathology) and molecular profiles (gene expression). Many multimodal models simply concatenate the two, which can let one modality dominate and hide conflicts between them.

CC-XFusion addresses this by:

1. Encoding each modality separately (ResNet-50 with MIL attention for images, MLP for selected genes).
2. Enforcing **cross-modal consistency** between the two representations.
3. Combining them with **gated attention fusion**.
4. Producing **explainable output**: attention maps, gene importance and uncertainty.

The system supports clinicians. It does not replace professional diagnosis.

## Prototype screens

| # | Screen | What it shows |
|---|--------|---------------|
| 1 | Login | Clinician sign-in |
| 2 | Dashboard | Summary cards and recent analyses table |
| 3 | New Analysis | Patient details; upload a histopathology image and a gene-expression file (or use demo data) |
| 4 | AI Processing | Animated dual-stream pipeline with modality contributions |
| 5 | Clinical Result | High-probability result, confidence and consistency |
| 6 | Visual Explanation | Original / Attention Map / Overlay views and important tissue regions |
| 7 | Molecular Explanation | Gene-importance chart (TP53, KRAS, APC, BRAF, MLH1) |
| 8 | Cross-Modal Consistency | Evidence panels, consistency check, and a low-consistency conflict state |
| 9 | Confidence & Uncertainty | Gauge and review recommendation |
| 10 | Explainable Summary | Reasoning chain and four evidence cards |
| 11 | Clinical Report | Printable report |
| 12 | Model Insights | AUC 0.962, accuracy 0.92, F1 0.93 and baseline comparison |

## How to run

The prototype is a single file with no build step and no dependencies to install.

1. Download `index.html`.
2. Open it in a modern browser (Chrome, Edge, Firefox or Safari).
3. Click **Sign in**, then follow the flow: Dashboard, New Analysis, Run CC-XFusion Analysis, and use the Next / Back bar at the bottom.

It also works when hosted as a static site (GitHub Pages, Netlify and similar).

### Using your own files

On **New Analysis** you can upload your own image (any image format) and a gene-expression file (CSV, TSV or TXT), or click **Use demo slide / Use demo file**. Files are read in your browser only and are never sent anywhere. The gene count shown comes from the number of rows in your file.

## Research results (from the paper)

Evaluated on TCGA-COAD with five-fold, patient-level cross-validation.

| Method | Modality | AUC | Accuracy | F1 |
|--------|----------|-----|----------|----|
| CNN-MIL | Histopathology | 0.842 | 0.79 | 0.81 |
| MLP | Gene expression | 0.885 | 0.83 | 0.84 |
| Concatenation Fusion | Image + Gene | 0.910 | 0.86 | 0.88 |
| MCAT | Image + Gene | 0.935 | 0.89 | 0.90 |
| **CC-XFusion (proposed)** | Image + Gene | **0.962** | **0.92** | **0.93** |

These are research results, not live clinical performance.

## Implementation details (from the paper)

| Component | Configuration |
|-----------|---------------|
| Image encoder | ResNet-50 (ImageNet pretrained) |
| Patch size / magnification | 256 × 256 at 20× |
| Patch aggregation | Multiple Instance Learning (MIL) attention |
| Gene encoder | Multi-Layer Perceptron (MLP) |
| Fusion | Gated Attention Fusion |
| Optimizer | AdamW, learning rate 1 × 10⁻⁴, batch size 16 |
| Loss | Cross-entropy + consistency constraint |

## Limitations of this prototype

- No model inference: outputs are fixed demonstration values, whatever you upload.
- The tissue image and heatmap are illustrative. A heatmap shown on an uploaded image is not a real model output.
- Patients and Analysis History reuse the dashboard table.
- Download Report is simulated; Print Report uses the browser print dialog.

## Tech

Plain HTML, CSS and JavaScript in a single file, with inline SVG for charts. Supports light and dark mode and is designed for desktop screens.

## Disclaimer

AI-generated results are intended for clinical decision support and do not replace professional diagnosis. This repository is for academic and research demonstration only.
