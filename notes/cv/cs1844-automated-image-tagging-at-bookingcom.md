---
id: cs1844
title: Automated Image Tagging at Booking.com
company: Booking.com
primary_category: cv
sub_category: image-classification
year: 2017
source_url: https://booking.ai/automated-image-tagging-at-booking-com-7704f27dcc8b
tags: [image-tagging, cnn, inception-v3, personalization, image-classification]
---

# Automated Image Tagging at Booking.com
**Booking.com** · 2017 · [source](https://booking.ai/automated-image-tagging-at-booking-com-7704f27dcc8b)

## Problem
Booking.com hosts over 150 million hotel and user-generated images with no systematic semantic labels, making it impossible to automatically select the most relevant image for a given user or context. Manual tagging at that scale was infeasible, so an automated system was needed to tag images and enable context-aware image selection.

## Approach / System design
The team trained deep convolutional neural networks to classify images into semantic categories relevant to accommodation search. Multiple CNN architectures were evaluated and compared, including Inception-v3, with models trained on the internal image catalog. The output tags are used downstream to serve the contextually most appropriate image to each user based on their browsing context.

## Key decisions
Evaluating multiple CNN architectures (including Inception-v3) allowed the team to pick the best accuracy-efficiency tradeoff for their label taxonomy. The tag outputs were designed to feed directly into a personalization layer, so tag granularity was chosen to support user-level image selection rather than just generic categorization.

## Stack
Deep CNNs including Inception-v3. Specific training infrastructure and serving details are not covered in the source.

## Results
Not covered in the source.

## Takeaways
Automated image tagging at scale enables downstream personalization experiences that are otherwise impossible with unstructured image catalogs. Evaluating multiple architectures during the model selection phase helps avoid premature commitment to a single approach when the label space and data distribution are novel.
