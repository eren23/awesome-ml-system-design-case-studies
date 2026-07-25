---
id: cs2388
title: Arming Customer Service with Technology to Detect Fraud Over the Phone
company: Block (Square)
primary_category: fraud
sub_category: account-takeover
year: 2022
source_url: https://block.xyz/inside/arming-square-customer-service-with-technology-to-detect-fraud-over-the-phone
tags: [voice-authentication, phone-fraud, customer-service, ml, social-engineering]
---

# Arming Customer Service with Technology to Detect Fraud Over the Phone
**Block (Square)** · 2022 · [source](https://block.xyz/inside/arming-square-customer-service-with-technology-to-detect-fraud-over-the-phone)

## Problem
Imposter scams became the leading fraud category: social engineers impersonate Square sellers (or Square itself) on phone calls to manipulate people into revealing sensitive information or compromising accounts. These attacks bypass traditional online security controls because they target human interactions with customer service.

## Approach / System design
Block partnered with Pindrop to add ML-enabled voice authentication to Square customer service phone lines. Incoming calls are scored in real time using multiple signal families — phone-number evaluation through carriers, acoustic and device characteristics, and voice indicators — to flag high-risk callers before they reach support agents, specifically targeting fraudsters impersonating real sellers.

## Key decisions
- Bought rather than built: partnered with a phone-fraud specialist (Pindrop) instead of building voice-risk models in-house.
- Multi-factor call analysis: carrier verification, acoustic patterns, device fingerprinting, and voice analysis combined, rather than relying on any single signal.
- Real-time scoring (identification within seconds) so risk is known before or during the agent conversation.

## Stack
Pindrop's ML-based voice authentication and phone-risk platform, integrated into Square's customer service call flow. Further implementation detail is not covered in the source.

## Results
The system identifies malicious callers with a high degree of accuracy and has been effective at decreasing impersonation-based phone fraud. The source does not disclose specific metrics (fraud-reduction percentages, false-positive rates).

## Takeaways
- Fraud defense has to extend beyond online controls to the phone channel, where social engineering thrives.
- Layered signals (network, device, acoustic, voice) are more robust than any single authentication factor.
- Arming human agents with real-time risk scores blends ML detection with human judgment at the point of attack.
