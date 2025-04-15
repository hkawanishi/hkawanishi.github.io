---
layout: post
title: Turning Legal Jargon into Plain English with emoji 
subtitle: A Gen AI Translator for Terms of Service
gh-repo: hkawanishi/GenAI-Intensive-Course
author: Hiromi
---
## Introduction

Let's face it, wading through the legal complexities of Terms of Service agreements is rarely a highlight of anyone's day. For my Gen AI Intensive Course project, I initially aimed to explore sports data analysis with Gemini, envisioning summaries of exciting basketball or baseball matches. However, a seemingly insurmountable hurdle appeared: the Terms of Service of my chosen data source made it unclear whether using the data for machine learning was even permitted due to the dense legal language. This experience highlighted a common problem, the inaccessibility of legal documents. It was this frustration that ignited the idea for my capstone project, **a Terms of Service translator** powered by Gen AI. My goal is to transform convoluted legal jargon into clear, casual English and showcase the practical applications of the skills I gained during the intensive course.

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

### Initial Setup

My coding for this Gen AI Intensive Course project, hosted on Kaggle, began with obtaining the necessary API key to access Google's AI models. Google's documentation provides the steps for this, and it's important to secure your key once you have it.

With the technical setup done, I needed a Terms of Service document. To steer clear of copyright issues with real-world examples, I created my own for a quirky fictitious company named "Dig-A-Hole." This company offers a subscription for digging holes in a field as a stress reliever and form of exercise. I outlined the service's terms in a PDF, which was then ready for the AI.

### Reading the PDF document

When I first started, the gemini-1.5-pro model caught my eye, mainly due to its massive context window. I figured, the longer the Terms of Service, the better this model would handle it. However, as things progressed and I started evaluating the output, my model choice actually changed, a little surprise I'll get into later.

So, with gemini-1.5-pro chosen for its ability to handle potentially long documents, I proceeded to the first task: summarizing our "Dig-A-Hole" Terms of Service. I used a simple prompt for this: "Please summarize the following terms of service in plain, easy-to-understand English." The resulting summary was quite good, providing a clear and easy-to-grasp overview, which looked like this:

`````
This is a summary of the Dig-A-Hole Terms of Service:

What Dig-A-Hole offers: Dig-A-Hole lets you dig holes in their field for fun and stress relief. They offer a free trial dig, monthly subscriptions, and optional shovel rentals.

Agreement: By using their services, you agree to these terms.

Subscriptions: Subscriptions are monthly and require a one-month minimum commitment. You can cancel anytime, but you still have to pay for the current month. No refunds for partial months. The price is listed on their website or at the facility.

Shovel Rental: You can rent shovels for an extra fee, but you're responsible for any damage or loss (beyond normal wear and tear).
`````
While this was clear, it felt a little… formal. I wanted to inject some personality and make it more approachable.

### Make it Friendlier. Enter Few-Shot Prompt!

One of the cool techniques I picked up during the Gen AI Intensive Course was "Few-Shot Prompting." It's like giving Gemini a few examples to learn from, showing it the style and tone you're aiming for. I wanted the translations to be more casual and friendly, sprinkled with some relevant emojis. So, I provided Gemini with a few examples like this:

~~~
few_shot_prompt = """
Here are some examples of how to translate leagal terms of service and their friendly summaries using emoji:

Original: "We reserve the right to accept or refuse membership in our discretion." 
Translated: "We get to say yay 👍 or nay 👎 to memberships, just because we can💪!"

Original: "To the maximum extent permitted by law, you agree that the Company shall not be held liable for any injuries, damages, or losses incurred in connection with the use of our services or products. By using our services, you waive any right to bring a claim or lawsuit against us for such injuries."
Translated: "Oops! If you trip, slip, or fall dramatically and get hurt while using our stuff, please don’t sue us 😅🙏. By hanging out with us, you're saying, 'Okay cool, I won't blame you if I bonk myself💖'"

Please summarize the following terms of servicein plain, easy-to-undersand English with emoji.
"""
~~~

Here, I was essentially asking Gemini to channel its inner friendly neighbor. I made sure to include emojis in the examples and explicitly asked for them in the final translation. The results were exactly what I was hoping for. Much more casual and fun!
 
`````
Welcome to Dig-A-Hole! 🕳️  Here's the simple version of our rules:

* **What we do:** We give you a place to dig holes!  It's for fun and stress relief. 😄  You can dig by yourself or with friends.👯‍♀️
* **Free Trial:**  First dig is on us! 🎉
* **Membership:**  If you like digging, you can sign up for a monthly membership. 🗓️  You're in for at least one month.  You can cancel anytime, but you still have to pay for the current month. 💰 No refunds for partial months.
* **Shovels:** We have shovels you can rent. 🥄  Pay extra, and please bring them back in one piece (normal wear and tear is okay).  If you break or lose it, you'll have to pay for it. 💸
`````

As you can see, Few-Shot Prompting is a relatively straightforward technique that can significantly influence the tone and style of Gemini's output, making the translated texts much more aligned with my vision.

### Pairing Original and Translated Text

I was really happy with the friendlier translations achieved with Few-Shot Prompting. However, I then had another idea: what if I could display the original legal terms directly alongside their easy-to-understand translations? To achieve this, I thought about leveraging Gemini API's JSON mode...

 
