# Scene Understanding via Semantic Segmentation in Autonomous Driving

**Master of Science in Computer Science | CSC-590 | California State University, Dominguez Hills**  
**Author:** Durgaprasad Bollapally  
**Project:** Comparative implementation of four semantic segmentation models on urban-driving imagery

## Overview

Semantic segmentation assigns a class to each image pixel, supporting scene understanding in autonomous-driving research. This project explores the training, visualization, and preliminary comparison of four model architectures using Cityscapes-derived image/mask pairs.

> **Research transparency:** This is a course research project and **not a validated autonomous-driving safety system**. The notebook uses a simplified mask-label transformation (`mask % NUM_CLASSES`) rather than the official Cityscapes train-ID mapping. Consequently, the recorded accuracy/IoU figures should **not** be interpreted as standard Cityscapes benchmark results. The original notebook is preserved for reproducibility and inspection.

## Models explored

| Model | Implementation in notebook | Role |
|---|---|---|
| U-Net | Custom encoder-decoder | Segmentation baseline |
| SegNet | Custom encoder-decoder | Alternative baseline |
| MobileNetV3 LRASPP | TorchVision `lraspp_mobilenet_v3_large(weights=None)` | Lightweight architecture comparison |
| SimpleFRRN | Simplified full-resolution residual design | Spatial-detail experiment |

**Note:** MobileNet is initialized with `weights=None`; it is **not** described here as ImageNet-pretrained. SimpleFRRN is a simplified implementation, not a claim of reproducing the full published FRRN.

## Repository contents

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── semantic_segmentation.ipynb
├── models/
│   ├── unet_checkpoint.pth
│   ├── segnet_checkpoint.pth
│   ├── mobilenet_checkpoint.pth
│   └── frrn_checkpoint.pth
├── outputs/
│   └── final_output.mp4
├── data/
│   └── README.md
└── docs/
    └── EVALUATION_NOTES.md
```

## Quick start

1. Install Python 3.10+ and create a virtual environment.
2. Install dependencies: `pip install -r requirements.txt`.
3. Obtain the Cityscapes dataset through the authorized source and arrange the image and label folders as described in [`data/README.md`](data/README.md).
4. Open [`notebooks/semantic_segmentation.ipynb`](notebooks/semantic_segmentation.ipynb) in Jupyter or Google Colab.
5. **Before running**, change the Colab-specific dataset paths (`/content/dataset/dataset/...`) to your own locations. The notebook is a preserved research artifact, **not** a turnkey one-click training script; execute and review cells in order.

The original run used **256 × 512** input resolution, **34 configured classes**, **batch size 2**, **Adam learning rate 0.001**, and **CrossEntropyLoss**. U-Net and SegNet were trained for 5 epochs; MobileNet and SimpleFRRN for 10 epochs. These short training runs are exploratory.

## Demonstration

The saved demonstration is [`outputs/final_output.mp4`](outputs/final_output.mp4). It shows the notebook's video-style segmentation output; it is **not** a real-time vehicle deployment demonstration.

## Evaluation and limitations

The notebook includes pixel accuracy, IoU, FPS and parameter-count calculations. See [evaluation notes](docs/EVALUATION_NOTES.md) for why these preliminary measurements need validation before scientific comparison. In particular, an evaluation cell appears to reuse the `model` variable after it was assigned to the FRRN model, so a U-Net-labelled result may not actually evaluate U-Net.

## Future improvements

- Implement official Cityscapes label-ID to train-ID mapping and correct ignored classes.
- Re-run all models using identical, documented evaluation splits and correctly selected model objects.
- Synchronize CUDA timing and measure warm-up, latency, throughput, and hardware details.
- Add per-class IoU, mean IoU, confusion matrices, qualitative examples and fixed random seeds.
- Convert notebook code into modular training/evaluation scripts with repeatable configurations.

## Academic context

Prepared as a CSUDH CSC-590 master's project. The code, checkpoint files, and video in this repository are project artifacts. For reproducible benchmarks, follow the limitations above and re-evaluate before citing performance figures.

## Dataset attribution

Cityscapes dataset: [cityscapes-dataset.com](https://www.cityscapes-dataset.com/). Dataset files are not redistributed here; follow its license and access requirements.
