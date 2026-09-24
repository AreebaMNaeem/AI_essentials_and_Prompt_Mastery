# 🌎 The Basics You Need

## 🔶 What is AI?
**Definition:** AI (Artificial Intelligence) means building computer systems that can do things that normally need a human brain — like understanding language, telling things apart, or making choices.

➡️ **Examples:** Siri and Alexa, Netflix showing you shows you might like, your inbox blocking spam emails, and self-driving cars are all AI.

Note: AI is just the big umbrella name for this whole field. Everything you'll read below (ML, GenAI, LLMs...) is one small part *inside* that umbrella — not something separate.

---

## 🔶 Machine Learning (ML)
**Definition:** Machine Learning means the computer learns on its own by looking at lots of examples, instead of a person telling it exact rules to follow.

➡️ **Example:** Your email's spam filter was never given a list of rules. Instead, it was shown millions of emails already marked "spam" or "not spam," and it figured out the pattern itself. Same idea behind Netflix's suggestions and your bank catching a fraud charge.

🎯 **Analogy:** Teaching a small child what a dog looks like by showing them 1,000 dog pictures — not by reading them a definition.

---

## 🔶 Generative AI (GenAI)
**Definition:** Generative AI means AI that *makes* brand-new things — text, pictures, sound, video, or code — instead of just sorting or checking things that already exist.

➡️ **Examples:**
- **Text:** ChatGPT or Claude writing an email for you
- **Pictures:** Midjourney or DALL·E turning a sentence into an image
- **Video:** Sora turning a sentence into a short video
- **Code:** GitHub Copilot writing a piece of code for you

🎯 **Analogy:** A food critic tells you if a meal is good (checking). A chef makes a brand-new dish from nothing (making). GenAI is the chef.

---

## 🔶 Neural Network
**Definition:** A neural network is a computer system made of small steps stacked on top of each other, loosely copying how brain cells pass messages to one another. Each step builds a little more understanding than the step before it.

➡️ **Example:** When a phone unlocks using your face, the first step just looks for basic shapes in the photo. The next step notices those shapes make up eyes, a nose, and a mouth. The last step puts it all together and says "yes, this is you." The same step-by-step idea is also used to read handwriting and understand spoken words.

🎯 **Analogy:** A group of friends passing a photo down a line. Friend 1 only notices shapes. Friend 2 sees those shapes forming a face. Friend 3 says the name out loud. No single friend saw the whole picture by themselves — the answer was built one small step at a time. More steps = what people call "deep learning."

---

## 🔶 LLM (Large Language Model)
**Definition:** An LLM is a kind of Generative AI that was shown huge amounts of writing, and now its main job is simple: guess the next word, again and again, until it has written a full answer.

➡️ **Examples:** GPT-4 (the model behind ChatGPT), Claude, Gemini, and LLaMA are all LLMs.

**How it actually guesses:** Say you type → `"The sky is ___"`

```
blue     ████████████████████████  72% ✅ picked
cloudy   ██████                     15%
falling  ██                          6%
```

It picks the word with the highest score ("blue"), adds it to the sentence, then does the exact same thing again for the *next* word — one word at a time, until the whole reply is finished.

Note: An LLM is not searching a database for facts. It's guessing the next word based on patterns it has seen before. That's why it can sound very sure of itself while still being wrong.

---

## 🔶 Transformer
**Definition:** The Transformer is the design (made in 2017) that lets AI read a whole sentence all at once — instead of one word at a time — so it can tell which words go together, even if they're far apart in the sentence.

➡️ **Example:** In the sentence *"The trophy didn't fit in the suitcase because it was too big,"* the AI needs to know that "it" means "trophy," not "suitcase." A Transformer can figure this out because it looks at the whole sentence together, not one word at a time. This design is what ChatGPT, Claude, and Gemini are all built on.

Note: The "T" in GPT stands for **Transformer**. It's also why these AI tools can remember something you said many messages ago in a long conversation.

---

## 🔶 Types of AI Tools
| Category | What it makes | Examples |
|---|---|---|
| 💬 Chatbots | Text and conversation | ChatGPT, Claude, Gemini |
| 🖼️ Image tools | Pictures from a sentence | Midjourney, DALL·E |
| 🎬 Video tools | Short video clips | Sora, Runway |
| 🎙️ Audio tools | Speech, voices, music | ElevenLabs, Suno |

🎯 **Analogy:** A toolbox — a hammer isn't a screwdriver. ChatGPT isn't Midjourney. Every job needs the right tool.

---

## 🔶 What is a Prompt?
**Definition:** A prompt is just the message you type to tell the AI what you want.

➡️ **Weak prompt:** "Give me food." → You get something random and not very useful.
➡️ **Clear prompt:** "Suggest a medium-spicy chicken biryani recipe, low oil, for 2 people." → You get exactly what you asked for.

Note: This is the whole idea behind "prompt mastery" — the clearer your message, the better the AI's answer.

---

## 🔶 Must-Know Words
**Token** — a small piece of text the AI reads at one time (close to a word, or part of one).
➡️ *Example: "unbelievable" might get broken into small pieces like "un," "believ," and "able."*

**Training** — showing the AI a huge amount of text or data so it can learn from it.
➡️ *Example: GPT-4 was trained on a big mix of books, websites, and articles.*

**Fine-tuning** — taking an AI that already knows a lot, and teaching it one extra skill.
➡️ *Example: a general AI trained further on legal documents becomes a legal-helper AI.*

**Hallucination** — when the AI says something confidently, but it's actually wrong.
➡️ *Example: the AI names a book or study that doesn't really exist.*

⚠️ Sounding sure doesn't mean it's true — always double-check facts yourself.

---

## 🔶 Context Window
**Definition:** The context window is how much of your conversation the AI can actually hold in its memory at one time.

➡️ **Example:** If you talk to an AI for a very long time, it may start forgetting things you said near the start — not because it's careless, but because the conversation has gone past what it can hold at once.

🎯 **Analogy:** A whiteboard — once it's full, the oldest notes get wiped off to make room for new ones.

---

## 🔶 Multimodal AI
**Definition:** Multimodal AI means the AI can understand more than one kind of input at the same time — like a picture and text together, not just one on its own.

➡️ **Example:** You send a photo of a half-solved math problem and ask "what's the next step?" — the AI looks at the picture *and* reads your question together to give one answer. GPT-4o and Gemini can both do this.

---

## 🔶 AI Agents
**Definition:** An AI agent doesn't just reply with text — it can actually go and do a task for you, step by step, using tools like the internet on its own.

➡️ **Example:** Asking a chatbot for a cake recipe gives you text back. Asking an agent to "order the ingredients for this cake" makes it search a grocery website, pick the items, and check out — without you doing each step yourself.

🎯 **Analogy:** A chatbot is a waiter who tells you what's on the menu. An agent is a waiter who also goes into the kitchen, cooks the food, and brings it to your table.

---

## 🔶 Bias & Limitations
**Definition:** Because AI learns from information made by people, it can also pick up people's mistakes and one-sided opinions — without meaning to.

➡️ **Example:** If a face-recognition tool was mostly shown photos of one group of people, it may work less accurately for people outside that group — not on purpose, just because it wasn't shown enough variety.

Note: This is why you should always double-check what AI tells you, especially on sensitive topics or opinions.

---

## 🔶 Free vs. Paid AI Tools
**Definition:** Paying for an AI tool usually gets you more usage, faster replies, and a bigger memory — not a "smarter" AI underneath.

➡️ **Example:** A free chatbot might limit how many messages you can send per day. The paid version usually removes that limit and replies faster.

🎯 **Analogy:** Free = economy seat on a flight — you still get there. Paid = business class — same flight, just more comfort and speed.

---

## 🔶 Bringing It All Together

```text
AI is the goal
     ↓
Machine Learning gets us there — it learns from examples, not fixed rules
     ↓
Neural Networks are the engine — they build understanding step by step
     ↓
Generative AI is that engine used to create, not just check
     ↓
LLMs are the text version of Generative AI
     ↓
Transformers are the design that makes LLMs work well
     ↓
You use it through Prompts, its Memory (context window), Images/Voice (multimodal), or Agents
     ↓
Always watch out for wrong guesses (Hallucination) and one-sided answers (Bias)
```