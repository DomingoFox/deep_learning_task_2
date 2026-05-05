# Lithuanian LRT Summarization (LLM Fine-Tuning)

## Overview

This project collects a small Lithuanian news summarization dataset from LRT and fine-tunes a pretrained LLM to generate short article summaries.

---

## Dataset

**Source:** LRT news articles

**Size:** currently 149 valid article-summary pairs in `data/lrt_summarization_200.jsonl`

**Structure:**

* `input` - LRT article body text
* `output` - existing LRT article summary
* `title` - article title
* `url` - article URL

**Creation process:**

1. Discover article URLs from selected LRT categories
2. Extract title, summary, and article body
3. Remove duplicated summary text from the body when needed
4. Filter examples by summary length, article length, and summary/article ratio
5. Split by article URL so the same article cannot appear in both train and test

**Why useful:**

* Uses real Lithuanian news summaries instead of synthetic labels
* Gives cleaner input-output pairs for summarization fine-tuning
* Demonstrates a full low-resource language adaptation workflow

---

## Model Fine-Tuning

**Base model:** Qwen (`Qwen2.5-0.5B-Instruct`)

**Method:**

* LoRA parameter-efficient fine-tuning
* Causal LM objective
* Chat-style prompts

**Key settings:**

* Epochs: 3
* LR: 1e-4
* Batch size: 1 with gradient accumulation
* Max length: 512 (Decreased from 1024 for speed)

---

## Limitations

* Small dataset means limited generalization
* News summaries follow LRT editorial style
* Long articles may be truncated to fit the model context

---

## Demo

After training, run:

```python
summarize_lithuanian(text)
```

The model should answer with a short Lithuanian summary.
