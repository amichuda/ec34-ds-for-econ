# Problem Set 4: Answer Key

This document describes what a strong answer looks like for each part. It does not contain runnable code. Actual numerical results will vary across students depending on model version, API behavior, and random seeds — the grading rubric rewards correct reasoning and method over hitting specific numbers.

---

## Setup

A strong answer defines `classify_statement` as a clean, reusable function. The key design decisions are:

**System prompt**: The prompt must be precise enough to force a single-word output. A good prompt looks something like:

> "You are a monetary policy expert. Classify the following Federal Reserve statement as exactly one of: hawkish, dovish, or neutral. Hawkish means the statement signals tighter monetary policy (higher rates, reduced accommodation). Dovish means it signals looser monetary policy (lower rates, more accommodation). Neutral means neither. Respond with only one word: hawkish, dovish, or neutral."

Common mistakes to flag:
- A vague prompt that does not define the three categories, causing the model to use idiosyncratic interpretations
- No enforcement of single-word output, causing the model to return explanations that need fragile string parsing
- Hard-coding the API key anywhere in the notebook

The function should catch API errors gracefully and should accept `temperature` as a parameter so it can be reused across all parts.

---

## Part 1: Baseline Performance

**What to expect**: A well-prompted GPT-4o or GPT-4 at `temperature=0.0` should achieve reasonably high accuracy — likely 8/10 or 9/10 on this dataset. The most challenging statements are the neutral ones, since "neutral" requires the model to withhold a judgment rather than detect a clear signal.

**A good confusion matrix** will have most mass on the diagonal. The most common off-diagonal error is classifying "neutral" statements as "hawkish" or "dovish" — the model tends to find a signal where human experts saw ambiguity.

**A strong written answer** explains *why* the model makes the errors it does. For example:

- Statement 2 ("Inflation remains elevated...") is labeled "hawkish" in the ground truth, but the statement itself is a factual observation, not a policy signal. A student who notices this and discusses the ambiguity of the ground truth itself is demonstrating strong critical thinking.
- Statements that mention "strengthening labor markets" may be labeled neutral by human experts but hawkish by the model, because tight labor markets are typically a precursor to rate hikes. Both interpretations are defensible.

The key takeaway students should articulate: even at its best setting, the LLM is not a perfect substitute for a trained human coder, and agreement with ground truth depends heavily on how contested the categories are.

---

## Part 2: The Non-Determinism Problem

**What to expect at temperature=0.7**: Consistency rates will vary across statements. Statements with unambiguous language (e.g., "raise the target range by 75 basis points") will be classified consistently across nearly all 20 calls. Statements that are genuinely ambiguous will show lower consistency — perhaps 60–80% agreement with the modal response.

The distribution of consistency rates will be bimodal: many statements cluster near 100% consistency, while a few ambiguous ones cluster lower.

**At temperature=0.0**: Most API providers will return identical results for every call, giving consistency rates of 100% per statement. Students should note that this is not guaranteed by the API specification, but is typical in practice for current OpenAI models.

**A strong answer to question 5** identifies the core problem clearly: a researcher using a single API call per statement at temperature=0.7 has no way to know whether any given classification is the modal (most-likely) response or an outlier. If 20% of statements have a 25% chance of flipping to a wrong label on any given call, then a dataset of 10,000 statements will contain ~2,500 mislabeled observations — with no obvious way to detect them. This is a sampling problem: the researcher has drawn one sample from a noisy distribution, and they cannot know where on that distribution they landed.

**A practical implication** worth mentioning: running each classification multiple times and taking the majority vote substantially reduces this noise. This is sometimes called "ensemble querying" and is analogous to running a regression on multiple imputed datasets.

---

## Part 3: The Prompt Sensitivity Problem

**Four meaningfully different prompts** should vary along real dimensions. Here are examples of what each might look like at a high level:

- **Prompt A (zero-shot, minimal)**: Just the task and the three category names, no definitions.
- **Prompt B (zero-shot, with definitions)**: Defines hawkish and dovish explicitly in economic terms.
- **Prompt C (few-shot)**: Provides 2–3 labeled examples before asking for a classification.
- **Prompt D (role-framed)**: Asks the model to act as a central bank analyst before classifying.

**What to expect in the pairwise agreement matrix**: Prompts B and C (with definitions and examples) will tend to agree with each other more than with Prompt A. This is because additional context anchors the model's interpretation of the category boundaries. Prompt D may agree or disagree depending on how the role framing interacts with the model's priors.

A reasonable agreement matrix might show pairwise agreement ranging from 70% (Prompt A vs. Prompt C) to 90% (Prompt B vs. Prompt C). Students should display this as a symmetric 4×4 matrix with 1.0 on the diagonal.

**Accuracy across prompts**: Few-shot prompts (C) tend to outperform zero-shot prompts (A) on small, ambiguous datasets like this one. The gap might be 1–2 statements out of 10. Students should not over-interpret small differences on a 10-statement dataset.

**A strong answer to question 4** makes the replicability point explicit: two researchers who independently write prompts for the same task may get systematically different results, even if both prompts appear reasonable. Since the choice of prompt is rarely justified or reported in papers, readers cannot know which prompt was used or how sensitive the results are to that choice. This is analogous to researcher degrees of freedom in specification searching.

---

## Part 4: The Bias Problem

**What to expect**: The LLM will likely assign slightly lower average scores to version B candidates (Black- and Latino-associated names) than to version A candidates (white-associated names) across most pairs. The direction of the gap should be consistent even if the magnitude is small.

This finding mirrors results from the existing literature on LLM bias — multiple published audit studies have found that models trained on internet text encode the same hiring biases present in human behavior.

**Means and confidence intervals**: With 30 draws per version, confidence intervals will be wide. Means for both groups will likely fall in the 6–8 range. A typical gap might be 0.3–0.8 points on a 10-point scale. Students should not expect huge, dramatic gaps — subtle but consistent gaps are the realistic and more insidious finding.

**T-tests**: For individual pairs, t-tests may or may not reject at conventional significance levels — the sample size (n=30 per group) is small. Students should recognize this and not over-claim based on individual pairs. The more convincing analysis is the average gap across all 5 pairs, which pools the evidence. A student who notes that the consistent *direction* of the gap across pairs is itself evidence of systematic bias (even if no single pair clears p<0.05) is demonstrating sophisticated statistical reasoning.

**A strong answer to question 5** connects to the economics literature. If a researcher uses the LLM to score applicants in a wage study, the bias will manifest as a spurious negative coefficient on a "Black name" dummy even in the absence of any real productivity differences. This would cause the researcher to *overestimate* labor market discrimination — they would be measuring LLM bias, not market bias. Alternatively, if they use the scores as a control variable, they would introduce collider bias. The key point is that LLM-derived variables are not neutral measurements: they carry the model's priors about the world.

**A nuance worth crediting**: Students who question whether the "true" scores should be identical across all pairs (i.e., whether the ground truth is that no name should change the score) are engaging seriously with the audit design. The answer is yes — in this design, the bios are constructed to be identical in all productivity-relevant dimensions, so any score difference is definitionally attributable to name.

---

## Part 5: The Econometric Cost of Measurement Error

**The analytical result**: For a binary $X^*$ drawn with probability 0.5, $\text{Var}(X^*) = 0.25$. With a misclassification rate $p$, the mismeasured variable $\tilde{X}$ has $\text{Var}(u) = p(1-p) \cdot 4 \cdot \text{Var}(X^*) = p(1-p)$... 

Actually, the cleaner way to derive the attenuation factor for binary variables with symmetric misclassification is:

$$\text{plim}(\hat{\beta}) = \beta_{true} \cdot (1 - 2p)$$

So at $p = 0.0$, the estimate is $3.0$. At $p = 0.10$, it is $3.0 \times 0.8 = 2.4$. At $p = 0.20$, it is $3.0 \times 0.6 = 1.8$. At $p = 0.40$, it approaches $3.0 \times 0.2 = 0.6$. At $p = 0.50$, the estimate collapses to zero (the mislabeled variable is pure noise).

**What the plot should look like**: The average estimated coefficient starts near 3.0 at $p = 0.05$ and falls monotonically as $p$ increases, approaching 0 near $p = 0.5$. The dashed horizontal line sits at $\hat{\beta} = 3$. The curve should be close to linear in this range, consistent with the $(1 - 2p)$ formula above.

**A strong answer to question 5** uses the Part 1 misclassification rate to locate the class on the attenuation curve. If the model achieved 80% accuracy in Part 1, the misclassification rate is 20%, implying attenuation to about 60% of the true coefficient. A student who writes something like: "Our LLM misclassified 20% of statements, which means a researcher using these labels would estimate a coefficient of about 1.8 instead of the true 3.0 — a 40% underestimate — without any indication that something is wrong" has understood the point of the exercise.

**A deeper point worth crediting**: Classical measurement error assumes the error $u$ is independent of $X^*$. The errors we found in Parts 1–3 are *not* classical — they are systematically related to the content of the text (ambiguous statements get mislabeled more often). This means the true attenuation bias is more complicated than the formula suggests, and could be non-random in ways that bias coefficients in unpredictable directions, not just toward zero.

---

## General Grading Notes

- Students who correctly implement the API calls and simulations but write shallow interpretations should receive partial credit in the discussion components.
- Students who write strong interpretations but make implementation errors should receive partial credit in the code components — the goal of the problem set is conceptual understanding, not API debugging.
- The consistent theme across all five parts is: **LLM outputs are not measurements, they are samples from a distribution**. Students who internalize this and apply it throughout their answers should be rewarded even if their specific numbers differ from expected ranges.
- Deduct points for any notebook that hard-codes an API key, even in a comment.
