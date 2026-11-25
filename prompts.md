# Prompt templates for Kimi models

Starting templates only; they are not tested outputs or benchmark prompts. Replace bracketed text and use only fields supported by the chosen route.

## Long document

```text
Summarize this document in five bullets. Then list key decisions, unresolved questions, and assumptions: [document].
```

## Image question

```text
Describe the visible elements in this image and distinguish direct observations from guesses: [image].
```

## Code review

```text
Review this change for correctness and maintainability. Prioritize concrete issues and cite relevant lines: [diff].
```

## Image prompts

For a route that accepts image_url, provide the image as a separate request field and refer to it in prompt. Do not assume a text-only route can fetch or inspect an image URL.
