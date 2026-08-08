---
id: cs1837
title: Hardware Accelerated Inference on Edge Devices at Samsara
company: Samsara
primary_category: cv
sub_category: object-detection
year: 2021
source_url: https://medium.com/samsara-engineering/hardware-accelerated-inference-on-edge-devices-at-samsara-1bad5f406128
tags: [edge-ml, dashcam, mobilenet, quantization, on-device-inference]
---

# Hardware Accelerated Inference on Edge Devices at Samsara
**Samsara** · 2021 · [source](https://medium.com/samsara-engineering/hardware-accelerated-inference-on-edge-devices-at-samsara-1bad5f406128)

## Problem
Samsara's dashcam fleet needs to detect driving hazards — such as forward collisions and distracted driving — in real time directly on the camera device. The hardware in these cameras is roughly smartphone-class, meaning it lacks the compute budget of a data-center GPU, yet latency requirements are strict enough that cloud offloading is not viable.

## Approach / System design
Samsara adopted lightweight mobile neural network architectures (SqueezeNet and MobileNet variants) designed for constrained devices. Models are quantized to reduce arithmetic precision and memory bandwidth. Graph surgery techniques are applied to restructure the computation graph for better hardware fit, and inference is delegated to specialized on-device accelerators — DSPs and ISPs — rather than the CPU or GPU alone.

## Key decisions
Choosing architectures that were designed for mobile deployment from the start (SqueezeNet, MobileNet) rather than attempting to compress large server-class models was a foundational decision. Quantization and graph surgery are applied as complementary optimizations: quantization cuts memory and compute costs, while graph surgery ensures operations map efficiently to the available hardware accelerators.

## Stack
SqueezeNet, MobileNet, on-device quantization, DSP/ISP hardware delegation, dashcam edge hardware.

## Results
The pipeline achieves low-latency real-time hazard detection across hundreds of thousands of deployed vehicles without any cloud round-trip for inference.

## Takeaways
Running meaningful CV models on constrained edge hardware requires a combination of architecture selection, quantization, and hardware-aware graph optimization working together. No single technique is sufficient on its own; the full stack must be co-designed around the target device's accelerator capabilities.
