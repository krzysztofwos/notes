[[Markowitz model]] — portfolio optimization
[[Sherrington-Kirkpatrick model]] — spin glasses
[[Hopfield model]] — neural networks

![[Mathematical Models Portfolio Optimization, Spin Glasses, and Neural Networks.png]]

Typesetting similar diagram in LaTeX:

```latex
\documentclass{article}
\usepackage{amsmath}
\usepackage{tikz}
\usetikzlibrary{tikzmark, positioning, arrows.meta}

\tikzset{
    smaller/.tip={Latex[length=1mm,width=1mm]}
}

\begin{document}

\begin{align*}
    \tikzmarknode{F}{F} & = \sum_{i,j} \tikzmarknode{Cij}{C_{ij}} \tikzmarknode{ni}{n_i} n_j - \tikzmarknode{zeta}{\zeta} \sum_{i} \tikzmarknode{Ri}{R_i} n_i \\
\end{align*}

\begin{tikzpicture}[overlay, remember picture]
    \node[above = 0.5cm of F,font=\scriptsize] (labelf) {risk minus returns};
    \draw[-smaller,shorten >=3pt] (labelf) -- (F);

    \node[above = 1.0cm of ni,font=\scriptsize] (labelni) {no. of assets of type \(i\)};
    \draw[-smaller,shorten >=3pt] (labelni) -- (ni);

    \node[below = 1.0cm of Cij,font=\scriptsize] (labelcij) {correlations between assets};
    \draw[-smaller,shorten >=3pt] (labelcij) -- (Cij);

    \node[above = 0.5cm of zeta,font=\scriptsize] (labelzeta) {risk tolerance};
    \draw[-smaller,shorten >=3pt] (labelzeta) -- (zeta);

    \node[below = 0.5cm of Ri,font=\scriptsize] (labelri) {return on \(i\)th asset};
    \draw[-smaller,shorten >=3pt] (labelri) -- (Ri);
\end{tikzpicture}

\end{document}
```
