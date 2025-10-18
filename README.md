# MentorCraft

**A framework for evolving LLM agents through iterative mentorship and workflow refinement.**

MentorCraft is an experimental approach to AI-agent development where the human is not just the user — they are the mentor. It enables a feedback loop in which LLM agents improve over time by learning from real-world design interactions, much like a junior engineer learning from daily design reviews.

---

## ✨ Concept

Modern LLMs are powerful, but each session typically starts from scratch. MentorCraft challenges that paradigm.

> Instead of "starting fresh," what if your agent could reflect on yesterday's work — and get better the same way you did early in your career?

MentorCraft imagines a future where agents grow in capability and alignment through consistent exposure to:

- **Your workflow**
- **Your design preferences**
- **Your unique reasoning patterns**

MentorCraft is not just about tool use — it's about **crafting judgment**. It bridges the gap between one-off interactions and long-term mentorship by generating training examples from real-world collaboration.

---

## 🔁 The MentorCraft Pipeline

MentorCraft defines a minimal pipeline that automatically generates high-quality training pairs during your normal workflow. These pairs can be used for fine-tuning or retrieval-augmented learning.

### 🧱 Inputs

- **Initial Prompt or Feature Request**: A vague or under-defined user request (e.g., "Add auth to the API")
- **Final Design or Outcome**: The result after refinement, including design rationale, diagrams, or code

### ⚙️ Processing

1. **Capture Sessions**: Store initial prompts and resulting design/code
2. **Pair Examples**: Match each "vague request" to the corresponding "refined output"
3. **Optionally Annotate**: Add reasoning, notes, or decision tradeoffs (optional, but helpful)
4. **Tag & Store**: Categorize by topic, difficulty, or system area

### 📦 Output

- JSONL or Markdown records for each training pair
- Useable as:
  - LoRA fine-tuning data
  - Retrieval docs in a memory system
  - Demos for agent validation

---

## 📚 Example Pair

```json
{
  "input": "We need a way to track user login events",
  "output": "I added a new `audit_log` table with a `log_user_event(user_id, event_type)` helper. This keeps auth logic clean and makes future event tracking extensible."
}

Here's a structured `README.md` draft for your GitHub repo, **MentorCraft**. The format is clean, documented, and ready to evolve.

---

````markdown
# MentorCraft

**A framework for evolving LLM agents through iterative mentorship and workflow refinement.**

MentorCraft is an experimental approach to AI-agent development where the human is not just the user — they are the mentor. It enables a feedback loop in which LLM agents improve over time by learning from real-world design interactions, much like a junior engineer learning from daily design reviews.

---

## ✨ Concept

Modern LLMs are powerful, but each session typically starts from scratch. MentorCraft challenges that paradigm.

> Instead of "starting fresh," what if your agent could reflect on yesterday's work — and get better the same way you did early in your career?

MentorCraft imagines a future where agents grow in capability and alignment through consistent exposure to:

- **Your workflow**
- **Your design preferences**
- **Your unique reasoning patterns**

MentorCraft is not just about tool use — it's about **crafting judgment**. It bridges the gap between one-off interactions and long-term mentorship by generating training examples from real-world collaboration.

---

## 🔁 The MentorCraft Pipeline

MentorCraft defines a minimal pipeline that automatically generates high-quality training pairs during your normal workflow. These pairs can be used for fine-tuning or retrieval-augmented learning.

### 🧱 Inputs

- **Initial Prompt or Feature Request**: A vague or under-defined user request (e.g., "Add auth to the API")
- **Final Design or Outcome**: The result after refinement, including design rationale, diagrams, or code

### ⚙️ Processing

1. **Capture Sessions**: Store initial prompts and resulting design/code
2. **Pair Examples**: Match each "vague request" to the corresponding "refined output"
3. **Optionally Annotate**: Add reasoning, notes, or decision tradeoffs (optional, but helpful)
4. **Tag & Store**: Categorize by topic, difficulty, or system area

### 📦 Output

- JSONL or Markdown records for each training pair
- Useable as:
  - LoRA fine-tuning data
  - Retrieval docs in a memory system
  - Demos for agent validation

---

## 📚 Example Pair

```json
{
  "input": "We need a way to track user login events",
  "output": "I added a new `audit_log` table with a `log_user_event(user_id, event_type)` helper. This keeps auth logic clean and makes future event tracking extensible."
}
```

---

## 🧠 Philosophy

MentorCraft assumes that:

* **You are not always the best explainer at first pass**
* **The refined solution reflects real tradeoffs and domain nuance**
* **These improvements are worth teaching to your agent**

It’s an attempt to simulate the way junior engineers learn:

> *Observe. Draft. Review. Iterate. Reflect.*

---

## 🔧 Potential Extensions

* 🧑‍🎓 **Mentor Feedback Scoring**: Score how well an agent’s attempt compares to your final solution
* 🧬 **Reflection Loops**: Let the agent critique its own past outputs
* 🔍 **Tool Usage Recording**: Record which APIs or tools were used in the final solution
* 🕸️ **Session DAGs**: Graph the flow of reasoning across multi-step sessions

---

## 🚧 Status

MentorCraft is currently experimental. Contributions and feedback welcome!

---
