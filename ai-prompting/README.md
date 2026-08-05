# AI Prompting

This folder captures my continued improvement in working with AI models over time.

Rather than focusing on individual prompts, it contains structured artifacts that document:

- how I configure and instruct different AI systems
- why those instructions are shaped the way they are
- how my understanding of effective AI collaboration evolves

The goal is to make learning explicit, reviewable, and transferable.

---

## Structure

Each AI system added to this folder is represented by two files:

- ai-system.instructions.md
- ai-system.intent.md

---

## Instructions

Files named "*.instructions.md" contain raw instruction text.

They are intended to be:
- copied directly into the configuration or instruction interface of an AI system
- treated as operational behavior rules
- updated as understanding improves

These files define what the AI should do.
They do not explain why the rules exist.

---

## Intent

Files named "*.intent.md" explain the intent behind the instructions.

They describe:
- what I am optimizing for overall
- how I reason about intent, alignment, and risk
- why specific rules exist in the instruction file
- which trade-offs are intentional

These files are explanatory and reflective.
They exist to support review, adaptation, and learning.

---

## Adding Other Models

Additional AI systems can be added using the same pattern:

- <system>.instructions.md
- <system>.intent.md

The intent files are expected to evolve slowly.
The instruction files may change more frequently as models and tooling change.
