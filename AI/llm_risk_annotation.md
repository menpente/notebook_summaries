# Briefing Document: Quantifying the Hidden Risks of Large Language Model Hacking in Text Annotation

## Executive Summary

Large Language Models (LLMs) are rapidly transforming social science research by automating labor-intensive tasks like text analysis and data annotation. However, research demonstrates a fundamental threat to scientific validity termed **LLM hacking**.

LLM hacking occurs when researchers' configuration choices (such as model selection, prompting, or temperature settings) result in **incorrect scientific conclusions** in downstream analyses. This risk stems from the vast degrees of freedom researchers have in configuring LLMs, where even minor variations like prompt paraphrases can dramatically alter outcomes that propagate to statistical conclusions. This issue is distinct from $p$-hacking because LLM hacking operates at the **data generation stage** rather than the analysis stage.

The risk is not merely theoretical; analysis of 13 million LLM labels replicating 37 annotation tasks shows that LLM configuration choices can systematically bias results while maintaining apparent methodological rigor.

---

## Key Findings and Quantification of Risk

The study quantified the risk of LLM hacking by replicating 37 data annotation tasks and testing 2,361 realistic hypotheses.

| Model Type | LLM Hacking Risk (Incorrect Conclusions) |
| :--- | :--- |
| **State-of-the-Art (SOTA) Models** | Approximately **one in three** hypotheses (31% risk). |
| **Small Language Models** | Approximately **half** the hypotheses (50% risk). |
| **Overall** | LLM hacking occurs in 31–50% of cases across all experiments, even with highly capable models. |

### Types of Errors

LLM hacking can introduce various error types, including Type I (false positive), Type II (false negative), Type S (wrong sign), or Type M (exaggerated effect) errors.

*   **Error Dominance:** Type II errors dominate, meaning models more frequently **miss true effects** than fabricate false ones (occurring in 31–59% of cases depending on model size).
*   **Effect Magnitude Distortion:** Even when models correctly identify significant effects, the estimated effect sizes deviate from true values by **40–77% on average**.

### Intentional LLM Hacking Feasibility

Beyond accidental errors, the flexibility of LLM configuration makes **intentional result manipulation shockingly easy**.

*   Using only the tested models and a handful of prompt paraphrases, false positives can be manufactured for **94.4% of null hypotheses**.
*   True effects can be hidden in **98.1% of cases**.
*   Statistically significant effects can be **reversed entirely** (Type S error) in 68.3% of cases with true differences.
*   The distinction between legitimate and manipulated analyses becomes virtually undetectable *post hoc*.

---

## Predictors of Risk and Ineffective Practices

The study established a clear hierarchy of risk factors across all hypothesis-model-prompt combinations.

1.  **Proximity to Significance Thresholds:** This is the **strongest predictor** of LLM hacking. For $p$ values near 0.05, error rates approach 70%.
2.  **Task Characteristics:** Account for 21% of the explained variance.
3.  **Model Performance:** Contributes only 8% of the explained variance.

**Surprisingly Ineffective Practices:**

*   **Prompt Engineering:** Careful prompt design contributes less than 1% of explained variance, challenging the common belief that it can eliminate risks.
*   **Human Agreement:** There is **no correlation** between human inter-annotator agreement and LLM hacking risk, meaning tasks where human experts agree can still yield unreliable LLM-based conclusions.
*   **Statistical Corrections:** Common regression estimator correction techniques are largely ineffective because they face an unavoidable **trade-off between Type I and Type II errors**. For instance, methods that reduce Type I errors can increase Type II errors by up to 60 percentage points.

---

## Mitigation Strategies and Recommendations for Researchers

The findings advocate for a fundamental shift in LLM-assisted research practices. Researchers must move from viewing LLMs as convenient replacements for human annotators to recognizing them as **complex instruments requiring careful calibration and validation**.

### The LLM Data Scale Paradox

*   **Human annotation provides the strongest protection against false positives**.
*   **100 human annotations** often **outperform 100K LLM annotations** for mitigating false positives (achieving error rates of 10%).

### Evidence-Based Guidelines

| Research Context | Primary Concern | Recommendation |
| :--- | :--- | :--- |
| **Novel Discovery Claims** | **False Positives (Type I Errors)** | **Ground-truth-only approaches** provide the only reliable protection. |
| **High Annotation Infeasibility** | **Type II Errors** | Use specific model selection strategies and correction techniques tailored to minimize false negatives. |

### Transparency and Validation

*   Researchers should use LLMs **wisely, not widely**.
*   Essential safeguards against both accidental and deliberate manipulation include adopting **transparency standards**, such as pre-registration of LLM configuration choices and comprehensive reporting of all tested combinations.
*   The current literature reveals insufficient validation practices, with 43% of reviewed papers disregarding model validation despite recommending LLM use. This gap threatens to undermine the credibility of research utilizing these methods.
