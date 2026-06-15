---
name: paper-reading
description: >
  Use this skill whenever a user wants to deeply read, analyze, understand, or summarize a research paper, preprint, or academic article. Triggers include: sharing an arXiv link or PDF, pasting a paper title or abstract and asking for a breakdown, saying "help me read this paper," "summarize this paper," "explain this paper," "analyze this paper," "what does this paper say," "walk me through this," or anything that implies the user wants to extract deep understanding from a piece of academic work. Also trigger when the user asks you to critique, attack, or find weaknesses in a paper, or when they want follow-up research ideas inspired by a paper. This skill applies across all technical domains — machine learning, NLP, computer vision, systems, biology, physics, economics, etc. The goal is not passive summarization but active reconstruction of the author's reasoning, honest critique, and generative thinking.
---

# Paper Reading Skill

## Preparation

First, identify the paper and obtain the full text.

The user may provide:

* A URL, such as arXiv, ACL Anthology, OpenReview, PapersWithCode, a publisher page, or a lab page
* A PDF or file attachment
* A paper title
* A title plus abstract

If the user provides a URL, fetch the full paper before writing the analysis. If the user provides only a title, search the web for the canonical version. Prefer arXiv or the official venue page when available. If the user provides only an abstract and the full paper cannot be found, say that the analysis is provisional and explain which parts cannot be verified.

Do not rely on the abstract alone for a full paper reading. The method, experiments, figures, tables, limitations, and appendices often contain the real contribution and the real failure modes.

After getting the paper, read it once end to end before writing. Cover the abstract, introduction, related work, method, experiments, conclusion, and appendices when relevant. Identify three things before producing the final analysis:

1. The central technical claim.
2. The key experiment or argument that supports it.
3. The strongest baseline or prior work comparison.

If the novelty is unclear, search for 2 to 3 closely related papers before summarizing. Use this to calibrate the paper's contribution. Do not invent related work or claim novelty without evidence.

---

## Output structure

Your task is to produce a clear, readable, detailed, and technically accurate paper analysis.

Use the following 12 sections in order. The order matters: background before method, method before experiments, understanding before critique. Do not skip any section except Section 6, which may be skipped if the paper has no meaningful formal math.

Write mostly in paragraphs. Use bullet points only when they improve clarity, such as in experiment summaries or implementation steps. Avoid decorative transitions, exaggerated praise, and vague claims. Each sentence should add information.

---

### § 1 — Research problem and importance

State the research question the paper tries to answer. Be specific about the task, domain, failure mode, or gap.

Then explain why the problem matters. What capability, system behavior, product use case, scientific understanding, or evaluation problem would improve if this were solved? If the importance is not obvious, do a small amount of background research to calibrate the context.

Separate the authors' stated motivation from your own broader-context interpretation.

---

### § 2 — Prior work and limitations

Explain how this problem was handled before this paper.

Name the most relevant prior methods, systems, datasets, or theoretical results. Briefly state what they can already do. Then explain why they are insufficient for the problem this paper targets.

Avoid the weak framing `prior work did not consider X`. Explain why X was missing. Was it technically difficult, too expensive, overlooked, based on an assumption that later failed, or not recognized as a problem at the time?

---

### § 3 — Reconstructing the authors' thought process

Before explaining the method, reconstruct a plausible path that could have led to the paper's idea.

Use only what would have been knowable before this paper: prior methods, known failure cases, empirical observations, theoretical hints, and neighboring techniques. Do not use the paper's own contribution as the starting point.

Explain:

* What failure or strange observation would have bothered an expert in this area.
* What simple fixes a researcher might have tried first, and why they would likely be insufficient.
* What shift in framing, assumption, objective, or representation makes the paper's idea possible.
* Which parts of this reconstruction are stated by the authors, and which parts are your own reasonable interpretation.

Be explicit about uncertainty. Use phrasing like `one plausible path is` or `the paper suggests this motivation, but does not fully spell it out` when needed.

---

### § 4 — Core intuition

Explain the paper's core intuition in 2 to 4 sentences.

Remove the formalism, engineering details, ablations, and benchmark numbers. State the one idea that makes the method work, or that the authors believe makes it work. If the intuition cannot be stated in plain language, continue reasoning until it can.

---

### § 5 — Method and full pipeline

Explain the method as an end-to-end pipeline.

Start with the input. Then walk through each computation, decision, model component, training step, inference step, or evaluation step. End with the output.

Use a concrete example when possible. The example should be realistic and should not introduce fake evidence. Trace the example through the method so the reader can see what each part is doing.

Make clear:

* What each component does.
* Why the component is needed.
* What alternative design could have been used.
* Which parts are conceptually simple.
* Which parts carry the real technical difficulty.

---

### § 6 — Mathematical foundations

Skip this section only if the paper has no substantial formal math.

If the paper contains important derivations, proofs, probabilistic models, optimization objectives, or theoretical claims, explain them step by step. Assume the reader is smart but not specialized in this exact subfield.

Define the variables and assumptions. Explain why each equation follows from the previous one. Connect the math back to the intuition in Section 4. If there is a trick, relaxation, approximation, or hidden assumption, name it and explain why it matters.

If the paper is mainly empirical or system-oriented, say that there is no central formal derivation and move on.

---

### § 7 — Experimental design and results

Explain how the paper tests its main claims.

For each major claim, use this logic:

* What question is the experiment asking?
* What data, baseline, metric, and control does it use?
* What result does the paper report?
* Does the result actually answer the question, or does it leave another explanation open?

Do not turn this section into a score dump. The goal is to understand the experimental logic, not to memorize benchmark numbers. Include numbers only when they are central to the claim or useful for judging effect size.

---

### § 8 — Takeaways

Summarize what the paper adds to the field.

Frame the takeaways as what the reader now knows that they did not know before: a new capability, a new failure mode, a new method, a new evaluation, a cleaner framing, or a surprising empirical fact.

Be specific about who should care: model builders, interpretability researchers, benchmark designers, domain scientists, product teams, or theorists.

---

### § 9 — Most vulnerable assumption

Identify the single most important assumption behind the paper.

This is not a list of limitations. Find the assumption whose failure would most seriously damage the paper's main contribution.

Explain why the assumption might fail in practice. Then state what evidence the paper provides for it, what evidence is missing, and what would make you more confident.

---

### § 10 — Minimum reproducible experiment

Design the smallest experiment that could test the paper's central claim within about one week and a normal research compute budget.

Specify:

* What data to use.
* What to implement.
* What to measure.
* What baseline to compare against.
* What outcome would support the claim.
* What outcome would weaken or refute it.

Prefer an experiment that tests the core idea directly rather than reproducing the full system.

---

### § 11 — Strongest counterargument

Design the strongest serious attack on the paper.

Do not focus on typos, missing minor ablations, or vague complaints. Give an experiment, theoretical objection, alternative explanation, or class of real-world cases that would genuinely challenge the method.

A good counterargument should either explain the reported results in another way or identify conditions under which the method should predictably fail.

---

### § 12 — Follow-up research idea

Propose one non-incremental research idea inspired by the paper.

Do not suggest a trivial extension like applying the method to another dataset, adding one module, or scaling the same pipeline. Look for a new framing, objective, connection to another area, or evaluation setup that could open a different direction.

Before proposing the idea, calibrate the research taste when possible. Look at high-impact or award-level work in the relevant venue or area only if doing so would help judge what makes a problem important. Do not pretend that a direction is novel or high-impact without evidence.

Ground the idea in three parts:

1. The limitation or unmet need that motivates it.
2. The neighboring method, literature, or technical tool it could draw from.
3. The first experiment that would test whether the direction is promising.

Clearly separate what is already known from what you are proposing.

---

## Source discipline

Throughout the analysis, distinguish four kinds of claims:

* **Paper states**: the authors explicitly claim, show, or report this.
* **Prior work establishes**: this is documented in existing literature. Cite it when possible.
* **Reasonable inference**: this follows from the paper's evidence, but the authors do not explicitly state it.
* **Speculation**: this is a hypothesis or research guess, not directly supported by the paper.

Never present speculation as fact. Never present an inference as something the paper proved. If you are unsure which category a claim belongs to, say so.

When citing the paper or related work, cite the source that actually supports the statement. Do not cite a paper merely because it is topically related.

---

## Style

Use American English.

Write with the technical directness associated with Andrej Karpathy and the structural discipline associated with Kaiming He. This means:

* Start from a concrete technical situation.
* Name the problem directly.
* Show the failure mode before explaining the solution.
* Prefer specific nouns, actions, and numbers over generic praise.
* State the claim before the evidence.
* Use structure to make the reasoning easy to follow.
* Keep uncertainty visible.
* Do not over-polish the prose until it loses human texture.

Avoid filler phrases such as `it is worth noting`, `it is important to mention`, `in conclusion`, `furthermore`, and `this paper sheds light on`. Avoid hype words such as `groundbreaking`, `game-changing`, `robust`, and `seamless` unless the paper itself supports that exact claim.

Avoid overusing em dashes, scare quotes, semicolons, and parentheses. Keep the writing clean and readable.

The default output language is English. Preserve technical terms when they are standard in the field, such as attention, fine-tuning, ablation, retrieval, policy gradient, representation, or benchmark.
