---
id: cs1842
title: Using On-Device Machine Learning to Suggest Presets for Images in VSCO
company: VSCO
primary_category: cv
sub_category: image-classification
year: 2019
source_url: https://eng.vsco.co/on-device-ml/
tags: [on-device-ml, squeezenet, tensorflow, image-classification, preset-suggestion]
---

# Using On-Device Machine Learning to Suggest Presets for Images in VSCO
**VSCO** · 2019 · [source](https://eng.vsco.co/on-device-ml/)

## Problem
VSCO users must browse a large library of photo filter presets to find one that suits the image they are editing. The manual search is time-consuming, and a good match depends heavily on the content and lighting of the specific photo. VSCO wanted to surface relevant presets automatically without sending user photos to a server.

## Approach / System design
VSCO trained a SqueezeNet convolutional neural network in TensorFlow to classify the content and visual characteristics of the photo being edited. The classifier runs entirely on the user's device and outputs a category label (such as landscape, portrait, or low-light scene). Based on that label, the app surfaces a curated shortlist of presets likely to complement the image under the "For This Photo" feature.

## Key decisions
Running the model on-device was a deliberate privacy choice: photos never leave the device for classification purposes. SqueezeNet was selected because its compact architecture fits comfortably within the memory and compute budget of mobile hardware. TensorFlow's mobile runtime (TensorFlow Lite's predecessor) enabled deployment on both iOS and Android.

## Stack
SqueezeNet, TensorFlow (mobile), on-device inference, iOS and Android deployment.

## Results
Not covered in the source.

## Takeaways
On-device inference enables ML-powered personalization without compromising user privacy, and lightweight architectures like SqueezeNet make this practical on consumer mobile hardware. Framing the task as image classification rather than end-to-end preset ranking keeps the on-device model tractable while still delivering useful recommendations.
