---
id: cs1833
title: Zomato Digitizes Menus Using Amazon Textract and Amazon SageMaker
company: Zomato
primary_category: cv
sub_category: ocr
year: 2020
source_url: https://aws.amazon.com/blogs/machine-learning/zomato-digitizes-menus-using-amazon-textract-and-amazon-sagemaker/
tags: [ocr, textract, faster-rcnn, bert, menu-digitization]
---

# Zomato Digitizes Menus Using Amazon Textract and Amazon SageMaker
**Zomato** · 2020 · [source](https://aws.amazon.com/blogs/machine-learning/zomato-digitizes-menus-using-amazon-textract-and-amazon-sagemaker/)

## Problem
Zomato aggregates menus for a large number of restaurants, but menus arrive as photos or scanned PDFs with varied layouts, fonts, and languages. Converting these unstructured images into structured, searchable data manually is costly and slow, and existing generic OCR tools do not understand menu-specific structure such as sections, item names, and prices.

## Approach / System design
Zomato built a three-stage pipeline. First, Amazon Textract extracts raw text and bounding-box information from menu images. Second, a Faster R-CNN object detection model identifies and localizes menu sections within the page (starters, mains, drinks, etc.). Third, a BERT-based classifier assigns each detected text block to the appropriate semantic category within the structured output. All models were trained and managed on Amazon SageMaker.

## Key decisions
Splitting the task into separate OCR, layout detection, and classification stages allowed each component to be optimized and evaluated independently. Using a pretrained BERT model for the classification stage leveraged existing language understanding rather than training a text classifier from scratch. SageMaker was used both for training and for managing the inference pipeline.

## Stack
Amazon Textract (OCR), Faster R-CNN (layout/section detection), BERT (text classification), Amazon SageMaker.

## Results
The Faster R-CNN menu-section detector reached 0.93 mAP. The BERT classifier achieved 0.86 AUROC on the categorization task.

## Takeaways
A multi-model pipeline that separates OCR, layout understanding, and semantic classification is more robust than a single end-to-end model for document digitization tasks with structured but visually varied inputs. Leveraging managed cloud services like SageMaker for training and Textract for OCR reduces the engineering overhead of building and scaling the system.
