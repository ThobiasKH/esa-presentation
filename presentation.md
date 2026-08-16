---
marp: true
theme: dark
paginate: true
math: katex
size: 16:9
style: |
  section {
    font-family: "Aptos", "Inter", sans-serif;
    font-size: 30px;
    padding: 56px 72px;
    background: #0d1117;
    color: #dce3ea;
  }
  h1 {
    font-size: 52px;
    line-height: 1.05;
    letter-spacing: -0.03em;
  }
  h2 {
    font-size: 42px;
    line-height: 1.08;
    letter-spacing: -0.025em;
  }
  h3 {
    font-size: 32px;
  }
  h1, h2 {
  color: #ffffff;
  }

  h2 {
    border-bottom: 2px solid #30363d;
    padding-bottom: 0.15em;
  }

  strong {
    color: #ffffff;
  }

  a {
    color: #93c5fd;
  }

  .small { font-size: 23px; }
  .tiny { font-size: 19px; }
  .muted { color: #666; }
  .accent { color: #0b5cad; font-weight: 700; }
  .danger { color: #9b1c1c; font-weight: 700; }
  .box {
    border: 2px solid #222;
    border-radius: 14px;
    padding: 18px 24px;
    margin: 12px 0;
  }
  .todo {
    border-left: 8px solid #f2c94c;
    background: #fff8df;
    padding: 12px 18px;
    font-size: 23px;
  }
  .two-col {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 36px;
    align-items: start;
  }
  .three-col {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 24px;
    align-items: start;
  }
  .center { text-align: center; }
  .bigmath { font-size: 44px; text-align: center; }
  .theorem {
    border-left: 6px solid #58a6ff;
    background: #161b22;
    padding: 0.7em 1em;
    margin: 0.7em 0;
    border-radius: 8px;
  }

  .theorem h3 {
    margin-top: 0;
    color: #58a6ff;
  }

  .theorem strong {
    color: #ffffff;
  }
  blockquote {
  border-left: 5px solid #58a6ff;
  color: #c9d1d9;
  }

  code {
    background: #161b22;
  }

  footer {
    color: #8b949e;
  }

  img[alt~="center"] {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

    .type-table {
    display: flex;
    justify-content: center;
    margin: 22px 0;
  }

  .type-table table {
    width: 92%;
    margin: 0;
    border-collapse: collapse;
    font-size: 25px;
    background: transparent !important;
  }

  .type-table th,
  .type-table td {
    padding: 13px 16px;
    text-align: center !important;
    border: 1px solid #30363d !important;
    color: #dce3ea !important;
  }

  .type-table th {
    background: #21262d !important;
    color: #ffffff !important;
  }

  .type-table td {
    background: #161b22 !important;
  }

  .type-note {
    color: #8b949e;
    font-size: 19px;
    text-align: center;
  }

  
---

<!--
Timing: 0:15–0:20
Goal: Establish the title and one-sentence framing. Do not explain technicalities yet.
Visual TODO: Optional very faint background silhouette of a narrow graph/path decomposition.
-->

# Edge Geography is XNLP-hard for Pathwidth and in XP for Tree-Partition Width

**Thobias Kvalvik Høivik (presenting)** · **Erlend Raa Vågset**  
Western Norway University of Applied Sciences

ESA 2026 · L’Aquila

---

<!--
Timing: ~1:00
Goal: Make everyone understand the game before any complexity language appears.
Visual TODO: Create a tiny directed graph with token at s. Animate/step through: choose edge → move token → delete edge → opponent moves → no move loses.
Animation TODO: Prefer 3–4 duplicated slides in Marp rather than complex animation.
-->

## Edge Geography

One of the most famous $\text{PSPACE}$-complete problems.

A token starts at a vertex $s$.

Players alternate:

1. choose an unused edge from the current vertex,
2. move the token along it,
3. delete that edge.

<div class="box center">
The first player unable to move loses.
</div>

---

![invert hue-rotate:90deg width:1100px](./geography.svg)

---


## Parameterizing the problem

<div class="theorem">

### Theorem (Bodlaender, modern language)

(Undirected) Edge Geography is solvable in time $f(k,d) \cdot O(n)$ where 
$k$ is the treewidth of the graph and $d$ is the maximum 
degree of any vertex in the graph.   

</div>

Exponential time becomes "linear time" when two parameters are controlled!
What if we allow $d$ to be unbounded? 

---

![center invert width:600px](./crossings.svg)

---

## Our first result

<div class="theorem">

### Theorem 

Directed Edge Geography is XNLP-hard parameterized by pathwidth.   

</div>

XNLP "rules out" fixed-parameter tractability.  
Bounded pathwidth $\Rightarrow$ bounded treewidth.
Pathwidth, and thus treewidth, is not enough!
This result transfers to Undirected Edge Geography in a simple way!



---

<!--
Timing: ~0:45
Goal: Introduce the source problem visually, not formally. Only one formula.
Visual TODO: Recreate a simple weighted graph with red vertex budgets, inspired by Figure 2. Maybe show one feasible and one infeasible orientation.
-->

## Source problem: Chosen Maximum Outdegree

Does there exist an orientation of every edge so that each vertex respects its budget.


$$
  \displaystyle \sum_{e\in\theta_\omega(v)} w(e) \leq t(v) \qquad \forall v
$$
FIX THIS IMAGE IT IS WRONG

![center invert width:800px](./orientation.svg)

<p class="small muted">Known XNLP-complete when parameterized by pathwidth.</p>

---

<!--
Timing: ~1:30
Goal: Explain the reduction at the highest useful level. This is the most important conceptual slide.
Visual TODO: Two-phase diagram: a chain of edge gadgets, then a challenge gadget. Show Player 1 chooses sides, Player 2 later challenges one vertex.
Animation TODO: Step 1: chain only. Step 2: orientation choices. Step 3: challenge vertex. Step 4: compare outgoing weight to return paths.
-->

## Reduction idea in two phases

### Phase I — Player 1 encodes an orientation

For each input edge $e=\{x,y\}$, Player 1 chooses one of two sides.
 
$$
 \text{choose the} \ y\text{-side}
 \quad\Longleftrightarrow\quad x\to y 
$$


### Phase II — Player 2 challenges a vertex

Player 2 chooses $x$ and tests the total weight oriented out of $x$.

$$
\text{If outgoing weight} >t(x), \ 
\text{Player 2 has one excursion too many}.
$$

---

## Phase 1

![center invert hue-rotate:125deg width:900px](./edge-gadget.png)

---

## Phase 2

![center invert hue-rotate:125deg width:900px](./black-box.png)

--- 
## The full reduction for a small source instance

![center invert hue-rotate:125deg width:900px](./full-reduction.png)

---

<!--
Timing: ~1:00
Goal: Present correctness as a budget-counting argument. Avoid gadget details here.
Visual TODO: Two columns with yes/no source instance and who wins.
-->

## Why correctness follows

<div class="two-col">

<div>
<h3>Feasible orientation</h3>

$\displaystyle \sum_{e\in\theta_\omega(x)} w(e) \leq t(x)$ for every $x$.

Player 2 eventually runs out of non-losing challenges.


<div class="box center accent">Player 1 wins</div>
</div>

<div>
<h3>Infeasible orientation</h3>

For some $x$,

$\displaystyle \sum_{e\in\theta_\omega(x)} w(e) > t(x)$.

Player 2 chooses this $x$ and survives one challenge too many.

<div class="box center danger">Player 2 wins</div>

---

<!--
Timing: ~1:00
Goal: Address the obvious concern: gadgets are large, so why does pathwidth stay small?
Visual TODO: Simplified version of Figure 6. Timeline of a path decomposition, green block where one edge gadget is active, auxiliary vertices appearing locally.
-->

## Why pathwidth is preserved

Process an input edge $e=\{x,y\}$ when $x$ and $y$ coexist in the source path decomposition.

Keep only the necessary anchors alive.

Introduce auxiliary gadget vertices locally, then forget them immediately.

$$
\operatorname{pw}(G') = O(k)
$$



---

<!--
Timing: ~0:30–0:40
Goal: Transfer directed hardness to undirected without derailing the talk.
Visual TODO: Pseudoarc replacing a directed edge. Very small and clean.
-->

## Directed to undirected

Each directed edge is replaced by a constant-size pseudoarc.

$$
u\to v \qquad\rightsquigarrow\qquad \text{undirected pseudoarc}
$$

Safe traversal works from $u$ to $v$.

Entering the wrong way is losing under optimal play.

<div class="box center">
Directed hardness transfers to Undirected Edge Geography.
</div>

![center invert width:900px](./pseudoarc.svg)

---

<!--
Timing: ~1:00
Goal: Pivot from hardness to why tree partitions make an algorithm possible.
Visual TODO: Use/recreate Figure 8: graph bags on left, tree of bags on right. Highlight parent-child ports.
-->

## XP membership for width of treepartition

A rooted tree partition groups vertices into bags.

Edges are either:

- inside one bag, or
- between adjacent bags of the tree.

For width $k$, a parent-child cut has at most $k^2$ ports (on simple graphs).

<div class="theorem">

  ### Theorem 

  Undirected Edge Geography on simple graphs, given together with a
  rooted tree partition of width $k$, is solvable in XP time  parameterized by $k$.

</div>


---

![center invert hue-rotate:0deg width:1000px](tree-partition.png)

--- 

## Bottom-up symbolic minimax

<div class="bigmath">

leaf $\longrightarrow$ interface type $\longrightarrow$ parent $\longrightarrow\cdots\longrightarrow$ root

</div>

<div class="three-col">

<div>

### 1 · Leaves

For every entry port and local residual state, brute-force minimax **inside the bag**.

Treat possible returns to the parent as variables $\nu_p$.

</div>

<div>

### 2 · Internal bags

Replace each solved child by its interface type $\sigma$.

Collect equal types into counters $m_\sigma$ and run local minimax.

</div>

<div>

### 3 · Root

There is no unknown continuation above the root.

Evaluate the final compressed state to obtain the winner.

</div>
</div>

<div class="theorem center">
Entering a solved child is a <strong>table lookup</strong>; returning is a <strong>counter update</strong>.
</div>

---

## A solved child conveys a boolean function

<div class="two-col">

<div>


![center invert hue-rotate:0deg width:400px](small-child-parent-cut.png)

</div>

<div>

### The child exports a response

$$
\Phi_a(\nu_b,\nu_c)=\nu_b\wedge\nu_c .
$$

<p class="small">

$\nu_b$ and $\nu_c$ are the values of the two possible continuations in the parent.

</p>

<p class="small">

The cut has $O(k^2)$ ports, so the truth table of $\Phi_a$ has size only $f(k)$.

</p>

<div class="box center">

Returning through $p_b$ also exports the smaller residual type $\sigma_c$.

</div>

</div>
</div>

---

## Child counters comprise the worst factor

<div class="two-col">

<div>

### The $n$-dependent part

For fixed $k$, there are $t_k$ possible child types.

Each counter lies in $\{0,\ldots,n\}$, so

$$
m\in\{0,\ldots,n\}^{t_k}
\quad\Longrightarrow\quad
\#m\leq(n+1)^{t_k}=n^{O(t_k)}.
$$

</div>

<div>

### The other factors

Unused ports and internal edges contribute

$$
2^{k^2}\cdot2^{\binom{k}{2}}
=2^{O(k^2)}.
$$

All other boundary data depends only on $k$; collect it into $g(k)$.

</div>
</div>

$$
\underbrace{n}_{\text{bags}}
\cdot
\underbrace{g(k)}_{\text{includes }2^{O(k^2)}}
\cdot
\underbrace{n^{O(t_k)}}_{\text{counter states}}
=
n^{f(k)}.
$$


---

## Laughably bad in practice

Let $T_r$ be the number of ambient types on an interface with $r$ ports.

<div class="type-table">

| ports $r$ | $0$ | $1$ | $2$ | $3$ | $4$ |
|:---:|:---:|:---:|:---:|:---:|:---:|
| ambient types $T_r$ | $1$ | $2$ | $676$ | $\approx 2^{768}$ | $\geq 2^{2^{4058}}$ |

</div>

<div class="type-note">

Illustrative ambient count obtained by unwinding Definition 35.  
The number of realizable types may be vastly smaller.

</div>

<div class="theorem center">

A width-$k$ cut may have $k^2$ ports.<br>
The crude bound is a tower of exponentials of height $O(k^2)$.

</div>


---

<!--
Timing: ~1:00
Goal: End with the conceptual punchline and one open direction. This should be memorable.
Visual TODO: Return to the main landscape diagram, now with explanatory labels underneath.
-->

## Takeaway

<div class="two-col">

<div class="box center">
<h3>Pathwidth</h3>
small separators<br><br>
<span class="danger">but residual history is uncontrolled</span><br><br>
<strong>XNLP-hard</strong>
</div>

<div class="box center">
<h3>Tree-partition width</h3>
bounded interfaces<br><br>
<span class="accent">residual play can be compressed</span><br><br>
<strong>XP</strong>
</div>

</div>

<br>

<div class="box center">
Open: Is Edge Geography in XP parameterized by pathwidth alone?
</div>

