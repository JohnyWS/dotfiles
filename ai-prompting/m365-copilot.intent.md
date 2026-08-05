# M365 Copilot Intent

*DISCLAIMER: This is an early version of this document - it needs more iterations and thoughts put into it, but I'm postponing this for now, and leaving this as is, to make sure fewer things are forgotten.*

This document explains the intent behind the M365 Copilot instructions.

It describes what I am optimizing for overall, and why the rules in the instruction file are structured the way they are.

---

## Overall Optimization Goal

The primary goal is to improve the quality and reliability of collaboration with M365 Copilot over time.

For me, this means optimizing for:

- correct understanding over fast answers
- predictable behavior over clever responses
- reviewability over one-off usefulness
- smooth execution when intent is clear
- deliberate alignment when intent is ambiguous or high-impact

The intent model is designed to manage risk, not to maximize verbosity or caution by default.

---

## Intent Is About Outcomes, Not Wording

Intent is not the literal text of a prompt.

Intent includes:
- what outcome is actually useful
- how much uncertainty exists
- how costly a misunderstanding would be
- whether the output is disposable or durable

The instructions respond to intent risk, not prompt length alone.

---

## When Alignment Is Worth the Cost

Slowing down to clarify intent is valuable when:

- multiple interpretations are plausible
- trade-offs or decisions are involved
- the output will be used as a reference or artifact
- I have signalled that a previous response missed the mark

In these cases, alignment effort improves outcomes.

---

## When Execution Should Be Fast

Direct execution is preferred when:

- the task is deterministic or closed-form
- there is a single reasonable expected result
- I ask a short follow-up in context
- the cost of misinterpretation is low

In these cases, additional ceremony adds friction without increasing quality.

---

## Follow-Ups and Context

Follow-up questions inherit context by default.

They are treated as continuations unless I explicitly signal misalignment.

This preserves conversational flow and avoids unnecessary repetition.

---

## Artifacts vs Conversations

Intent also determines durability:

- conversational outputs support thinking and decisions
- artifacts are meant to live on, be shared, or reused

Only artifact intent justifies creating durable documents.

---

## Why This Is Explicit

Making intent handling explicit:

- reduces unpredictable AI behavior
- makes trade-offs visible and reviewable
- allows adaptation across different AI systems
- supports continuous improvement rather than static rules
