# Evaluation notes and scientific limitations

This document separates **observations recorded in the preserved notebook** from **validated benchmark results**. The latter have not been established.

## Recorded experimental setup

- Architectures: custom U-Net, custom SegNet, TorchVision MobileNetV3 LRASPP, simplified FRRN.
- Input resolution: 256 × 512; configured classes: 34; batch size: 2.
- Adam optimizer, learning rate 0.001; cross-entropy loss.
- Short exploratory training runs: U-Net and SegNet 5 epochs; MobileNet and SimpleFRRN 10 epochs.

## Important caveats

1. **Label handling:** `mask % NUM_CLASSES` is not an official Cityscapes semantic class mapping. Pixel accuracy and IoU are not comparable with published Cityscapes benchmark metrics.
2. **Model selection:** A later notebook cell assigns `model = frrn_model` for video output; a subsequent result labelled U-Net appears to evaluate the `model` variable. Verify the actual model instance before reporting results.
3. **Timing:** Simple elapsed-time timing without explicit CUDA synchronization may misstate GPU inference latency and FPS.
4. **Weights:** `weights=None` is used for MobileNetV3 LRASPP, so do not claim pretrained weights.
5. **Scope:** The notebook and video demonstrate an educational pipeline, not a production autonomous-driving system.

## Recommended re-evaluation protocol

Use a fixed validation split; official Cityscapes train IDs and ignored-label handling; explicitly load each model's own checkpoint; `model.eval()` and `torch.no_grad()`; warm up GPU; synchronize CUDA before and after timing; report pixel accuracy, per-class IoU and mean IoU, hardware, and qualitative samples.
