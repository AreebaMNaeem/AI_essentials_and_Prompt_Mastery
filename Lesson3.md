# 🤖 Week 3: Advanced Prompting Techniques

## 🔶 Few-Shot Prompting
**Definition:** Few-shot prompting means giving the AI a couple of examples of exactly the input → output pattern you want, before asking it to do the real task. Instead of guessing your format, it copies the pattern.

### ❌ Zero-shot (no examples)
```
Prompt: "Turn these notes into flashcards: 
Mitochondria = powerhouse of the cell. Produces ATP through 
respiration. Found in nearly all eukaryotic cells."
```
**Output:**
```
Flashcard 1: What is the mitochondria?
Mitochondria is the powerhouse of the cell...

(Format keeps changing every time you run it — sometimes numbered, 
sometimes Q&A, sometimes a paragraph)
```

### ✅ Few-shot (2 examples given first)
```
Prompt: "Turn notes into flashcards using this exact format:

Note: Photosynthesis = process where plants convert light into energy.
Q: What is photosynthesis?
A: The process where plants convert light into energy.

Note: DNA = molecule that carries genetic instructions.
Q: What is DNA?
A: The molecule that carries genetic instructions.

Now do the same for:
Note: Mitochondria = powerhouse of the cell. Produces ATP through 
respiration."
```
**Output:**
```
Q: What is the mitochondria?
A: The powerhouse of the cell, which produces ATP through respiration.
```
🔻 Same task, but now the AI locks onto your exact format every single time — because you showed it, instead of describing it.

---

## 🔶 Chain-of-Thought Prompting
**Definition:** Asking the AI to reason step by step *before* giving a final answer. This matters most for math, logic, and multi-step problems, where jumping straight to an answer increases the chance of a mistake.

### ❌ Without chain-of-thought
```
Prompt: "A restaurant bill is $84.50. Split evenly between 3 
people, with a 15% tip. How much does each person pay?"
```
**Output:**
```
Each person pays $32.40.   ← (wrong — it skipped steps and 
                               miscalculated)
```

### ✅ With chain-of-thought
```
Prompt: "A restaurant bill is $84.50. Split evenly between 3 
people, with a 15% tip. Show your steps first, then give the 
final answer."
```
**Output:**
```
Step 1: Tip = 15% of $84.50 = $12.68
Step 2: Total with tip = $84.50 + $12.68 = $97.18
Step 3: Split 3 ways = $97.18 ÷ 3 = $32.39 each

Final answer: $32.39 per person
```
🔻 Forcing the "show your work" step catches errors before they reach the final answer — same trick that works for humans, works for AI.

💡 Trigger phrases that work well: *"Think step by step,"* *"show your reasoning before answering,"* *"break this down first."*

---

## 🔶 Role-Based / Persona Prompting
**Definition:** Telling the AI to act as a specific character or professional. This shifts its tone, vocabulary, and priorities — same question, very different answer.

➡️ **Example — same question, two personas:**

```
Prompt A: "Act as a strict IELTS examiner. Grade this sentence: 
'I have went to the store yesterday.'"

Output A: "Grammatical error: incorrect past participle usage. 
Should be 'I went to the store yesterday.' This would cost you 
marks in the Grammatical Range and Accuracy band."
```

```
Prompt B: "Act as a friendly conversation partner helping a 
beginner. Respond to: 'I have went to the store yesterday.'"

Output B: "Nice! Just a small tip — we usually say 'I went' 
instead of 'I have went.' Where'd you go shopping?"
```

🔻 Same input sentence, same task, completely different tone and depth — because the *role* changes what the AI prioritizes.

**Template:**
```
Act as a [specific role — strict examiner / patient tutor / 
skeptical investor / senior developer]. [Task]. 
Respond in the tone and priorities that role would actually use.
```

---

## 🔶 Combining All Three — Real Multi-Step Problems

The real power shows up when you stack these techniques together on a problem that actually has multiple moving parts.

### 🎯 Hands-on Problem: The 10-Day Exam Conflict

*Scenario: You have 3 exams in 10 days — Biology (hardest, worth 40% of your grade), Chemistry (medium difficulty), and History (easiest). You have 3 study hours per day.*

➡️ **Weak prompt (what most students write):**
```
"Make me a study schedule for my 3 exams."
```
Generic, doesn't account for difficulty, weight, or your actual time.

➡️ **Advanced prompt (persona + few-shot + chain-of-thought stacked):**
```
Act as an academic strategist who plans schedules based on 
subject difficulty and grade weight. [persona]

Here's an example of how you should structure a day:
Day 1: Biology (1.5 hrs — hardest, highest weight), 
       Chemistry (1 hr), History (0.5 hr — review only) [few-shot]

Now, before creating the schedule, first reason through: 
how many total study hours are available, how they should be 
split across the 3 subjects based on difficulty and weight, and 
which subject needs the most repetition. Show this reasoning, 
then give me the final 10-day schedule as a table. [chain-of-thought]

My exams: Biology (hardest, 40% weight) — day 10. Chemistry 
(medium) — day 7. History (easiest) — day 5. I have 3 hours/day.
```
**Output:**
```
Reasoning:
- Total available hours: 10 days × 3 hrs = 30 hours
- Biology needs the most time (hardest + highest weight) → ~45%
- Chemistry is medium → ~35%
- History is easiest and due soonest, so front-load it, then 
  drop to light review → ~20%

Final Schedule:
| Day | Biology | Chemistry | History |
|-----|---------|-----------|---------|
| 1   | 1.0 hr  | 1.0 hr    | 1.0 hr  |
| 2   | 1.0 hr  | 1.0 hr    | 1.0 hr  |
| 3   | 1.0 hr  | 1.0 hr    | 1.0 hr  |
| 4   | 1.5 hr  | 1.0 hr    | 0.5 hr  |
| 5   | 1.5 hr  | 1.0 hr    | 0.5 hr (exam today) |
| 6   | 1.5 hr  | 1.5 hr    | —       |
| 7   | 1.0 hr  | 2.0 hr (exam today) | — |
| 8   | 2.0 hr  | —         | —       |
| 9   | 2.5 hr  | —         | —       |
| 10  | 1.0 hr (light review, exam today) | — | — |
```
🔻 Notice what made this work: the **persona** set the priorities, the **few-shot example** locked in the format, and **chain-of-thought** forced it to reason about hours before committing to a schedule — three techniques, one clean answer.

### 🎯 Bonus Hands-on: Build Something Real
Reuse the landing page idea from earlier — but this time, have students explicitly use all three techniques:
- **Persona:** "Act as a senior web designer who avoids generic templates."
- **Few-shot:** Give the AI a short example of a headline + subheading pair in the tone they want, before asking for the full page.
- **Chain-of-thought:** "Before writing code, first reason through: who is this product for, what's the one thing the hero section must communicate, and what should the visual mood be. Then build the page."

Same output type as before (a working landing page) — but the *process* now uses everything from this week instead of one-shot prompting.

---

## 🔶 Bringing It All Together

```text
Few-shot   → show examples so the AI copies your format, not guesses it
     ↓
Chain-of-thought → make it reason step by step before answering, catches errors
     ↓
Persona    → assign a role so tone and priorities match the task
     ↓
Stack all three on a real multi-step problem
     ↓
The result: fewer wrong answers, consistent format, and the right tone — 
on the first try, not the fifth
```