# MentorCraft

**A framework for evolving LLM agents through iterative mentorship and workflow refinement.**

---

## The Problem

Every conversation with an AI agent starts from scratch. No matter how much time you spend teaching an agent your codebase conventions, your design patterns, or your reasoning style—it forgets everything the moment the session ends.

Humans don't work this way. When you mentor a junior engineer, they absorb your feedback through repeated interaction. They learn that you prefer composition over inheritance, that you have a custom blob storage abstraction, that you always consider edge cases from production incidents. They dream about these patterns and internalize them.

LLMs dream every two years (when a new version trains on updated data), not every night.

**What if your agent could learn from working with you daily—and actually get better over time?**

---

## The MentorCraft Approach

MentorCraft turns your normal development workflow into a continuous fine-tuning pipeline. The key insight: **your daily iterations with an agent already contain the signal needed to adapt it to your workflow.**

You propose a feature. The agent suggests an approach. You refine it based on context the agent can't know—your codebase conventions, battle-tested patterns, domain nuance. That refinement is valuable training data—**if you capture it systematically**.

### The Practice Change

MentorCraft works by establishing a simple workflow discipline:

1. **Initial Commit**: When you conceive a feature, commit a brief description (even if rough)
   - A few paragraphs, maybe half a page
   - Your off-the-cuff ideas about approach
   - No need to be polished

2. **Iterate Normally**: Work with your agent to refine the design
   - The agent proposes approaches
   - You course-correct based on domain knowledge
   - Together you arrive at a robust solution

3. **Final Commit**: Commit the polished design doc + tested implementation
   - Includes the "why" behind decisions
   - Documents tradeoffs and learnings
   - Captures what you discovered during implementation

This discipline creates clear "before/after" snapshots in your git history. Tooling can then automatically extract training pairs—no manual curation needed.

---

## The Pipeline

### 🧱 Inputs

- **Initial Concept**: Your rough feature request or design sketch
- **Final Design**: The refined solution after iteration, including rationale and implementation

### ⚙️ Processing

1. **Scan Git History**: Automatically detect initial-vs-final checkpoint pairs in commits or PRs
2. **Extract Pairs**: Match each "vague request" to its corresponding "refined output"
3. **Annotate** (optional): Tag with topic, difficulty, or flag "surprising" iterations for prioritized learning
4. **Generate Training Data**: Create JSONL or structured records for fine-tuning

### 📦 Output

- Training pairs suitable for:
  - **LoRA fine-tuning**: Lightweight daily weight updates as new pairs accumulate
  - **Retrieval-augmented memory**: Feed past decisions into agent context
  - **Validation sets**: Measure whether adapted models improve on held-out examples

### 🔄 Continuous Adaptation

As you accumulate training pairs, regenerate LoRA weights daily or weekly. The agent evolves alongside your codebase, learning your patterns the same way a junior engineer absorbs design intuition through code review.

---

## Example Training Pair

```json
{
  "input": "We need a way to track user login events",
  "output": "I added a new `audit_log` table with a `log_user_event(user_id, event_type)` helper. This keeps auth logic clean and makes future event tracking extensible. We considered embedding events in the users table but rejected it because: (1) unbounded growth, (2) different retention policies for compliance, (3) easier to add analytics later without touching core auth."
}
```

Notice the output doesn't just provide a solution—it explains **why**, documents **rejected alternatives**, and captures **reasoning tradeoffs**. This is the quality of training signal that comes from real iteration.

Open question: We'll need to experiment with what these training pairs should look like. For example, perhaps the second half of the above training pair should mention the tradeoff areas and make recommendations for the choices, rather than actually making all the decisions right there.

---

## Why This Works

### Not Just RAG, Not Just Fine-Tuning

- **RAG** gives agents access to documentation but doesn't teach *judgment*
- **Generic fine-tuning** requires massive datasets and doesn't capture your unique workflow
- **MentorCraft** creates domain-specific training pairs from your actual iteration patterns, then uses lightweight LoRA to adapt the agent to your reasoning style

### It's Bidirectional Mentorship

The name "MentorCraft" reflects a key insight: sometimes you mentor the agent, sometimes the agent mentors you.

When working in a language you rarely touch (Elixir, Gleam), the agent knows idioms you don't. When designing systems you've built dozens of times over 30 years, you know failure modes that aren't documented anywhere online.

Like any good partnership, you cover each other's blind spots. MentorCraft captures this bidirectional learning so the agent gets better at amplifying your strengths while you benefit from its breadth.

---

## Validating the Hypothesis

The core claim: fine-tuning on your iteration patterns makes agents better at your work. This is testable:

1. **Extract a corpus** of training pairs from past projects
2. **Split into train/hold-out** sets (e.g., 80/20)
3. **Fine-tune** a model on the training pairs using LoRA
4. **Compare** base model vs. adapted model on held-out initial concepts
5. **Measure**: Does the adapted model produce designs closer to your actual final solutions?

Preserve a subset of hold-out examples for longitudinal re-testing to track drift as the model and data evolve.

---

## How It Works in Practice

### Phase 1: Establish the Discipline (Week 1)

- Start committing initial feature concepts before iteration
- Work normally with your agent
- Commit final designs with reasoning/tradeoffs documented

### Phase 2: Build the Pipeline (Week 2-3)

- Create tooling to scan git history for checkpoint pairs
- Extract and validate training pairs (aim for 20-50 to start)
- Tag pairs by topic/difficulty

### Phase 3: First Adaptation (Week 4)

- Fine-tune using LoRA on accumulated pairs
- Test adapted model on new features
- Compare quality: Does it propose solutions closer to your style?

### Phase 4: Continuous Evolution (Ongoing)

- Keep committing checkpoint pairs as you work
- Regenerate weights weekly/daily as corpus grows
- Measure improvement on held-out validation set

---

## Potential Extensions

Once the core pipeline works, consider:

- **🧑‍🎓 Mentor Feedback Scoring**: Quantify how much each iteration diverged from the initial attempt (prioritized experience replay)
- **🧬 Reflection Loops**: Let the agent critique its own past outputs to identify failure patterns
- **🔍 Tool Usage Recording**: Capture which APIs/abstractions were used in final solutions
- **🕸️ Session DAGs**: Graph multi-step reasoning flows across complex features
- **📊 Drift Detection**: Monitor if the agent's suggestions regress toward generic patterns over time

---

## 🚧 Status

MentorCraft is currently **experimental**. The README you're reading is the first formal articulation of these ideas.

Next steps:
- [ ] Implement git history scanner to extract checkpoint pairs
- [ ] Create initial training corpus from past projects
- [ ] Run first LoRA fine-tuning experiment
- [ ] Validate on held-out design tasks

**Contributions, feedback, and experiment results welcome!**

---

## Philosophy

MentorCraft assumes that:

* **You are not always the best explainer at first pass** — Real solutions emerge through iteration
* **The refined solution reflects real tradeoffs and domain nuance** — Not just "what" but "why" and "why not"
* **These improvements are worth teaching to your agent** — Repeated patterns should compound, not reset

It's an attempt to simulate how junior engineers learn:

> *Observe. Draft. Review. Iterate. Reflect. Improve.*

The question is: can agents do the same?

---

## License

MIT License - See LICENSE file for details
