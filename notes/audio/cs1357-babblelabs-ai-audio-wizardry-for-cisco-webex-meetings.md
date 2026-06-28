---
id: cs1357
title: BabbleLabs - AI audio wizardry for Cisco Webex Meetings
company: Cisco (Webex)
primary_category: audio
sub_category: audio-classification
year: 2021
source_url: https://blog.webex.com/collaboration/video-conferencing/babblelabs-ai-audio-wizardry-for-cisco-webex-meetings/
tags: [noise-suppression, speech-enhancement, deep-learning, real-time, meetings]
---

# BabbleLabs - AI audio wizardry for Cisco Webex Meetings
**Cisco (Webex)** · 2021 · [source](https://blog.webex.com/collaboration/video-conferencing/babblelabs-ai-audio-wizardry-for-cisco-webex-meetings/)

## Problem
Video-conference audio is hurt by background noise, reverberation, and poor network conditions. Traditional noise suppression handles steady noise poorly and fails on transient sounds (barking dogs, honking horns) and highly reverberant rooms.

## Approach / System design
Integrate BabbleLabs' deep-learning speech enhancement into Webex Meetings to clean speech in real time, distinguishing speakers at different distances from the mic while suppressing background noise and reverberation, with minimal added latency.

## Key decisions
- Hit a ~10 ms processing latency to stay viable for live conferencing.
- Cut computational cost dramatically (cited as ~400x more efficient than the initial release) for broad deployment.
- Kept processing privacy- and security-conscious.

## Stack
Neural network models trained on hundreds of thousands of hours of speech and noise plus tens of thousands of hours of room-acoustics recordings; quality measured with the ITU P.862 (PESQ) standard.

## Results
Webex removed more noise and reverberation and scored significantly higher than the then-recent Zoom (5.4.1) and Microsoft Teams (1.4.00.4167) releases; speech quality reportedly improved 2x since the initial release.

## Takeaways
Production audio ML needs large labeled datasets and standardized metrics, and computational efficiency is essential for shipping enhancement to every meeting participant.
