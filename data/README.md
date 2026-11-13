# Dataset setup

The original notebook expects image and mask directories like:

```text
dataset/dataset/train/img/
dataset/dataset/train/label/
dataset/dataset/val/img/
dataset/dataset/val/label/
```

The notebook uses absolute Google Colab paths beginning `/content/dataset/dataset/`. Update these paths before running on another machine.

The original local dataset archive is intentionally **not included** in this public repository because it is large and dataset redistribution rights must be respected. Obtain Cityscapes data from the [official website](https://www.cityscapes-dataset.com/) and verify that the image/mask layout and labels match the notebook assumptions.

**Caution:** The notebook's `mask % NUM_CLASSES` transformation is not official Cityscapes train-ID preprocessing. Correct the label mapping before claiming standard benchmark accuracy or IoU.
