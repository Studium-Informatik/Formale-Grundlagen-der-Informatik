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
```tikz
\usepackage{tikz}
\usetikzlibrary{automata, positioning}

\begin{document}
\begin{tikzpicture}[shorten >=1pt,node distance=2cm,on grid,auto] 

\node[state, initial]          (q0) {$q_0$};
\node[state]                   (q1) [right=of q0] {$q_1$};
\node[state, accepting]        (q2) [right=of q1] {$q_2$};
\node[state]                   (q3) [below=of q0] {$q_3$};
\node[state, accepting]        (q4) [right=of q3] {$q_4$};
\node[state]                   (q5) [right=of q4] {$q_5$};

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


# 3
## 1.
$L(N)=L(a^*b^+)$

## 2
```tikz_o
\usepackage{tikz}
\usetikzlibrary{arrows,automata,positioning}

\begin{document}
\begin{tikzpicture}[->,>=stealth,auto,node distance=2cm,semithick]

% Row 1 (top)
\node (q0aab) at (0,0) {$\ast q0aab$};

% Row 2
\node (aq0ab)      [below left=1.5cm and 2cm of q0aab] {$aq0ab$};
\node (starq0ab)   [below right=1.5cm and 2cm of q0aab] {$\ast q0ab$};

% Row 3
\node (aaq0b)      [below left=1.2cm and 1.5cm of aq0ab] {$aaq0b$};
\node (astarq0b)   [below right=1.2cm and 1.5cm of aq0ab] {$a\ast q0b$};
\node (aq0b)       [below left=1.2cm and 1.5cm of starq0ab] {$aq0b$};
\node (starq0b)    [below right=1.2cm and 1.5cm of starq0ab] {$\ast q0b$};

% Row 4
\node (aabq1star)      [below=1.2cm of aaq0b]      {$aabq1\ast$};
\node (astarbq1star)   [below=1.2cm of astarq0b]   {$a\ast bq1\ast$};
\node (abq1star)       [below=1.2cm of aq0b]       {$abq1\ast$};
\node (bq1star)        [below=1.2cm of starq0b]    {$bq1\ast$};

% Row 5 (bottom)
\node (aabstarq2star)         [below=1.2cm of aabq1star]      {$aab\ast q2\ast$};
\node (astarbq1starq2star)    [below=1.2cm of astarbq1star]   {$a\ast bq1\ast q2\ast$};
\node (abq1starq2star)        [below=1.2cm of abq1star]       {$abq1\ast q2\ast$};
\node (bq1starq2star)         [below=1.2cm of bq1star]        {$bq1\ast q2\ast$};

% Arrows
\path (q0aab)         edge (aq0ab)
      (q0aab)         edge (starq0ab)

      (aq0ab)         edge (aaq0b)
      (aq0ab)         edge (astarq0b)

      (starq0ab)      edge (aq0b)
      (starq0ab)      edge (starq0b)

      (aaq0b)         edge (aabq1star)
      (astarq0b)      edge (astarbq1star)
      (aq0b)          edge (abq1star)
      (starq0b)       edge (bq1star)

      (aabq1star)     edge (aabstarq2star)
      (astarbq1star)  edge (astarbq1starq2star)
      (abq1star)      edge (abq1starq2star)
      (bq1star)       edge (bq1starq2star);

\end{tikzpicture}
\end{document}
```

![[Z_3.2.excalidraw]]

## 3.

| $\delta$ | $a$                                 | $b$                   | $*$                   |
| -------- | ----------------------------------- | --------------------- | --------------------- |
| $q_{0}$  | $\{ 1:(q_{0},a,R),2:(q_{0},*,R) \}$ | $\{ 1:(q_{1},b,R) \}$ | $\emptyset$           |
| $q_{1}$  | $\emptyset$                         | $\{ 1:(q_{1},b,R) \}$ | $\{ 1:(q_{2},*,L) \}$ |

$$aabq_{2}*,a*bq_{2}*,abq_{2}*,bq_{2}*$$
