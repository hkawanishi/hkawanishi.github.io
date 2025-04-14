---
layout: post
title: Turning Legal Jargon into Plain English with emoji 
subtitle: A Gen AI Translator for Terms of Service
gh-repo: hkawanishi/GenAI-Intensive-Course
author: Hiromi
---
## Introduction
Let's face it, wading through the legal complexities of Terms of Service agreements is rarely a highlight of anyone's day. For my Gen AI Intensive Course project, I initially aimed to explore sports data analysis with Gemini, envisioning summaries of exciting basketball or baseball matches. However, a seemingly insurmountable hurdle appeared: the Terms of Service of my chosen data source made it unclear whether using the data for machine learning was even permitted due to the dense legal language. This experience highlighted a common problem, the inaccessibility of legal documents. It was this frustration that ignited the idea for my capstone project, a Terms of Service translator powered by Gen AI. My goal is to transform convoluted legal jargon into clear, casual English and showcase the practical applications of the skills I gained during the intensive course.

## My Approach with Gen AI
Here's a breakdown of the key steps I took to build this Terms of Service translator:
* Created a sample Terms of Service document for a fictitious company, "Dig-A-Hole," offering a stress-relief digging service, and saved it as a PDF.
* Set up the necessary Google API key to access the Gen AI models.
* Selected a suitable Gemini model for language processing.
* Read the PDF document and used a prompt to instruct Gemini to summarize the legal text into plain, easy-to-understand English.
* Employed few-shot prompting with examples to guide Gemini in incorporating relevant emojis.
* Structured the output using JSON to directly link original legal terms to their simplified translations.
* Utilized Gemini again to evaluate the quality of the translated output based on defined metrics, criteria, and a rating rubric.
This multi-step process allowed me to create a tool that not only translates complex legal text but also aims to make it more accessible and engaging.
