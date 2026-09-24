# 🤖 Week 2: Prompt Engineering Fundamentals

## 🔶 Anatomy of a Good Prompt
A good prompt usually has 5 building blocks. Miss one, and the AI has to guess — and guessing is where bad output comes from.

| Part | What it does | Example piece |
|---|---|---|
| **Context** | Background info the AI needs | "I'm a first-year biology student" |
| **Role** | Who the AI should act as | "Act as a patient tutor" |
| **Task** | The actual thing you want done | "Explain photosynthesis" |
| **Format** | How you want the output shaped | "In 5 bullet points" |
| **Constraints** | Limits/rules to follow | "No jargon, under 100 words" |

➡️ **Put together:**
```
Context:     I'm a first-year biology student preparing for a quiz.
Role:        Act as a patient tutor.
Task:        Explain photosynthesis.
Format:      5 bullet points.
Constraints: No jargon, under 100 words.
```

That's one prompt, just written with each part labeled. Skip 3 of the 5, and you get the next section 👇

---

## 🔶 Structured vs. Unstructured — Same Question, Two Ways

### ❌ Unstructured prompt
```
Prompt: "Tell me about photosynthesis."
```
**Output:**
```
Photosynthesis is the process by which plants convert light energy 
into chemical energy. It occurs in the chloroplasts, primarily 
using chlorophyll... [continues as a generic 300-word paragraph, 
same as a textbook, not tailored to you at all]
```
🔻 Technically correct — but generic, too long for a quiz, and not aimed at your level.

### ✅ Structured prompt
```
Prompt: "I'm a first-year biology student prepping for a quiz. 
Act as a patient tutor and explain photosynthesis in 5 simple 
bullet points, no jargon, under 100 words."
```
**Output:**
```
• Plants make their own food using sunlight — that's photosynthesis.
• It happens inside chloroplasts, mostly in the leaves.
• Sunlight + water + CO2 → glucose (food) + oxygen (released).
• Chlorophyll (the green pigment) is what actually captures the light.
• This is why plants need light, water, and air to survive.
```
🔻 Same question, dramatically more useful answer — because the AI wasn't guessing what you needed.

### Second example — a research task

➡️ **Unstructured:** `"Compare renewable energy sources."`
**Output:** A long, unfocused essay covering solar, wind, hydro, geothermal, biomass — with no clear angle, because you never said *what* to compare them on.

➡️ **Structured:** `"Act as a research assistant. Compare solar vs wind energy for a small home setup, focusing on upfront cost and maintenance. Format as a 2-column table, under 150 words."`
**Output:** A tight, 2-column table — exactly the comparison you asked for, nothing extra.

---

## 🔶 Common Prompting Mistakes (and the Fix)

❌ **Mistake: Being too vague**
`"Help me with my essay."`
✅ **Fix:** `"Review my 500-word essay on climate change. Point out weak arguments and suggest 3 ways to strengthen the conclusion."`

❌ **Mistake: No format specified**
`"Give me study tips."`
✅ **Fix:** `"Give me 5 study tips for memorizing dates, as a numbered list."`

❌ **Mistake: Asking for too many things at once**
`"Summarize this paper, check my grammar, and also suggest a title."`
✅ **Fix:** Split it into 3 separate prompts, one task at a time — AI does each one better when it's not juggling three jobs.

❌ **Mistake: Expecting perfection on the first try**
Treating the first output as final, instead of refining it.
✅ **Fix:** See the next section — iteration is the actual skill.

---

## 🔶 Iterative Refinement — Treat It Like a Conversation, Not a Search Bar

A search engine gives one static answer. AI lets you push back, correct, and reshape the answer — that's the whole advantage, and most beginners never use it.

➡️ **Turn 1:**
```
You:   "Explain Newton's second law."
AI:    [gives a full textbook-style explanation with the formula F=ma]
```

➡️ **Turn 2 — refine:**
```
You:   "That's too technical. Explain it like I'm 12, using a 
        real-life example like pushing a shopping cart."
AI:    "Imagine pushing an empty shopping cart vs. one full of 
        groceries — the full one needs more force to speed up at 
        the same rate. That's F=ma: more mass (m) needs more 
        force (F) for the same acceleration (a)."
```

➡️ **Turn 3 — refine again:**
```
You:   "Perfect. Now give me one practice question based on 
        this, with the answer hidden below."
AI:    [creates a tailored practice question]
```

🔻 Notice: each turn built on the last. That back-and-forth *is* prompting — not writing one "perfect" prompt and hoping for the best.

---

## 🔶 Reusable Prompt Templates

Fill in the blanks for your own study/research tasks:

**📘 Explain a concept**
```
Act as a [tutor/expert] in [subject]. Explain [topic] to a 
[grade level/beginner], in [format: bullets/steps/analogy], 
under [word limit] words, no [jargon/complex terms].
```

**📝 Summarize something**
```
Summarize the following [text/article/chapter] in [X] sentences, 
focusing on [specific angle, e.g. "the main argument" or "key dates"]. 
Keep the tone [neutral/simple/formal].
```

**🔍 Research / compare**
```
Act as a research assistant. Compare [A] vs [B] on [specific 
criteria only — cost, speed, etc]. Present as a [table/bullets], 
under [word limit] words.
```

**✍️ Get writing feedback**
```
Review my [essay/paragraph] on [topic]. Point out [weak arguments/
grammar issues/unclear parts], and suggest [X] specific 
improvements. Don't rewrite the whole thing — just highlight fixes.
```

**❓ Practice / quiz me**
```
Create [X] practice questions on [topic], at [easy/medium/hard] 
difficulty. Hide the answers below a "---" line so I can test 
myself first.
```

---

## 🔶 Hands-On: Your Turn

Pick one real study or research task you have right now (an assignment, a topic you're stuck on, an essay you're writing). Then:

1. Write the **unstructured** version of your prompt first (just ask naturally).
2. Rewrite it as a **structured** prompt using the 5 parts (Context, Role, Task, Format, Constraints).
3. Run both and compare the two outputs side by side.
4. Refine the structured one **at least twice** — treat it as a conversation, not a one-shot search.

---

## 🔶 Bringing It All Together

```text
A prompt has 5 parts: Context, Role, Task, Format, Constraints
     ↓
Skip most of them → vague, unstructured, generic output
     ↓
Include them → structured, tailored, usable output
     ↓
The first output is a draft, not the answer
     ↓
Refine it — treat AI as a back-and-forth conversation
     ↓
Reuse templates so you don't rebuild the structure every time
```

Every prompt you'll ever write is really just these 5 parts, arranged differently.