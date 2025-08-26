# Phase 1 — Project 2: Sentiment Classifier (Zero-shot vs Few-shot)

This project practices **zero-shot vs few-shot prompting** for text classification into Positive, Negative, or Neutral.

---

## Prompts Used

### Zero-shot Prompt
You are a strict sentiment classifier. Labels: Positive, Negative, Neutral. Rules: - If mixed/unclear → Neutral. - Output JSON ONLY: {"label": "...", "confidence": 0-1} Classify each line separately: 1) "This service is amazing!" 2) "It’s okay, could be faster." 3) "Total waste of time." 4) "I don’t know what to feel." 5) "The update fixed my issue." 6) "Support never replied." 7) "Not bad, not great." 8) "Absolutely thrilled!" 9) "I’m disappointed with the delay." 10) "Works as expected." Think step-by-step internally but do not show reasoning; output only JSON per line.

### Few-shot Prompt
You are a strict sentiment classifier.

Labels: Positive, Negative, Neutral.
Definitions:
- Positive: clear satisfaction or praise.
- Negative: complaint, dissatisfaction, or failure.
- Neutral: mixed, ambiguous, or matter-of-fact.

Examples:
Text: "Loved the new feature!" → {"label":"Positive","confidence":0.90}
Text: "The UI is confusing." → {"label":"Negative","confidence":0.85}
Text: "It works." → {"label":"Neutral","confidence":0.70}
Text: "Not terrible, but far from great." → {"label":"Neutral","confidence":0.65}
Text: "Thrilled with the performance." → {"label":"Positive","confidence":0.92}
Text: "Still waiting for a response." → {"label":"Negative","confidence":0.82}

Task:
Classify each line separately (same 10 lines as before).
Think step-by-step internally but do not show reasoning; output JSON only per line.


---

## Results Table

| Text                               | Zero-shot Output | Few-shot Output | Expected (your judgment) | Notes                                                             |
| ---------------------------------- | ---------------- | --------------- | ------------------------ | ----------------------------------------------------------------- |
| "This service is amazing!"         | Positive (0.98)  | Positive (0.98) | Positive                 | ✅ Matches both                                                    |
| "It’s okay, could be faster."      | Neutral (0.74)   | Neutral (0.76)  | Neutral                  | ✅ Matches both                                                    |
| "Total waste of time."             | Negative (0.99)  | Negative (0.99) | Negative                 | ✅ Matches both                                                    |
| "I don’t know what to feel."       | Neutral (0.90)   | Neutral (0.92)  | Neutral                  | ✅ Matches both                                                    |
| "The update fixed my issue."       | Positive (0.95)  | Positive (0.90) | Positive                 | ✅ Matches both (slightly lower confidence in few-shot)            |
| "Support never replied."           | Negative (0.97)  | Negative (0.94) | Negative                 | ✅ Matches both                                                    |
| "Not bad, not great."              | Neutral (0.90)   | Neutral (0.90)  | Neutral                  | ✅ Matches both                                                    |
| "Absolutely thrilled!"             | Positive (0.99)  | Positive (0.99) | Positive                 | ✅ Matches both                                                    |
| "I’m disappointed with the delay." | Negative (0.96)  | Negative (0.96) | Negative                 | ✅ Matches both                                                    |
| "Works as expected."               | Positive (0.74)  | Neutral (0.74)  | Neutral                  | ❌ Zero-shot mislabeled as Positive; Few-shot corrected to Neutral |

---

## Accuracy Summary

- Zero-shot accuracy: 9/10 → 90%
- Few-shot accuracy: 10/10 → 100%

## Comparison & Insights

- Few-shot wins on nuance. It corrected the tricky “Works as expected” case, which was misclassified as Positive in zero-shot.
- Confidence differences: Few-shot outputs were slightly more balanced and less biased toward Positive.
- Impact: Providing examples made the classifier more reliable, especially for subtle or matter-of-fact expressions.

---

## What I Practiced
- Zero-shot prompting vs few-shot prompting
- Structuring strict JSON outputs for evaluation
- Building comparison tables
- Observing systematic errors and corrections

## Next Tweaks
- Expand to **multi-class sentiment** (add categories like Sarcastic, Excited, Frustrated).
- Add a **rule-based post-processor** to catch tricky neutral cases.
- Try with real-world data (product reviews, tweets).

## How to Reproduce
1) Run the Zero-shot prompt.
2) Run the Few-shot prompt.
3) Copy results into the comparison table.
4) Tally accuracy and note insights.

```bash
# Suggested repo layout
phase1/
  sentiment-classifier/README.md
```
