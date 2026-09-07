---
title: "Markdown Rendering Test"
date: 2026-09-07
draft: true
---

This page exists to test Markdown rendering.

## Text

This is a normal paragraph with **bold text**, *italic text*,
~~strikethrough~~, and `inline code`.

Here is a [link to Hugo](https://gohugo.io/).

---

## Headings

### Third-level heading

#### Fourth-level heading

A paragraph beneath a fourth-level heading.

## Lists

Unordered:

- First item
- Second item
  - Nested item
  - Another nested item
- Third item

Ordered:

1. First step
2. Second step
3. Third step

Task list:

- [x] Hugo installed
- [x] Basic layout created
- [ ] Finish website

## Blockquote

> Simplicity is not the absence of complexity.
> It is the result of understanding it.

## Inline code

Run `hugo server` to start the development server.

## Code block

```python
def fibonacci(n: int) -> int:
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))
```

And some shell:

```bash
hugo server
git status
git log --oneline
```

## Table

| Language | Type | Notes |
|---|---|---|
| C | Systems | Low-level |
| Python | General purpose | High-level |
| Haskell | Functional | Strong type system |

## Definition list

Hugo
: A static site generator written in Go.

Goldmark
: Hugo's default Markdown renderer.

## Footnotes

This sentence contains a footnote.[^1]

Another statement can have another footnote.[^long]

[^1]: This is a short footnote.

[^long]: This is a slightly longer footnote used to check line wrapping and spacing.

## Horizontal rule

Above.

---

Below.

## Image

![Markdown rendering test](/images/markdown-test.svg)

## Long paragraph

A well-designed technical website should remain readable even when a paragraph becomes fairly long. The purpose of this paragraph is to make it easier to judge text width, line height, visual rhythm, and the relationship between consecutive lines of prose. If reading this feels comfortable rather than cramped or excessively wide, the basic typography is probably working.

## Mathematics

Inline mathematics should appear naturally inside a sentence.
For example, \(E = mc^2\) is Einstein's mass-energy relation.

Another inline expression is
\(\operatorname{Var}(X) = \mathbb{E}[X^2] - \mathbb{E}[X]^2\).

### Display mathematics

A simple equation:

\[
e^{i\pi} + 1 = 0
\]

A summation:

\[
\begin{aligned}
\sum_{n=1}^{\infty} \frac{1}{n^2}
  &= \frac{\pi^2}{6}
\end{aligned}
\]

A matrix:

\[
A =
\begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix}
\]

An aligned derivation:

\[
\begin{aligned}
(a+b)^2
  &= (a+b)(a+b) \\
  &= a^2 + ab + ba + b^2 \\
  &= a^2 + 2ab + b^2
\end{aligned}
\]

A more technical expression:

\[
\begin{aligned}
p(\theta \mid x)
  &=
  \frac{
    p(x \mid \theta)p(\theta)
  }{
    \int p(x \mid \theta')p(\theta')\,d\theta'
  }
\end{aligned}
\]

Dollar signs in ordinary text should remain ordinary:
$10, $HOME, and USD $50.
