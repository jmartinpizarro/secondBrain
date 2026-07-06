---
aliases:
  - Category Theory - What is a category?
tags:
"References":
cssclasses:
---
# Category Theory - What is a category?

- **Abstraction**: we want to get rid of the details. Things that were different (because of unnecessary details) now they are identical.
- **Composition**
- **Identity**

Composition and identity define category theory.

## Composition

**Category**: is a bunch (not a set!) of objects. Not all categories have sets, as there things that are bigger than sets.

**Morphism**: something that goes between two objects. It is possible to have $[0, n]$ morphisms between a pair of objects $a, b$.
$$a \xrightarrow[f]{} b$$
**Categories can be represented as graphs (expand your mind about how graphs can be represented)**

```tikz
\usepackage{tikz-cd}

\begin{document}
\begin{tikzpicture}
  \node (a) at (0,0) {$a$};
  \node (b) at (2,0) {$b$};
  \node (c) at (4,0) {$c$};
  \draw[->] (a) -- node[below]{$f$} (b);
  \draw[->] (b) -- node[below]{$g$} (c);
  \draw[->] (a) to[bend left=40] node[above]{$g \circ f$} (c);
\end{tikzpicture}
\end{document}
```

$g \circ f$ is the same as applying $f$ from $a$ to $b$ and then $g$ from $b$ to $c$. The first one is a composition of the previous one.

**Theorem 1**. For every composable pair of arrows, then there must be a composition.



