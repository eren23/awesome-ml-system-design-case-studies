---
id: cs1820
title: "Duolingo & AWS — Powering Language Learning on Duolingo with Amazon Polly"
company: Duolingo
primary_category: audio
sub_category: tts
year: "2017"
source_url: https://aws.amazon.com/blogs/machine-learning/powering-language-learning-on-duolingo-with-amazon-polly/
tags: [tts, amazon-polly, microservices, caching, a-b-testing]
---

# Duolingo & AWS — Powering Language Learning on Duolingo with Amazon Polly
**Duolingo** · 2017 · [source](https://aws.amazon.com/blogs/machine-learning/powering-language-learning-on-duolingo-with-amazon-polly/)

## Problem
Duolingo relied on human voice recordings to deliver audio for its language courses, which made it expensive and slow to expand to new languages or add content. With 170 million users and a growing language catalog, producing and managing recordings by hand was no longer sustainable at scale.

## Approach / System design
Duolingo replaced human recordings with Amazon Polly's neural TTS across 25 languages, connecting it through an AWS microservice pipeline. Audio assets are generated on demand, then persisted and served through a combination of Elastic Beanstalk, SQS, DynamoDB, S3, and CloudFront to handle caching and global distribution efficiently.

## Key decisions
Choosing a managed TTS service rather than training a custom model allowed Duolingo to move quickly and offload voice-quality improvements to AWS. Pre-generating and caching audio in S3 with CloudFront distribution avoided re-synthesizing the same phrases repeatedly, keeping latency low for end users.

## Stack
Amazon Polly, AWS Elastic Beanstalk, Amazon SQS, Amazon DynamoDB, Amazon S3, Amazon CloudFront.

## Results
The pipeline successfully delivers synthesized audio to 170 million users across 25 languages. Quality was validated through A/B testing against the prior human-recorded baseline. No specific latency or cost figures are covered in the source.

## Takeaways
Neural TTS makes it practical to scale a language-learning product to dozens of languages without the bottleneck of recording studios and voice talent. A caching layer between synthesis and delivery is essential to avoid redundant synthesis calls at high traffic volumes.
