---
layout: post
title: Turning Legal Jargon into Plain English with emoji 
subtitle: A Gen AI Translator for Terms of Service
gh-repo: hkawanishi/GenAI-Intensive-Course
author: Hiromi
---
## Introduction
Let's face it, wading through the legal complexities of Terms of Service agreements is rarely a highlight of anyone's day. For my Gen AI Intensive Course project, I initially aimed to explore sports data analysis with Gemini, envisioning summaries of exciting basketball or baseball matches. However, a seemingly insurmountable hurdle appeared: the Terms of Service of my chosen data source made it unclear whether using the data for machine learning was even permitted due to the dense legal language. This experience highlighted a common problem, the inaccessibility of legal documents. It was this frustration that ignited the idea for my capstone project, a Terms of Service translator powered by Gen AI. My goal is to transform convoluted legal jargon into clear, casual English and showcase the practical applications of the skills I gained during the intensive course.

## My Approach
Here's a breakdown of the key steps I took to build this Terms of Service translator:
* Created a sample Terms of Service document for a fictitious company, "Dig-A-Hole," offering a stress-relief digging service, and saved it as a PDF.
* Set up the necessary Google API key to access the Gen AI models.
* Selected a suitable Gemini model for language processing.
* Read the PDF document and used a prompt to instruct Gemini to summarize the legal text into plain, easy-to-understand English.
* Employed few-shot prompting with examples to guide Gemini in incorporating relevant emojis.
* Structured the output using JSON to directly link original legal terms to their simplified translations.
* Utilized Gemini again to evaluate the quality of the translated output based on defined metrics, criteria, and a rating rubric.
This multi-step process allowed me to create a tool that not only translates complex legal text but also aims to make it more accessible and engaging.

## Details of how I did it
### Set up
My code ran inside Kaggle. Because this is a Gen AI intensive course done by Google, I first obtained the API key so that I can run code in Kaggle and connect to an external API. The details on how to get the API key is out of scope for this project. Please search Google site for that. However, once you get the API key, make sure to kee it secure. 
Also, before I ran my project, I created a sample terms of service document for a fictitious company. I might have been able to download the real company's terms of service but then I had to figure out the copyright and such, so I thought it was better to create a sample by myself. This document was saved it as a PDF. 

### Read the Sample Terms of Service
At first I selected gemini-1.5-pro model because it has an incredibly large context window. I thought, if in the future, I have a very long Terms of Service document, gemini-1.5-pro can handle well. It turns out that I had to switch the model later on when I did an evaluation. I will talk more about it later. I specified which pdf document should be read, and I asked Gemini to translate the document with a simple prompt saying "Please summarize the follwoing terms of service in plain, easy-to-understand English." The summary output was not too bad. This is the snippet of the output.
`````
This is a summary of the Dig-A-Hole Terms of Service:

What Dig-A-Hole offers: Dig-A-Hole lets you dig holes in their field for fun and stress relief. They offer a free trial dig, monthly subscriptions, and optional shovel rentals.

Agreement: By using their services, you agree to these terms.

Subscriptions: Subscriptions are monthly and require a one-month minimum commitment. You can cancel anytime, but you still have to pay for the current month. No refunds for partial months. The price is listed on their website or at the facility.

Shovel Rental: You can rent shovels for an extra fee, but you're responsible for any damage or loss (beyond normal wear and tear).
`````
