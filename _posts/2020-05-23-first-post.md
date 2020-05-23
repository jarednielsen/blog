---
toc: true
layout: post
description: An introduction, then straight to Python innovations
categories: [markdown]
title: Hello World
---
# Intro

You know how journals never work? Well, the allure of tech and easy (somewhat) self-hosted blogging has lured me in.
Sssh, no need to mention that Microsoft runs GitHub Pages. So what's the purpose of this thing?
- To learn. The best way to clarify and harden your thoughts is by writing them down. We'll probably range from programming to finance.
- To journal, permanently. Handwritten paper gets stuffed away, and digital Google Docs become too large. I hope the searchable, version-controlled format
improves discoverability.

## So, whatcha got for me today?
There's a better Python `argparse.ArgumentParser` out there. Before, you had
```python
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("--batch_size", default=6, type=int)
parser.add_argument("--total_steps", default=8144, type=int)
args = parser.parse_args()
```
Now you have
```python
@dataclass
class ModelArguments:
    model_type: str = field(default="bert")
    model_size: str = field(default="base")

@dataclass
class TrainingArguments:
    batch_size: int = field(default=6)
    total_steps: int = field(default=8144)

from transformers import HfArgumentParser
parser = HfArgumentParser((ModelArguments, TrainingArguments))
model_args, train_args = parser.parse_args_into_dataclasses()
```

The new `dataclass` in Python 3.7 combined with `huggingface/transformers` lets you group arguments, and
declare them in a more object-oriented way. It's not useful if you only have three command-line arguments.
But when you're creeping up on 15-20 args, your function signature will thank you!