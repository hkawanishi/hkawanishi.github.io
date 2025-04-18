---
layout: post
title: Turning Legal Jargon into Plain English with Emoji 
subtitle: A Gen AI Translator for Terms of Service Document
gh-repo: hkawanishi/GenAI-Intensive-Course
author: Hiromi
---
## Introduction

Let’s face it, digging through the legal maze of Terms of Service agreements isn’t exactly anyone’s idea of fun. For my Gen AI Intensive Course project, I originally planned to dive into sports data analysis with Gemini, imagining summaries of exciting basketball or baseball games. But I hit a roadblock when I realized the legal wording in my chosen data source's Terms of Service was so complicated, I couldn't tell if using the data for machine learning was even allowed.That frustration got me thinking about a bigger issue, which is how difficult legal documents can be to understand. And that’s what sparked the idea for my capstone project, a Terms of Service translator powered by Gen AI. My goal is to turn confusing legal jargon into clear, casual English and to show how the tools and techniques I’ve learned can be put to good use.

## My Approach

Here's a breakdown of the key steps I took to build this Terms of Service translator:

* Created a sample Terms of Service document for a fictitious company, "Dig-A-Hole," offering a stress-relief digging service, and saved it as a PDF.
* Set up the necessary Google API key to access the Gen AI models.
* Selected a suitable Gemini model for language processing.
* Read the PDF document and used a prompt to instruct Gemini to summarize the legal text into plain, easy-to-understand English.
* Employed few-shot prompting with examples to guide Gemini in incorporating relevant emojis.
* Structured the output using JSON to directly link original legal terms to their simplified translations.
* Utilized Gemini again to evaluate the quality of the translated output based on defined metrics, criteria, and a rating rubric.
* Implemented interactivity in the Terms of Service using Embedding and RAG.

This multi-step process allowed me to create a tool that not only translates complex legal text but also aims to make it more accessible and engaging.

## Details of how I did it

### Initial Setup

My coding for this Gen AI Intensive Course project, hosted on Kaggle, began with obtaining the necessary API key to access Google's AI models. Google Cloud AI Platform documentation provides the steps for this, and it's important to secure your key once you have it.

With the technical setup done, I needed a Terms of Service document. To avoid copyright issues with real-world examples, I created my own for a quirky fictitious company named "Dig-A-Hole." This company offers a subscription for digging holes in a field as a stress reliever and form of exercise. I outlined the service's terms in a PDF, which was then ready for the AI.

### Reading the PDF document

When I first started, the gemini-1.5-pro model caught my eye, mainly due to its massive context window. I figured, the longer the Terms of Service, the better this model would handle it. However, as things progressed and I started evaluating the output, my model choice actually changed, a little surprise I'll elaborate on later.

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
Here are some examples of how to translate legal terms of service and their friendly summaries using emoji:

Original: "We reserve the right to accept or refuse membership in our discretion." 
Translated: "We get to say yay 👍 or nay 👎 to memberships, just because we can💪!"

Original: "To the maximum extent permitted by law, you agree that the Company shall not be held liable for any injuries, damages, or losses incurred in connection with the use of our services or products. By using our services, you waive any right to bring a claim or lawsuit against us for such injuries."
Translated: "Oops! If you trip, slip, or fall dramatically and get hurt while using our stuff, please don’t sue us 😅🙏. By hanging out with us, you're saying, 'Okay cool, I won't blame you if I bonk myself💖'"

Please summarize the following terms of service in plain, easy-to-undersand English with emoji.
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

I was really happy with the friendlier translations achieved with Few-Shot Prompting. However, I then had another idea. What if I could display the original legal terms directly alongside their easy-to-understand translations? That way, the users can see exactly what was changed or clarified if they want. To achieve this structured output, I utilized the Gemini AI's capability to return responses in JSON format. This was activated by specifying the `response_mime_type` as `application/json` in my request to the API. This ensures that theoriginal legal terms and their corresponding translations were provided in a structured format. The results were shown below:

`````
[
    {
        "Original": "These Terms of Service constitute a legally binding agreement between you (\"Customer,\" \"you,\" or \"your\") and Dig-A-Hole (\"Dig-A-Hole,\" \"we,\" \"us,\" or \"our\"). By using our services, you acknowledge that you have read, understood, and agree to be bound by these Terms.",
        "Translated": "This is like a pinky swear 🤝 between you (that's \"you\" 😉) and us (that's \"Dig-A-Hole\" 🕳️). By using our services, you are saying \"I get it, and I agree!\" 👍"
    },
    {
        "Original": "Dig-A-Hole provides a facility where customers can engage in the activity of digging holes in designated areas of a field. Our services are intended for recreational exercise and stress relief.",
        "Translated": "We provide a place where you can dig holes 🕳️ to your heart's content! It's great for exercise 💪 and chilling out 😌."
    },
    ...
`````

### Evaluating the Translation. Did it Pass the 'Plain English' Test?

My goal was to make those intimidating Terms of Service feel like a friendly chat. But how well did my Gen AI translator actually pull that off? One of the coolest parts of this project was getting AI to evaluate AI! Here, I used Gemini to assess if the translations were done right by focusing on three key areas.

* **Clarity:** The translation is easy to understand for everyone. 
* **Friendliness:** The translation should be approachable, casual, and enthusiastic tone, using emojis and informal language to create a positive and engaging experience for the reader. 
* **Completeness:** Is it accurate? Does it fully conveys the core meaning, and are key pieces of information presented? All the essential facts, actions, entities, and relationships described need to be captured.

To get a sense of this, I also set up a simple rating scale from 1 (very bad) to 5 (very good) and evaluated a few examples.

Let's look at the evaluation of one of the terms.

`````
Original: These Terms of Service constitute a legally binding agreement between you ("Customer," "you," or "your") and Dig-A-Hole ("Dig-A-Hole," "we," "us," or "our"). By using our services, you acknowledge that you have read, understood, and agree to be bound by these Terms.
Translated: This is like a pinky swear 🤝 between you (that's "you" 😉) and us (that's "Dig-A-Hole" 🕳️). By using our services, you are saying "I get it, and I agree!" 👍
Verbose Evaluation:
## Evaluation

**STEP 1: Assessment**

*   **Clarity:** The translation is very clear and uses simple language. The analogy of a "pinky swear" is effective in conveying the binding nature of the agreement.
*   **Friendliness:** The translation is extremely friendly, using emojis and informal language to create a welcoming tone. The use of phrases like "that's 'you' 😉" and "I get it, and I agree! 👍" adds to the friendly and approachable feel.
*   **Completeness:** The translation captures the core meaning of the original sentence. It identifies the parties involved (you and Dig-A-Hole) and explains that using the services implies agreement with the terms. While it simplifies the legal jargon, it retains the essential information.

**STEP 2: Scoring**

Based on the rubric, the translation deserves a rating of **5 (Very good)**. It is accurate, clear, friendly, and complete, effectively conveying the meaning of the original sentence in a simplified and engaging manner.

Structured Evaluation: VERY_GOOD

`````

My evaluation of this translation highlighted it as **very good**. It was clear, extremely friendly with the emoji use and casual tone, and it effectively conveyed the core meaning of the original without getting bogged down in legal jargon. It earned a top score of 5!

I should note that, to perform this evaluation, I found that the `chat` functionality in the Gemini API within my Kaggle environment at the time required using a model like `gemini-2.0-flash`. While I initially leaned towards `gemini-1.5-pro` for its general capabilities, `gemini-2.0-flash` was readily available for this specific evaluation task using the `chat` endpoint. The core translation itself was performed using Gemini's general content generation capabilities.

Overall, my initial evaluation suggests that the Gen AI translator is doing a pretty good job of turning complex legal speak into something much more approachable and understandable for everyone.

### Ask Away! Making the Terms of Service Interactive

I was really happy with how the friendly translator turned out! But then I started thinking, "What could make this even cooler?" While this wasn’t part of my original project plan, I decided to go on a little side quest: making the Terms of Service interactive.

This part of the project is a sneak peek into what a "version 2.0" could look like. It allows users to ask specific questions and get AI-powered answers pulled directly from the document. Instead of reading through the entire (even if simplified) Terms of Service, users can just ask what they need to know. This makes navigating even the most boring legal docs faster, friendlier, and way more useful.

To make this happen, I used a technique called Retrieval-Augmented Generation (RAG). Think of it like giving the AI a superpower to “search” through the document for the best answers to your questions. It's kind of like an ultra-helpful chatbot with a legal cheat sheet.

Here’s how it works:

1. First, the Terms of Service document is broken into chunks, and each chunk is turned into a special numerical fingerprint called an embedding. These embeddings capture the semantic meaning of the text.
2. When someone asks a question (like “What is the cancellation policy?”), the question is also turned into its own embedding.
3. The system compares the question’s embedding to the document’s embeddings to find the most relevant sections.
4. Finally, the AI takes those chunks and generates a helpful, plain-English answer with a friendly tone and even some emojis! 🎯✨
    
For example, this is a Prompt, Question and Passage which the AI found the information:

`````
You are a very friendly bot that answers questions using text from the reference passage included below.
Be sure to respond in a complete sentence, but being casual and very friendly. Make sure to include some appropriate emoji.
You need to use easy-to-understand English instead of using legal terms. If the passage is irrelevant to the answer, you
may say that you can not find the information.

QUESTION: What is the cancellation policy?

PASSAGE: 3. Subscription Terms and Payment ● Minimum Subscription Period: All subscriptions have a minimum commitment of one (1) full month. ● Subscription Fees: The monthly subscription fee will be clearly communicated on our website or at our facility. ● Billing: Subscription fees will be billed on a recurring monthly basis, commencing on the date of your initial subscription. ● Payment Methods: We accept the payment methods specified on our website or at our facility. You agree to provide accurate and up-to-date payment information. ● Cancellation: You may cancel your subscription at any time. However, due to the minimum one-month commitment, you will be responsible for the full payment of the current billing cycle in which you cancel, and your access will continue until the end of that paid month. No refunds will be provided for partial months.
`````

And the AI's answer to the question "what is the cancellation policy?" is:

`````
Hey there! 👋 You can cancel your subscription whenever you want, but since there's a one-month minimum, you'll still need to pay for the current month you're in. Your access will keep going until the end of that month you've already paid for. Just so you know, there are no refunds for partial months. 😊
`````
This feature turns a static document into an interactive experience. It’s still a prototype, but the idea of blending translation, search, and conversation feels like a promising step toward making everyday legal documents way more accessible. 
Note that it is true that you might be able to achieve something similar using a few-shot prompt—just feed the whole Terms of Service into the AI and ask something like, “Can you tell me the cancellation policy?” In many cases, that actually works just fine!

But through my own experimenting, I found that using RAG is often more accurate, especially when the document does not contain an answer. For example, if someone asks “What is the rental shoes policy?” and that topic isn’t covered in the document, the few-shot prompt version might confidently provide an answer about something like shovel rentals, which is entirely unrelated.

With RAG, the AI is grounded in the actual document. If the answer isn’t there, it tends to say so, rather than guessing or hallucinating. In my limited testing, this led to fewer made-up answers and a more trustworthy user experience.

## Conclusion

In conclusion, this project demonstrates the powerful potential of Gen AI to transform complex legal documents like Terms of Service into clear, accessible language, even adding a touch of friendly personality with emojis. By combining translation, few-shot prompting for style, and evaluation, I've shown how AI can bridge the gap between dense legal jargon and everyday understanding. The "Ask Away!" feature further highlights the potential for interactive engagement with such documents, making information retrieval easier than ever.

## Future Work Recommendation

This was a really fun project to tackle in a short amount of time! For the future project idea, it would be fun to explore expanding it by supporting a wider range of legal document types beyond just Terms of Service, like privacy policies or even parts of contracts, and perhaps even adding the ability to read Terms of Service directly from a URL. Another interesting direction could involve incorporating user feedback mechanisms to continuously refine the translation quality and tailor the output to better meet individual comprehension needs.  



 
