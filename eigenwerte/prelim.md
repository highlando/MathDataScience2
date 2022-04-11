\newcommand{\coloneqq}{{:=}}
\newcommand{\eqqcolon}{{=:}}
\newcommand{\GL}{\operatorname{GL}}
\newcommand{\tr}{\operatorname{Spur}}
\newcommand{\Kern}{\operatorname{Kern}}
\newcommand{\Bild}{\operatorname{Bild}}
\newcommand{\Rang}{\operatorname{Rang}}

## Mathematische Grundlagen

Zur Entwicklung der Eigenwerttheorie betrachten wir in diesem Kapitel spezielle lineare Abbildungen $F \colon V \rightarrow V$, den sogenannten _Endomorphismen_, die von einem Vektorraum $V$ wieder nach $V$ abbilden. Hierbei beschränken wir uns auf den endlich-dimensionalen Fall und nehmen im Folgenden immer an, dass $V$ ein $\mathbb{K}$-Vektorraum über einem Körper $\mathbb{K}$ ist und eine endliche Dimension $\operatorname{dim}(V) = n, n \in \mathbb{N}$, besitzt.
Ein kanonisches Beispiel wäre der Vektorraum $V = \mathbb{R}^n$.
Es sei angemerkt, dass Eigenwerte auch für den Fall von unendlich-dimensionalen Vektorräumen untersucht werden können, zum Beispiel bei der Spektraltheorie in der Funktionanalysis.
Wir wollen uns in dieser Vorlesung jedoch auf den einfacheren, endlich-dimensionalen Fall beschränken.

Wir beginnen mit einer kurzen Auffrischung der Beziehung einer darstellenden Matrix und einer allgemeinen linearen Abbildung zwischen zwei $\mathbb{K}$-Vektorräumen.
Wie wir wissen, besteht zwischen Matrizen aus $\mathbb{K}^{n\times m}$ und linearen Abbildungen $F : V \rightarrow W$ zwischen $n$– bzw. $m$–dimensionalen $\mathbb{K}$–Vektorräumen $V$ und $W$ ein enger Zusammenhang.
Ist $B = (b_1 , . . . , b_n)$ eine Basis von $V$ und $C = (c_1, . . . ,c_m)$ eine Basis von $W$ , dann ist die darstellende Matrix $M_C^B(F) \in \mathbb{K}^{n \times m}$ diejenige Matrix, bezüglich derer der Vektor $\sum_{i=1}^n v_i b_i \in V$ unter $F$ auf den Vektor $\sum_{j=1}^m w_j c_j \in W$ mit
\[
w_j \ = \ \sum_{i=1}^n (M_C^B(F))_{j,i} v_i
\]
abgebildet wird.
Die Matrix $M_C^B(F)$ drückt also aus, wie sich die lineare Abbildung auf Vektoren von $V$ bezüglich der gewählten Basen $B$ und $C$ verhält, so dass viele mathematische Sätze für lineare Abbildungen und Matrizen äquivalent formuliert werden können.

Besonders wichtig für die Eigenwerttheorie ist der folgende grundlegende Basiswechselsatz.

::: {.theorem #basiswechselsatz name="Basiswechselsatz"}

Seien $V$ ein $n$-dimensionaler $\mathbb{K}$-Vektorraum mit $n \in \mathbb{N}$ und seien
\[
B \ \coloneqq \ (b_1, \ldots, b_n), \quad C \ \coloneqq \ (c_1, \ldots, c_n)
\]
zwei Basen von $V$.
Sei nun $v \in V$ ein Vektor, der in den beiden Basen folgende Darstellungen hat
\[
v \ = \ \sum_{i=1}^n x_i b_i \ = \ \sum_{i=1}^n y_i c_i.
\]
Die Koordinaten $(x_1, \ldots, x_n) \in \mathbb{K}^n$ und $(y_1, \ldots, y_n) \in \mathbb{K}^n$ sind eindeutig bestimmt und es existiert eine reguläre Matrix $T_C^B \in \GL(n; \mathbb{K})$, genannt _Transformationsmatrix_, die einen Basiswechsel von $B$ nach $C$ wie folgt realisiert:
$$
\begin{pmatrix}
y_1 \\
\vdots \\
y_n
\end{pmatrix}
\ = \ 
T_C^B
\begin{pmatrix}
x_1 \\
\vdots \\
x_n
\end{pmatrix}
$$
Außerdem lassen sich die Koordinaten des Vektors $v$ bezüglich der Basis $B$ aus den Koordinaten bezüglich der Basis $C$ unter zu Hilfenahme der inversen Transformationsmatrix $T_B^C = (T_C^B)^{-1}$ berechnen und es gilt
\[
\begin{pmatrix}
x_1 \\
\vdots \\
x_n
\end{pmatrix}
\ = \ 
T_B^C
\begin{pmatrix}
y_1 \\
\vdots \\
y_n
\end{pmatrix}
\]
:::

::: {.proof}
Siehe Bemerkung 2.6.2 und 2.6.3 in.
:::


Bevor wir uns dem eigentlich Studium von Eigenwerten und Eigenvektoren widmen, wollen wir noch einige grundlegende Begriffe aus der Linearen Algebra wiederholen, die aus {cite:p}`burger_2020` bereits bekannt sein sollten.
Hierbei handelt es sich um nützliche Begriffe und Eigenschaften von quadratische Matrizen als Repräsentanten von Endomorphismen, die ein Spezialfall von linearen Abbildungen zwischen $\mathbb{K}$-Vektorräumen darstellen.

::: {.definition #matrix-spur name="Spur einer Matrix"}
Sei $A \in \mathbb{K}^{n \times n}$ eine quadratische Matrix. Dann ist die _Spur_ $\tr(A)$ von $A$ definiert als die Summe der Diagonaleinträge von $A$, d.h.,
\[
\tr(A) \ \coloneqq \ \sum_{i=1}^n A_{i,i}.
\]
:::

::: {.definition name="Kern einer Matrix" #matrix-kern}
Sei $A \in \mathbb{K}^{n \times n}$ eine quadratische Matrix. Dann ist der _Kern_ $\Kern(A)$ von $A$, auch _Nullraum_ genannt, definiert als der Unterraum von $V$, dessen Vektoren von $A$ auf den Nullvektor $\vec{0} \in V$ abgebildet werden, d.h.,
\[
\Kern(A) \ \coloneqq \ \lbrace{ v \in V \, | \, Av = 0 \rbrace}.
\]
Der Kern von $A$ ist also gerade der Lösungsraum des homogenen, linearen Gleichungssystems $Av = 0$.
:::

::: {.definition name="Bild und Rang einer Matrix" #matrix-bild-rang}

Sei $A \in \mathbb{K}^{n \times n}$ eine quadratische Matrix. 

* Dann ist das mit $\Bild(A)$ bezeichnete _Bild_ von $A$, auch _Bildraum_ genannt, definiert als der Unterraum von $V$, auf den alle Vektoren $v \in V$ von $A$ abgebildet werden, d.h.,
\[
\Bild(A) \ \coloneqq \ \lbrace{ w \in V \, | \, Av = w, v \in V \rbrace}.
\]

* Weiterhin können wir den mit $\Rang(A)$ bezeichneten _Rang_ von $A$ definieren als Dimension des Bildraums von $A$, d.h., $\Rang(A) \coloneqq \dim \Bild(A)$.
:::

Folgende Lemmata werden uns nützlich sein in Bezug auf die Determinante $\det(A)$ einer quadratischen Matrix $A$.

::: {.lemma #rang-determinante}

Eine quadratische Matrix $A \in \mathbb{K}^{n \times n}$ hat genau dann vollen Rang, wenn ihre Determinante ungleich Null ist, d.h.
\[ 
\Rang(A) = \dim V \ \Leftrightarrow \ \det(A) \neq 0.
\]
:::

::: {.proof}
Sei $\Rang(A) = \dim \Bild(A) = \dim V$, dann wissen wir nach dem Satz über die Orthogonalität von Bild und Kern (siehe Satz 3.28 {cite:p}`burger_2020`), dass der Kern von $A^T$ trivial sein muss, d.h., $\Kern(A^T) = \lbrace{\vec{0}\rbrace}$. Dies ist äquivalent dazu, dass die Matrix $A^T$ regulär ist. Dann folgt schon mit der äquivalenten Bedingung aus {cite:p}`burger_2020` Satz 3.41], dass die Determinante $\det(A^T) = \det(A) \neq 0$ ist.
:::

::: {.lemma name="Determinanten-Regel von Sarrus" #sarrus}

Die Determinante $\det(A)$ einer quadratischen $(3\times 3)$-Matrix $A \in \mathbb{K}^{3 \times 3}$ mit
\[
A \ = \ 
\begin{pmatrix}
a_{11} & a_{12} & a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33}
\end{pmatrix}
\]
lässt sich mit der _Regel von Sarrus_ wie folgt berechnen.
\[ 
\det(A) \ = \ a_{11}a_{22}a_{33} + a_{12}a_{23}a_{31} + a_{13}a_{21}a_{32} - a_{13}a_{22}a_{31} - a_{11}a_{23}a_{32} - a_{12}a_{21}a_{33}.
\]
:::

::: {.proof}
Siehe Theorem 3.2.5 (Leibnizformel) in {cite:p}`fischer`.
:::

Das folgende Lemma erlaubt es uns die Determinante für Blockmatrizen besonders leicht auszurechnen und das Problem in einfachere Unterprobleme zu zerlegen.

::: {.lemma name="Determinanten-Regel für Blockmatrizen" #det-blockmatrix}

Sei $n \in \mathbb{N}$ mit $n \geq 2$ und sei $A \in \mathbb{K}^{n \times n}$ eine quadratische Blockmatrix von der Gestalt
\[
A \ = \
\begin{pmatrix}
A_1 & C \\
0 & A_2
\end{pmatrix},
\]
wobei $A_1$ und $A_2$ quadratische Blöcke sind.
Dann gilt für die Determinante der Blockmatrix $A$:
\[
\det(A) \ = \ \det(A_1) \cdot \det(A_2).
\]
:::

::: {.proof}
Siehe Satz 3.1.3, D9 [@fischer].
:::
