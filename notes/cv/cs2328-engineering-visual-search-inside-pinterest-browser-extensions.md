---
id: cs2328
title: Engineering Visual Search Inside Pinterest Browser Extensions
company: Pinterest
primary_category: cv
sub_category: object-detection
year: 2021
source_url: https://medium.com/pinterest-engineering/engineering-visual-search-inside-pinterest-browser-extensions-90e7ed9d2b14
tags: [visual-search, browser-extension, object-detection, embeddings, image-cropping]
---

# Engineering Visual Search Inside Pinterest Browser Extensions
**Pinterest** · 2021 · [source](https://medium.com/pinterest-engineering/engineering-visual-search-inside-pinterest-browser-extensions-90e7ed9d2b14)

## Problem
Pinterest's visual search technology (powering Lens, Shop the Look, and Instant Ideas over 100B saved ideas for 150M users) only worked inside Pinterest's own surfaces. The team wanted to let people visually search any image on the web — including non-static content like videos and GIFs — directly from the browser, without leaving the page they're on.

## Approach / System design
Visual search was built into the Pinterest browser button for Chrome:
- **Two entry points**: hovering over any image and clicking a magnifying-glass icon searches that image's URL; right-clicking the page uses Chrome's `captureVisibleTab` API to screenshot the whole visible page, which makes videos and GIFs searchable as static frames.
- **Extension architecture**: `captureVisibleTab` only works in background scripts, so the screenshot data URI is sent via Chrome's message-passing API to the injected content script, which resizes it and renders it in a visual search overlay on the page.
- **Cropping selector UI**: the image is resized to fit the page (max 50% of available width), drawn as the background of an HTML element, and overlaid with a transparent canvas holding a movable/resizable crop box. On open, ~90% of the image is selected with an inward animation to teach the interaction. The original image is drawn into a hidden canvas and converted to a data:URI via `canvas.context.getImageData`, resized to the minimum size the visual models need to cut latency.
- **Search flow**: the initial selection is searched immediately on load; crop coordinates (top/left/height/width) plus the image blob go to the Pinterest API via XMLHttpRequest from the background script. Results return as Pin objects rendered in a familiar Pinterest grid, which can be saved or re-searched in place.
- **API layer**: the image is uploaded to a temporary S3 store and sent to the visual search service. These were originally sequential steps; parallelizing them cut latency substantially. The API returns a link to the stored image so subsequent crop searches resend only the link plus new coordinates instead of re-uploading raw image data.

## Key decisions
- Screenshot-based capture (`captureVisibleTab`) instead of image-URL-only search, to cover dynamic content.
- Client-side downscaling to the minimum resolution the models require, trading pixels for latency.
- Temporary S3 storage with link-based re-search to avoid repeatedly shipping raw image bytes on crop refinements.
- Parallelizing the S3 upload and the visual search call, which had been needlessly serialized.
- Always searching the default 90% crop on load so users see results (and annotations) before interacting.

## Stack
Chrome extension APIs (`captureVisibleTab`, message passing, background/content scripts), HTML canvas, data:URI/blob handling, XMLHttpRequest, Amazon S3 (temporary image store), Pinterest visual search service and visual models, Pin-object result rendering.

## Results
Rolled out globally to Pinterest browser-button users on Chrome. No quantitative engagement metrics are given; the latency win from parallelizing upload and search is described qualitatively. Roadmap items included bringing real-time object detection to the extension, expanding results beyond visual similarity (e.g., recipes and how-tos for a detected avocado), and extending to all Pinterest browser extensions.

## Takeaways
- Extending a visual search system to third-party surfaces is largely a client-engineering problem: capture, cropping UX, and data transport dominate the design.
- Small transport optimizations (resize before upload, link-based re-search, parallel upload+search) are where most of the perceived latency was won.
- Defaulting to an initial search with an animated crop selector both teaches the interaction and guarantees non-empty first results.
