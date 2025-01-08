---
tags:
  - Übung
  - Hausaufgabe
  - WiSe_24-25
  - FGI
createdAt: 2025-01-08
---
[PDF](Uebung_Z.pdf)

# 1

|     | $i$              | $f$         | $\$$         |
| --- | -------------- | --------- | --------- |
| $q_1$ | $\{ q_2, q_3 \}$ | $\{ q_3 \}$ | $\emptyset$ |
| $q_2$ | $\emptyset$      | $\{ q_4 \}$ | $\emptyset$ |
| $q_3$ | $\{ q_3 \}$      | $\{ q_3 \}$ | $\{ q_4 \}$ |
| $q_4$ | $\emptyset$      | $\emptyset$ | $\emptyset$ |

| $\delta$        | $i$             | $f$             | $\$$        |
| --------------- | --------------- | --------------- | ----------- |
| $[q_{1}]$       | $[q_{2},q_{3}]$ | $[q_{3}]$       | $\emptyset$ |
| $[q_{2},q_{3}]$ | $[q_{3}]$       | $[q_{4},q_{3}]$ | $[q_{4}]$   |
| $[q_{4},q_{3}]$ | $[q_{3}]$       | $[q_{3}]$       | $[q_{4}]$   |
| $[q_{3}]$       | $[q_{3}]$       | $[q_{3}]$       | $[q_{4}]$   |
| $[q_{4}]$       | $\emptyset$     | $\emptyset$     | $\emptyset$ |

```tikz
\usepackage{tikz}
\usetikzlibrary{automata, positioning}

\begin{document}
\begin{tikzpicture}[shorten >=1pt,node distance=2cm,on grid,auto] 

\node[state, initial]          (q0) {$[q_1]$};
\node[state]                   (q1) [right=of q0] {$[q_2,q_3]$};
\node[state, accepting]        (q2) [right=of q1] {$[q_3,q_4]$};
\node[state]                   (q3) [below=of q0] {$\emptyset$};
\node[state, accepting]        (q4) [right=of q3] {$[q_4]$};
\node[state]                   (q5) [right=of q4] {$[q_3]$};

\path[->]
   (q0) edge              node        {$i$}      (q1)
   (q0) edge [swap]       node        {$\$$}     (q3)
   (q0) edge[out=-90, in=135, looseness=1.2] node {$f$} (q5)
   
   (q1) edge              node        {$f$}      (q2)
   (q1) edge              node        {$\$$}     (q4)
   (q1) edge              node        {$i$}      (q5)
   
   (q2) edge              node        {$i,f$}    (q5)
   (q2) edge[out=90, in=135, looseness=1.2] node[above] {$\$$} (q3)
   
   (q3) edge [loop below] node        {$i,f,\$$} (q3)
   
   (q4) edge              node        {$i,f,\$$}      (q3)
   
   (q5) edge [loop right] node        {$i,f$}    (q5)
   (q5) edge              node        {$\$$}     (q4);
\end{tikzpicture}
\end{document}
```

$r=(if)+(i+f)^+\$$

# 2
Algorithmus mit:
Eingabe TM $M$ und $w$

Konstruktion einer TM $M^\prime$ für das Unendlichkeits Problem

$M^\prime$ löscht die Eingabe und schreibt $w$ auf das Band.
Dann simuliert $M^\prime$ die TM $M$ auf $w$
Wenn $M$ hällt ist $w\in L(M)$

# 3
## 1.
$L(N)=L(a^*b^+)=\{ xy \mid x \in\{ a \}^*, y\in\{ b \}^+ \}$

## 2
![[Z_3.2.excalidraw]]

## 3.

| $\delta$ | $a$                                 | $b$                   | $*$                   |
| -------- | ----------------------------------- | --------------------- | --------------------- |
| $q_{0}$  | $\{ 1:(q_{0},a,R),2:(q_{0},*,R) \}$ | $\{ 1:(q_{1},b,R) \}$ | $\emptyset$           |
| $q_{1}$  | $\emptyset$                         | $\{ 1:(q_{1},b,R) \}$ | $\{ 1:(q_{2},*,L) \}$ |

$$aabq_{2}*,a*bq_{2}*,abq_{2}*,bq_{2}*$$
