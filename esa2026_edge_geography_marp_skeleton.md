---
marp: true
theme: default
paginate: true
math: katex
size: 16:9
style: |
  section {
    font-family: "Aptos", "Helvetica Neue", Arial, sans-serif;
    font-size: 30px;
    padding: 56px 72px;
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
  footer { font-size: 18px; color: #666; }

  
---

<!--
Timing: 0:15–0:20
Goal: Establish the title and one-sentence framing. Do not explain technicalities yet.
Visual TODO: Optional very faint background silhouette of a narrow graph/path decomposition.
-->

# Edge Geography is XNLP-hard for Pathwidth and in XP for Tree-Partition Width

**Thobias Kvalvik Høivik** · **Erlend Raa Vågset**  
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

A token starts at a vertex $s$.

Players alternate:

1. choose an unused edge from the current vertex,
2. move the token along it,
3. delete that edge.

<div class="box center">
The first player unable to move loses.
</div>

---

![width:1100px](./geography.svg)

---

<!--
Timing: ~1:00
Goal: Set up why graph width seems relevant, then reveal the obstruction.
Visual TODO: Narrow path decomposition separating “past” and “future”. Then overlay several deleted edges incident to the same separator vertex.
-->

## Why should width help?

Small separators often suggest small dynamic-programming states.

$$
\text{Past} \quad |\quad \text{separator} \quad |\quad 
\text{future}
$$

But Edge Geography has a catch:

<div class="box center">
The game deletes <span class="danger">edges</span>, not vertices.
</div>

A separator vertex may be revisited many times while different incident edges disappear.

---

![width:600px](./crossings.svg)

---

<!--
Timing: ~1:00
Goal: Give the whole paper in one slide. This is the audience’s map.
Visual TODO: Make this a clean landscape diagram. Use arrows or three horizontal bands.
-->

## What width alone can and cannot do

<div class="three-col">

<div class="box center">
<strong>pathwidth</strong><br><br>
<span class="danger">XNLP-hard</span>
</div>

<div class="box center">
<strong>treewidth + degree</strong><br><br>
<span class="accent">FPT</span>
</div>

<div class="box center">
<strong>tree-partition width</strong><br><br>
<span class="accent">XP</span>
</div>

</div>

<br>

<div class="center">
Main question: <strong>which decompositions support a compact summary of residual play?</strong>
</div>

---

<!--
Timing: ~0:45
Goal: Introduce the source problem visually, not formally. Only one formula.
Visual TODO: Recreate a simple weighted graph with red vertex budgets, inspired by Figure 2. Maybe show one feasible and one infeasible orientation.
-->

## Source problem: Chosen Maximum Outdegree

Choose an orientation of every edge so that each vertex respects its budget.


$$
  \displaystyle \sum_{e\in\theta_\omega(v)} w(e) \leq t(v) \qquad \forall v
$$

![width:800px](./orientation.svg)

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

<!--
Timing: ~1:30
Goal: Give just enough gadget behavior for the correctness proof to feel inevitable.
Visual TODO: Abstract the edge gadget heavily. Do not paste full Figure 3. Use two symmetric corridors: x-side and y-side. Show used side / unused side.
Animation TODO: Use duplicate slides to show: enter → choose side → side consumed → later challenge.
-->

## How a gadget remembers an orientation

<div class="center">

put wicked sick picture here

</div>

During the initial traversal, one side is consumed.

Later, in the challenge phase:

<div class="two-col">
<div class="box center">
<strong>used side</strong><br><br>
challenging it is losing
</div>
<div class="box center">
<strong>unused side</strong><br><br>
one successful challenge excursion
</div>
</div>

<div class="todo">
TODO visual: simple side-selection gadget with “used” side greyed out and “unused” side highlighted.
</div>

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


<div class="todo">
TODO visual: path-decomposition timeline. Show $x,y$ intervals, a green local gadget block, short-lived auxiliary vertices.
</div>

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

---

<!--
Timing: ~1:00
Goal: Pivot from hardness to why tree partitions make an algorithm possible.
Visual TODO: Use/recreate Figure 8: graph bags on left, tree of bags on right. Highlight parent-child ports.
-->

## Tree partitions give controlled interfaces

A rooted tree partition groups vertices into bags.

Edges are either:

- inside one bag, or
- between adjacent bags of the tree.

For width $k$, a parent-child cut has at most $k^2$ ports.

<div class="box center">
A child subtree can only interact with its parent through boundedly many ports.
</div>

<div class="todo">
TODO visual: parent bag with several child bags; highlight ports crossing one parent-child boundary.
</div>

---

<!--
Timing: ~1:15
Goal: Communicate the DP without drowning in notation. This is the positive-side conceptual slide.
Visual TODO: Parent bag with child subtrees collapsed into typed black boxes. Show A, A, A, B, C becoming multiplicity vector 3A + B + C.
-->

## Compress child subtrees by type

Think of each child subtree as a black box.

An interface type records:

- where play can enter,
- where it may return,
- what residual child remains,
- whose turn it is after returning.

For fixed $k$, there are only finitely many types.

$$
A,A,A,B,C \quad\leadsto\quad 3A+B+C
$$
<div class="todo">
TODO visual: several child subtrees collapsed to labelled boxes, then compressed into multiplicities.
</div>

---

<!--
Timing: ~0:50
Goal: State the algorithmic mechanism and result, but only at talk level.
Visual TODO: Bottom-up arrows on tree partition; local acyclic games solved by reverse DP.
-->

## Bottom-up dynamic programming

At each bag, a compressed residual configuration is roughly:


$$
  \Gamma=(U,F,m)
$$

<div class="three-col small">
<div class="box center">unused<br>ports</div>
<div class="box center">unused<br>internal edges</div>
<div class="box center">multiplicities<br>of child types</div>
</div>

Local games are acyclic because every move consumes an edge or reduces a residual child type.

$$
\text{This gives an} \ n^{f(k)}\text{-time algorithm: XP}.
$$

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

---

<!--
Timing: reserve / optional slide
Goal: Use only if there is extra time or for questions. This can also be hidden by moving it after a backup divider.
Visual TODO: A small table of results and open problems.
-->

## Backup: result table

| Parameter | Directed | Undirected |
|---|---:|---:|
| pathwidth | XNLP-hard | XNLP-hard |
| treewidth + max degree | FPT | follows via known results / transfer context |
| tree-partition width | XP | XP |

<div class="todo">
TODO: verify exact phrasing for the undirected/treewidth+degree cell before final deck. This is a backup slide, not part of the core talk.
</div>

---

<!--
Timing: backup / questions
Goal: Keep details available for technical questions about the gadget.
Visual TODO: Include simplified version of the actual edge gadget, perhaps cropped/redrawn from Figure 3.
-->

## Backup: edge gadget behavior

During initial traversal:

- Player 1 chooses a side.
- Player 2's replies are forced.
- play exits at the return vertex.

During challenge:

- challenging the used side is losing,
- challenging the unused side consumes one challenge edge and one return path.

<div class="todo">
TODO visual: cleaned-up Figure 3 or a custom simplified gadget diagram.
</div>

---

<!--
Timing: backup / questions
Goal: Have the pathwidth-preservation detail ready if asked.
Visual TODO: Full cleaned-up Figure 6 with labels: anchors, local gadget block, local return paths.
-->

## Backup: pathwidth bookkeeping

The constructed decomposition follows the source path decomposition.

For a bag $B_i$:

- keep challenge anchors for vertices currently in $B_i$,
- realize edge gadgets in local contiguous blocks,
- introduce auxiliary vertices only briefly,
- realize return paths just before forgetting their vertex.


Only $O(k)$ long-lived vertices are needed.


