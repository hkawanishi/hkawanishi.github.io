---
layout: post
title: Turning Legal Jargon into Plain English with Emoji 
subtitle: A Gen AI Translator for Terms of Service Document
gh-repo: hkawanishi/GenAI-Intensive-Course
author: Hiromi
---
## Introduction

Let’s face it, digging through the legal maze of Terms of Service agreements isn’t exactly anyone’s idea of fun. For my Gen AI Intensive Course project, I originally planned to dive into sports data analysis with Gemini, imagining summaries of exciting basketball or baseball games. But I hit a roadblock when I realized the legal wording in my chosen data source's Terms of Service was so complicated, I couldn't tell if using the data for machine learning was even allowed. That frustration got me thinking about a bigger issue, which is how difficult legal documents can be to understand. And that’s what sparked the idea for my capstone project, **a Terms of Service translator powered by Gen AI**. My goal is to turn confusing legal jargon into clear, casual English and to show how the tools and techniques I’ve learned can be put to good use.

## How I Built This: A Step-by-Step Journey

So, how did I go about building this translator to make sense of those tricky Terms of Service? Let me walk you through the steps I took:

* It all began with the creation of a sample Terms of Service document for a fun, made-up company called "Dig-A-Hole." I saved these digging rules as a PDF, ready for AI magic.
* Then, I secured my access to the Gen AI world by setting up the necessary Google API key.
* Next, I carefully selected a Gemini model that seemed well-suited for the task of understanding and simplifying legal language.
* My initial move was to read the PDF and use a clear prompt to ask Gemini to summarize the legal text in plain, easy-to-grasp English.
* To add a touch of friendliness, I used few-shot prompting, showing Gemini examples of translations that included relevant emoji.
* To make the results easy to follow, I structured the output using JSON, directly connecting the original legal terms with their newly translated texts.
* In an interesting twist, I even used Gemini to evaluate the quality of its own translation work, based on criteria I defined.
* And to take it a step further, I implemented interactive querying of the Terms of Service using Embeddings and RAG, allowing users to ask specific questions and get direct answers.

This step-by-step approach allowed me to create a tool that I hope makes those often-intimidating legal documents much more approachable and understandable.

## Details of how I did it

### Initial Setup

My coding for this Gen AI Intensive Course project, hosted on Kaggle, began with obtaining the necessary API key to access Google's AI models. Google Cloud AI Platform documentation provides the steps for this, and it's important to secure the key once obtained it.

With the technical setup done, I needed a Terms of Service document. To avoid copyright issues with real-world examples, I created my own for a quirky fictitious company named "Dig-A-Hole." This company offers a subscription for digging holes in a field as a stress reliever and form of exercise. I outlined the service's terms and saved it in a PDF.

### Selecting a Model and Reading the PDF document

When I first started, the gemini-1.5-pro model caught my eye, mainly due to its massive context window. I figured, the longer the Terms of Service, the better this model would handle it. However, as things progressed and I started evaluating the output, my model choice actually changed, a little surprise I'll elaborate on later.

So, with the model chosen, I proceeded to the first task: summarizing our "Dig-A-Hole" Terms of Service. I used a simple prompt: "Please summarize the following terms of service in plain, easy-to-understand English." The resulting summary was quite good, providing a clear and easy-to-grasp overview, which looked like this:

`````
Dig-A-Hole's Terms of Service basically say:

* Digging Holes: You can dig holes at their facility for fun and stress relief. They offer a free trial dig, then you need a monthly subscription. You can also rent shovels.
* The Agreement: By using their services, you agree to these rules.
* Subscriptions: Subscriptions are monthly and you have to pay for the whole month even if you cancel early. The price is on their website or at the facility.
* Shovel Rental: You can rent shovels for an extra fee and you're responsible for any damage beyond normal wear and tear.
...
`````
While this was clear, it felt a little… formal. I wanted to inject some personality and make it more approachable.

### Make it Friendlier. Enter Few-Shot Prompt!

One of the cool techniques I picked up during the Gen AI Intensive Course was "Few-Shot Prompting." It's like giving Gemini a few examples to learn from, showing it the style and tone you're aiming for. I wanted the translations to be more casual and friendly, sprinkled with some relevant emoji. So, I provided Gemini with a few examples like this:

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

Here, I was essentially asking Gemini to channel its inner friendly neighbor. I made sure to include emoji in the examples and explicitly asked for them in the final translation. The results were exactly what I was hoping for. Much more casual and fun!
 
`````
Want to dig a hole? 🕳️ Here's the deal:

1. **The Agreement:** This is a contract. By digging with us, you agree to these rules. 🤝
2. **What We Do:** We provide a place for you to dig holes for fun and stress relief!  We offer a free trial dig, then monthly subscriptions.  You can also rent a shovel. 🥄
3. **Subscriptions & Payment:** Subscriptions are for a minimum of one month.  We'll tell you the price on our website or at our facility.  You can cancel anytime, but you still have to pay for the current month.  No refunds for partial months. 🗓️💰
4. **Shovel Rental:**  You can rent a shovel 🥄 for an extra fee.  Please return it in good condition (normal wear and tear is okay).  We might charge you if you break or lose it.
...
`````

As you can see, Few-Shot Prompting is a relatively straightforward technique that can significantly influence the tone and style of Gemini's output, making the translated texts much more aligned with my vision.

### Pairing Original and Translated Text

I was really happy with the friendlier translations achieved with Few-Shot Prompting. However, I then had another idea. What if I could display the original legal terms directly alongside their easy-to-understand translations? That way, the users can see exactly what was changed or clarified if they want. To achieve this structured output, I utilized the Gemini AI's capability to return responses in JSON format. This was activated by specifying the `response_mime_type` as `application/json` in my request to the API. This ensures that the original legal terms and their corresponding translations were provided in a structured format. The results were shown below:

`````
[
    {
        "Original": "These Terms of Service constitute a legally binding agreement between you (\"Customer,\" \"you,\" or \"your\") and Dig-A-Hole (\"Dig-A-Hole,\" \"we,\" \"us,\" or \"our\"). By using our services, you acknowledge that you have read, understood, and agree to be bound by these Terms.",
        "Translated": "This is like a pinky swear 🤝 between you (that's you!) and us (Dig-A-Hole!). By playing here, you're saying you get the rules and promise to follow them. 💖"
    },
    {
        "Original": "Dig-A-Hole provides a facility where customers can engage in the activity of digging holes in designated areas of a field. Our services are intended for recreational exercise and stress relief.",
        "Translated": "We've got a place where you can dig holes to your heart's content! 🕳️ It's great for exercise and chilling out. 😎"
    },
    ...
`````

### Evaluating the Translation. Did it Pass the 'Plain English' Test?

My goal was to make those intimidating Terms of Service feel like a friendly chat. But how well did my Gen AI translator actually pull that off? And guess what? I can make AI to evaluate AI! Here, I used Gemini to assess if the translations were done right by providing three key areas.

* **Clarity:** The translation is easy to understand for everyone. 
* **Friendliness:** The translation should be approachable, casual, and enthusiastic tone, using emojis and informal language to create a positive and engaging experience for the reader. 
* **Completeness:** Is it accurate? Does it fully conveys the core meaning, and are key pieces of information presented? All the essential facts, actions, entities, and relationships described need to be captured.

To get a sense of this, I also set up a simple rating scale from 1 (very bad) to 5 (very good) and evaluated a few examples.

Let's look at the evaluation of one of the terms.

`````
Original: These Terms of Service constitute a legally binding agreement between you ("Customer," "you," or "your") and Dig-A-Hole ("Dig-A-Hole," "we," "us," or "our"). By using our services, you acknowledge that you have read, understood, and agree to be bound by these Terms.
Translated: This is like a pinky swear 🤝 between you (that's you!) and us (Dig-A-Hole!). By playing here, you're saying you get the rules and promise to follow them. 💖
Verbose Evaluation:
## Evaluation

**STEP 1:**

*   **Clarity:** The translation uses a "pinky swear" analogy to explain the legally binding agreement, which is clear and easy to understand. It simplifies the language effectively.
*   **Friendliness:** The translation is extremely friendly, using phrases like "that's you!" and emojis (🤝, 💖). The tone is enthusiastic and welcoming.
*   **Completeness:** The translation captures the core meaning of the original sentence, explaining that using the services means agreeing to the terms.

**STEP 2:**

Based on the rubric, the translation is very good.

`````

My evaluation of this translation highlighted it as **very good**. It was clear, extremely friendly with the emoji use and casual tone, and it effectively conveyed the core meaning of the original without getting bogged down in legal jargon. It earned a top score of 5!

I should note that, to perform this evaluation, I found that the `chat` functionality in the Gemini API within my Kaggle environment at the time required using a model like `gemini-2.0-flash`. While I initially leaned towards `gemini-1.5-pro` for its general capabilities, `gemini-2.0-flash` was readily available for this specific evaluation task using the `chat` endpoint. The core translation itself was performed using Gemini's general content generation capabilities.

Overall, my initial evaluation suggests that the Gen AI translator is doing a pretty good job of turning complex legal speak into something much more approachable and understandable for everyone.

### Ask Away! Making the Terms of Service Interactive

I was really happy with how the friendly translator turned out! But then I started thinking, "What could make this even cooler?" While this wasn’t part of my original project plan, I decided to go on a little side quest: making the Terms of Service interactive.

This part of the project is a sneak peek into what a "version 2.0" could look like. It allows users to ask specific questions and get AI-powered answers pulled directly from the document. Instead of reading through the entire (even if simplified) Terms of Service, users can just ask what they need to know. This makes navigating even the most boring legal docs faster, friendlier, and way more useful.

To make this happen, I used a technique called Retrieval-Augmented Generation (RAG). Think of it like giving the AI a superpower to “search” through the provided document for the best answers to your questions. It's kind of like an ultra-helpful chatbot with a legal cheat sheet.

Here’s how it works:

1. First, the Terms of Service document is broken into chunks, and each chunk is transformed into a vector representation called an embedding. These embeddings capture the semantic meaning of the text.
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
This feature turns a static document into an interactive experience. It’s still a prototype, but the idea of blending translation, search, and conversation feels like a promising step toward making everyday legal documents more accessible. 

Now, you might be thinking, "Could I just use a few-shot prompt for this?" You could certainly try feeding the entire Terms of Service to the AI and asking something like, “What's the cancellation policy?” And you know what? That probably works. But what I quickly discovered in my testing is that RAG is often significantly more reliable, especially when the answer isn't explicitly in the document. For example, if someone asks “What is the rental shoes policy?” and that topic isn’t covered in the document, the few-shot prompt version might confidently provide an answer about something like shovel rentals, which is entirely unrelated. With RAG, because it's retrieving information directly from the document, it's much better at saying "I don't know" instead of making things up, which ultimately builds more trust.

## Conclusion

So, what's the takeaway? This project shows just how powerful Gen AI can be when it comes to tackling those complex legal documents, like Terms of Service, and making them clear and accessible, even adding a bit of friendly personality with emojis. By putting together translation, style guidance, and evaluation, I think we've seen how AI can help bridge that gap between dense legal speak and what we can all understand. And with the "Ask Away!" feature, getting the information you need from these documents could become easier than ever.

## Future Work Recommendation

This was a really fun project to tackle in a short amount of time! For the future project idea, it would be fun to explore expanding it by supporting a wider range of legal document types beyond just Terms of Service, like privacy policies or even parts of contracts, and perhaps even adding the ability to read Terms of Service directly from a URL. Another interesting direction could involve incorporating user feedback mechanisms to continuously refine the translation quality and tailor the output to better meet individual comprehension needs.  



 
