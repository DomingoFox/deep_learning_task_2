# Lithuanian Wikipedia Summarization (LLM Fine-Tuning)

## Overview

This project creates a small **Lithuanian summarization dataset** and fine-tunes a pretrained LLM to generate short summaries (1–2 sentences). The focus is on **low-resource language adaptation**.

---

## Dataset

**Source:** Lithuanian Wikipedia articles (manually selected topics)

**Size:** ~150–200 samples (after sliding-window expansion)

**Structure:**

* `instruction` – Lithuanian task prompt
* `input` – cleaned article paragraphs
* `output` – short extractive summary
* `title` – article title

**Creation process:**

1. Fetch article HTML
2. Extract and clean paragraphs
3. Filter by length
4. Generate summaries using sentence selection

**Why useful:**

* Provides Lithuanian summarization examples
* Simple, stable targets for small models
* Suitable for demonstration in low-resource settings

---

## Model Fine-Tuning

**Base model:** Qwen (`Qwen2.5-0.5B-Instruct`)

**Method:**

* LoRA (parameter-efficient fine-tuning)
* Causal LM objective
* Chat-style prompts

**Key settings:**

* Epochs: 5
* LR: 1e-4
* Batch size: 1 (grad accumulation)
* Max length: 768

---

## Results

**Before fine-tuning:**

* Inconsistent Lithuanian output
* Often continues text instead of summarizing

**After fine-tuning:**

* Produces short Lithuanian summaries
* Follows instruction format
* Extracts key sentences from input

---

## Limitations

* Small dataset → limited generalization
* Mostly extractive summaries
* Occasional repetition or truncation

---

## Demo

Run:

```python
summarizelithuanian(text)
```

Test with unseen Lithuanian text to evaluate behavior.

---

## Conclusion

The dataset successfully teaches a small LLM to:

* Follow Lithuanian instructions
* Produce concise summaries
* Adapt to a low-resource language setting

This demonstrates effective fine-tuning with minimal data.
