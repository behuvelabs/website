<!--
  TEMPLATE INSTRUCTIONS
  =====================
  1. Replace everything in [BRACKETS] with real content.
  2. Choose a post-type badge: Paper Review · Project · Explainer · Notes
  3. For paper reviews: keep the Paper Card section. Delete for others.
  4. For project posts: replace the Paper Card with a short callout summarizing what you built.
  5. Section headers (##) should be short uppercase-style labels — they function as navigation anchors, not titles.
  6. Delete these comments before publishing.
-->

**[Post Type]** · [Month YYYY] · [Your Name]

# [Post Title: The Main Claim or Finding]

[One or two sentences. What does this post cover and why does it matter?
Think of this as the abstract — someone should know whether to keep reading after this line alone.]

---

## Paper Card

<!-- For paper reviews. Delete this section for project posts. -->

| | |
|---|---|
| **Paper** | [Full paper title] |
| **Authors** | [Author names] |
| **Venue** | [Conference / journal / year — e.g., USENIX Security 2023] |
| **Link** | [PDF / arXiv / ACM DL link] |
| **TL;DR** | [One sentence verdict. What's the thing to take away?] |

---

## Background

Set the stage. What problem does this paper address and why does it exist?
What should the reader already know, and what's the one key thing they
might be missing that makes this hard? Keep it tight — one or two paragraphs.
Assume the reader is a CS undergrad or early grad student, not a specialist.

For a paper review, place the work in context: what existed before it
and what gap it was designed to fill. For a project post, describe the
motivation — what you were trying to build and why.

---

## The Core Idea

State the central claim or design in one sentence. Then unpack it.
This is the heart of the post — spend the most words here.
Use concrete examples instead of abstract descriptions wherever possible.

```c
// Example: minimal seccomp-bpf filter allowing only read/write/exit
struct sock_filter filter[] = {
    BPF_STMT(BPF_LD | BPF_W | BPF_ABS, offsetof(struct seccomp_data, nr)),
    BPF_JUMP(BPF_JMP | BPF_JEQ | BPF_K, __NR_read,  2, 0),
    BPF_JUMP(BPF_JMP | BPF_JEQ | BPF_K, __NR_write, 1, 0),
    BPF_STMT(BPF_RET | BPF_K, SECCOMP_RET_KILL),
    BPF_STMT(BPF_RET | BPF_K, SECCOMP_RET_ALLOW),
};
```

Always follow a code block with an explanation. What does this do?
What's important about it? What would a reader miss if they skimmed it?

> **Key insight:** [One sentence capturing the most important thing in this section.
> Use callouts sparingly — they lose force if overused.]

---

## What's Interesting

This section separates a review from a summary. What didn't you expect?
What was clever? What was a weird tradeoff? What made you go back and re-read a section?

For a project post, this becomes "What was harder than expected" or
"What I got wrong the first time." Be honest. Posts that document
confusion are more useful than posts that only document conclusions.

---

## Evaluation

<!-- Optional. Use for paper reviews when the eval is significant, or for project posts when you have benchmark data. -->

How did they measure success? What were the workloads, baselines,
and metrics? If there's a key table or figure from the paper,
describe it in your own words here.

| Approach | Overhead | Coverage | Notes |
|---|---|---|---|
| `seccomp-strict` | <1% | 4 syscalls | Too restrictive for most workloads |
| `seccomp-bpf` | ~2–5% | Configurable | Flexible; policy complexity is manual |
| [This paper] | [X%] | [Y syscalls avg] | [Key result] |

---

## Limitations and Open Questions

Every paper has limits. Every project has unsolved parts. Name them.
This is where you show critical reading rather than summarizing.
A few honest sentences here are worth more than a paragraph of praise.

- What does this approach not handle?
- What assumption might not hold in practice?
- What would you want to see in follow-up work?

> **Caveat:** [Something the reader should know before applying this to their own work.]

---

## What This Means for Our Work

<!-- Rename freely: "Takeaways", "Why We Read This", etc. Optional but high value — connects the post to Behuve's research. -->

How does this connect to something we're building or thinking about?
This section is what makes the post ours rather than just another summary.
Be specific — a vague "this is relevant" is worse than nothing.
