---
layout: article
render_with_liquid: false
title: "Metalogic for Propositional Logic"
subtitle: "What makes a logical system trustworthy? Metalogic asks not how to use logic, but what logic itself is — examining the deep relationship between semantic truth and formal proof."
category: "Philosophy · Logic"
date: 2026-03-14
author: "subkiy"
author_initials: "SS"
author_image: /images/me.jpg
author_title: "University of Oslo"
author_bio: "This paper is a summary of metalogic theory for propositional logic, written as a companion to an introductory logic course. It covers semantics, axiomatic proof theory, and the soundness and completeness theorems."
read_time: 18
image: /images/logic.jpg
image_caption: "Your image caption goes here — photograph courtesy of …"
featured: true
mathjax: true
tags:
  - Logic
  - Metalogic
  - Philosophy of Mathematics
  - Proof Theory
  - Semantics
  - Completeness
related:
  - title: "What Gödel Really Proved"
    category: "Mathematics"
    description: "The incompleteness theorems are the most misunderstood results in all of mathematics."
    url: "#"
  - title: "The Church–Turing Thesis at 90"
    category: "Computing"
    description: "A conjecture that became the foundation of computer science is due for reappraisal."
    url: "#"
  - title: "Against Intuition"
    category: "Philosophy"
    description: "Why the most powerful tool in formal reasoning is also its greatest enemy."
    url: "#"
---

## 1. Introduction

This paper is a rough summary of the **metalogic** theory concerning propositional logic. Metalogic can be described as the study of logical systems themselves. In introductory logic courses, we learn the meanings of logical connectives, inference rules, and truth table verification methods — ultimately learning how to use a logical system so that we can understand the logical meaning of sentences in natural language and the inferential relationships between them. Metalogic asks questions at a different level: questions *about* the logical system itself.

To use the analogy of a chess game: "How does a knight move?" is a question about the rules of the game, whereas "Is there a strategy that guarantees victory?" is a meta-level question about the game itself.

So what is metalogic for? In truth, the answer may differ from logician to logician. However, in *Logic for Philosophy* — the main reference for this paper — Theodore Sider says that the most central concept in logic is **logical consequence**. In this sense, logic centrally deals with the nature of logical consequence. A related concept is **logical truth**. Logical consequence is truth-preservation by virtue of form; logical truth is truth by virtue of form.[^1]

What is the genuine concept of logical consequence for logic? There are two approaches: one understands it **semantically** (or model-theoretically), and the other understands it **proof-theoretically**.[^2] Each will be introduced in Sections 4 and 5 respectively. In Section 6, it will be proven that these two concepts ultimately coincide.

The structure of the paper is as follows. Section 2 introduces several basic preliminary matters. Section 3 defines well-formed formulas (wffs). Sections 4 and 5 introduce semantics and axiomatic proof theory respectively. Finally, through the Soundness and Completeness Theorems, it will be shown that the semantic and proof-theoretic concepts of logical consequence are identical.[^3]

---

## 2. Preliminaries

### 2.1 The Use–Mention Distinction

The use–mention distinction is very important to philosophers, especially in analytic philosophy. Intuitively, the object a piece of language refers to and the language itself are different things. The written character for "apple" and the fruit *apple* are different: the latter can be eaten, the former cannot. Since we must always use language as our tool, we need to make this distinction explicit.

When we refer to an *object*, we **use** a word. When we refer to the *word itself*, we **mention** it — placing quotation marks around the expression being mentioned.

Metalogic studies logical systems. When stating metalogical theory, we must distinguish between statements of the **object language** (the logical system under investigation) and statements of the **metalanguage** that describes it. A notorious example of failing to do so: the conditional connective "⊃" is a symbol of propositional logic, while "(logically) imply" is metalogical language. The former connects two propositions to form one; the latter expresses the logical relationship between two propositions. Confusing them is a use–mention error — a failure to keep object language and metalanguage distinct.[^4][^5]

### 2.2 Some Definitions from Set Theory

The basics of set theory will be assumed. A few definitions useful for formalization:

1. An ordered set with $$n$$ elements is called an **n-tuple**, written $$\langle N_1, N_2, \ldots, N_n \rangle$$.
2. An **n-place relation** is a set of n-tuples.
3. A **function** $$f$$ is a set of ordered pairs such that if both $$\langle u, v \rangle$$ and $$\langle u, w \rangle$$ are elements of $$f$$, then $$v = w$$.

**(1)** In an ordinary set, the order between elements does not affect identity. In an ordered set, however, order matters — $$\langle u, v \rangle$$ and $$\langle v, u \rangle$$ are not the same.

**(2)** A relation is the set of ordered tuples of objects between which the relation holds. The relation "OO is less than ㅁㅁ" is a binary relation:

$$R = \{\langle 1, 2 \rangle,\, \langle 1, 3 \rangle,\, \ldots,\, \langle 50, 51 \rangle,\, \ldots\}$$

**(3)** A function is a special relation — each argument yields exactly one function value. If different arguments always yield different function values, the function is called a **one-to-one function (injection)**.

### 2.3 Mathematical Induction

Mathematical induction is frequently used to show either (1) that all wffs have some property, or (2) that all theorems have some property. The underlying principle is the same in both cases: establish the property for a base case, then use an inductive hypothesis to show it holds for all cases. In metalogic, the final inductive step is typically justified by the formation rules for wffs or the derivation rules for theorems.

---

## 3. Grammar for PL

Every language has rules governing the formation of meaningful words and sentences — a grammar. In propositional logic, a sequence of symbols arranged according to grammar is called a **well-formed formula (wff)**. Wffs are defined recursively from the following basic vocabulary:

- Logical connectives[^6]: "$$\supset$$", "$$\sim$$"
- Sentence letters: "$$P$$", "$$Q$$", "$$R$$", …
- Parentheses: "(", ")"

**(1)** Every sentence letter is a PL-wff.

**(2)** If $$\phi$$ and $$\psi$$ are PL-wffs, then "$$(\phi \supset \psi)$$" and "$${\sim}\phi$$" are also PL-wffs.

**(3)** No string of symbols expressible by neither of the above is a PL-wff.

Here "$$\phi$$" and "$$\psi$$" are *metasymbols* indicating that any wff may be substituted in. From the above, we can express the other familiar connectives "$$\bullet$$", "$$\vee$$", "$$\equiv$$" as abbreviations:[^7]

| Abbreviation | Definition |
|---|---|
| $$(\phi \bullet \psi)$$ | $${\sim}(\phi \supset {\sim}\psi)$$ |
| $$(\phi \vee \psi)$$ | $${\sim}\phi \supset \psi$$ |
| $$(\phi \equiv \psi)$$ | $$(\phi \supset \psi) \bullet (\psi \supset \phi)$$ |

---

## 4. Semantics for PL

From a semantic perspective, logical consequence is "truth-preservation by virtue of the meaning of the logical constants." This captures the intuition of truth-preservation by virtue of form: fix the meaning of the logical constants, vary the meanings of everything else — if the argument still preserves truth, it does so solely in virtue of the formal meanings of the logical constants.[^8]

The semantics of propositional logic is, in essence, a rigorous formulation of the truth table method. We begin by defining:

> **Interpretation:** A PL-interpretation $$f$$ is a function that assigns each sentence letter to either 1 (true) or 0 (false).[^9]

Once the truth values of atomic sentences are fixed, the truth values of compound sentences are determined by the **principle of compositionality**. We define this formally as a *valuation*:

> **Valuation:** For any PL-interpretation $$f$$, the PL-valuation $$V_f$$ is a function assigning each wff to 1 or 0, satisfying the following conditions for any sentence letter $$\alpha$$ and wffs $$\phi$$, $$\psi$$:[^10]
>
> $$V_f(\alpha) = f(\alpha)$$
>
> $$V_f({\sim}\phi) = 1 \iff V_f(\phi) = 0$$
>
> $$V_f(\phi \supset \psi) = 1 \iff V_f(\phi) = 0 \text{ or } V_f(\psi) = 1$$

Valuations for the remaining connectives are defined analogously. We can now define **validity** and **semantic consequence**:

> A wff $$\phi$$ is **PL-valid** ("$$\models_{PL} \phi$$") iff for all PL-interpretations $$f$$, $$V_f(\phi) = 1$$.

> A wff $$\phi$$ is a **PL-semantic consequence** of a set $$\Gamma$$ ("$$\Gamma \models_{PL} \phi$$") iff for all $$f$$: if $$V_f(\gamma) = 1$$ for all $$\gamma \in \Gamma$$, then $$V_f(\phi) = 1$$.

PL-validity and PL-semantic consequence are the semantic versions of logical truth and logical consequence. Valid wffs of propositional logic are also called **tautologies**. When semantic consequence holds in both directions, it is called **semantic equivalence** — the two wffs have exactly the same truth conditions (the same *Sinn* in Frege's sense).

---

## 5. Axiomatic Proof Theory for PL

Besides the semantic approach, there is a **proof-theoretic** interpretation of logical consequence. In this section, axiomatic proof theory is adopted. Natural deduction and sequent calculus are alternatives that yield the same results.[^11]

An axiomatic proof system derives target wffs from **axiom schemas** and **rules of inference**. One notable feature: starting solely from axioms, one cannot initially perform conditional proofs that introduce assumptions — unlike in natural deduction.

**Axiomatic System for PL:**

- **Rule of Inference:** Modus Ponens (MP)
- **Axiom Schemas:**

$$\phi \supset (\psi \supset \phi) \tag{A1}$$

$$(\phi \supset (\psi \supset \chi)) \supset ((\phi \supset \psi) \supset (\phi \supset \chi)) \tag{A2}$$

$$({\sim}\psi \supset {\sim}\phi) \supset (({\sim}\psi \supset \phi) \supset \psi) \tag{A3}$$

We now define:

> **Axiomatic proof from a set:** When $$\Gamma$$ is a set of wffs and $$\phi$$ is a wff, an axiomatic proof from $$\Gamma$$ to $$\phi$$ is a finite sequence of wffs ending with $$\phi$$, where each line is either (1) an axiom, (2) an element of $$\Gamma$$, or (3) derived from preceding lines by MP.

> **Axiomatic proof:** An axiomatic proof of $$\phi$$ is an axiomatic proof from the *empty set* to $$\phi$$.

Here "$$\Gamma \vdash_{PL} \phi$$" means $$\phi$$ is provable from $$\Gamma$$; "$$\vdash_{PL} \phi$$" means $$\phi$$ is provable from the empty set (axioms and rules alone). Below is a proof of $$P \supset P$$ from the empty set:

| Line | Formula | Justification |
|---|---|---|
| 1 | $$P \supset ((P \supset P) \supset P)$$ | (A1) |
| 2 | $$(P \supset ((P \supset P) \supset P)) \supset ((P \supset (P \supset P)) \supset (P \supset P))$$ | (A2) |
| 3 | $$(P \supset (P \supset P)) \supset (P \supset P)$$ | 1, 2 MP |
| 4 | $$P \supset (P \supset P)$$ | (A1) |
| 5 | $$P \supset P$$ | 3, 4 MP |

$$\blacksquare$$

A wff provable from the axioms is called a **PL-theorem**. PL-theorems and PL-provability are the proof-theoretic versions of logical truth and logical consequence.

---

## 6. Soundness and Completeness

We have now examined two different approaches to logical truth and logical consequence. The Soundness and Completeness Theorems tell us they coincide:[^12]

> **Weak Soundness:** If $$\vdash \phi$$, then $$\models \phi$$. *(PL-theorems are PL-valid.)*
>
> **Weak Completeness:** If $$\models \phi$$, then $$\vdash \phi$$. *(PL-validity implies being a PL-theorem.)*
>
> **Strong Soundness:** If $$\Gamma \vdash \phi$$, then $$\Gamma \models \phi$$.
>
> **Strong Completeness:** If $$\Gamma \models \phi$$, then $$\Gamma \vdash \phi$$.

Strong Soundness says: if $$\phi$$ is true in every interpretation where all members of $$\Gamma$$ are true, then a formal proof is also possible. Strong Completeness says: if a proof from $$\Gamma$$ to $$\phi$$ can be constructed, then $$\phi$$ is also a semantic consequence of $$\Gamma$$. Below, we sketch the proofs of the weak versions. The strong forms require only a few additional steps.

### 6.1 Weak Soundness Theorem

The rough idea: PL-theorems are either (1) axioms, or (2) derived from preceding lines by MP.[^13] By mathematical induction, we show the axioms are PL-valid and that MP is **validity-preserving** — therefore all PL-theorems are valid.

*That (A1) is valid:* Suppose (A1) is not valid. Then there exists an interpretation $$f$$ such that $$V_f(\phi \supset (\psi \supset \phi)) = 0$$. By the definition of $$V$$: $$V_f(\phi) = 1$$ and $$V_f(\psi \supset \phi) = 0$$. The latter gives $$V_f(\psi) = 1$$ and $$V_f(\phi) = 0$$ — contradicting $$V_f(\phi) = 1$$. Therefore (A1) is valid.

*That MP preserves validity:* Suppose valid wffs $$\phi \supset \psi$$ and $$\phi$$ appear in the proof. If MP did not preserve validity, there would exist an $$f$$ with $$V_f(\phi \supset \psi) = 1$$, $$V_f(\phi) = 1$$, and $$V_f(\psi) = 0$$. This is an immediate contradiction by the definition of $$V$$. Therefore $$V_f(\psi) = 1$$, and MP preserves validity. $$\blacksquare$$

### 6.2 Weak Completeness Theorem

For the completeness theorem, two important results are needed:[^14]

> **Cut Rule:** If $$\Gamma_1 \vdash \delta_1, \ldots, \Gamma_n \vdash \delta_n$$ and $$\Sigma, \delta_1, \ldots, \delta_n \vdash \phi$$, then $$\Gamma_1, \ldots, \Gamma_n, \Sigma \vdash \phi$$.

> **Deduction Theorem:** If $$\Gamma, \phi \vdash \psi$$, then $$\Gamma \vdash \phi \supset \psi$$.

The Cut Rule says intermediate conclusions can be eliminated en route to the final conclusion. The Deduction Theorem is especially useful: it enables conditional proofs that the bare axiomatic system could not perform on its own.

The completeness proof follows the **Henkin method**.[^15] We first define:

> **Inconsistency:** A set $$\Gamma$$ is *inconsistent* iff $$\Gamma \vdash \bot$$; otherwise it is *consistent*.
>
> **Maximality:** A set $$\Gamma$$ is *maximal* iff for every wff $$\phi$$, either $$\phi$$ or $${\sim}\phi$$ (or both) is in $$\Gamma$$.
>
> **Maximal Consistent Set Theorem:** If $$\Delta$$ is a consistent set of wffs, then there exists a maximal consistent set $$\Gamma$$ with $$\Delta \subseteq \Gamma$$.

Two lemmas follow:

> **Lemma 1:** For any wff $$\phi$$, exactly one of $$\phi$$ or $${\sim}\phi$$ belongs to $$\Gamma$$.
>
> **Lemma 2:** $$\phi \supset \psi \in \Gamma$$ if and only if $$\phi \notin \Gamma$$ or $$\psi \in \Gamma$$.

We prove the contrapositive of completeness: *if $$\nvdash \phi$$, then $$\nvDash \phi$$*. We assume $$\nvdash \phi$$ and construct an interpretation that makes $$\phi$$ false.

By assumption, $$\{{\sim}\phi\}$$ must be consistent. If it were not, then $${\sim}\phi \vdash \bot$$, and by the Deduction Theorem $$\vdash {\sim}\phi \supset \bot$$. By the definition of $$\bot$$: $$\vdash {\sim}\phi \supset {\sim}(P \supset P)$$. Taking the contrapositive[^16] gives $$\vdash (P \supset P) \supset \phi$$; since $$\vdash (P \supset P)$$, we get $$\vdash \phi$$ — a contradiction.

By the Maximal Consistent Set Theorem, $$\{{\sim}\phi\} \subseteq \Gamma$$ for some maximal consistent set $$\Gamma$$. Define an interpretation $$f$$ by:

$$f(\alpha) = 1 \iff \alpha \in \Gamma \quad \text{for each sentence letter } \alpha$$

We claim that for all wffs $$\phi$$:

$$V_f(\phi) = 1 \iff \phi \in \Gamma$$

*Proof by induction.* The base case holds by definition of $$f$$. For the inductive step, we verify $${\sim}\phi$$ and $$\phi \supset \psi$$ (using Lemmas 1 and 2):

$$V_f({\sim}\phi) = 1 \iff {\sim}\phi \in \Gamma$$

$$V_f(\phi \supset \psi) = 1 \iff \phi \supset \psi \in \Gamma$$

Since $$\{{\sim}\phi\} \subseteq \Gamma$$, we have $${\sim}\phi \in \Gamma$$, and by Lemma 1, $$\phi \notin \Gamma$$. Therefore $$\phi$$ is not true under $$f$$, establishing $$\nvDash \phi$$. $$\blacksquare$$

---

## References

Sider, Ted (2010). *Logic for Philosophy*. New York: Oxford University Press.

---

[^1]: Not even the slightest content may be involved!
[^2]: Beyond these, there are also Quinean and modal interpretations. The modal interpretation holds: "The conclusion is a logical consequence of the premises if and only if it is impossible for all the premises to be true while the conclusion is false."
[^3]: To be precise, sentence, proposition, and statement are distinct concepts. However, in this paper they will be used without any special distinction for the time being.
[^4]: Bertrand Russell made this confusion, and Willard Van Orman Quine said the mistaken attempt to introduce necessity into logic originated from it.
[^5]: For strict distinction, one ought to write $$\ulcorner(\phi \supset \psi)\urcorner$$, but here for convenience we write "$$(\phi \supset \psi)$$."
[^6]: The choice of primitive connectives does not ultimately matter, as long as the combination is an adequate set.
[^7]: Of course, they can also be expressed in other ways.
[^8]: Sider adds an elaboration on what "remaining elements" means — roughly, that the truth of a sentence is determined by its meaning and the world.
[^9]: Strictly speaking, assigning the value 1 or 0 represents having the truth value true or false.
[^10]: One might wonder if using "iff" and "or" here is circular. It is not — these words are being used to *define* the valuation function, not to define logical concepts.
[^11]: Sider deals with sequent calculus. For natural deduction, see Copi's *Symbolic Logic*.
[^12]: From here on, the subscript "PL" is omitted.
[^13]: Strictly speaking, what was defined are axiom *schemas*, not axioms proper. But substituting any wff for the metasymbols yields an axiom, and the argument holds for arbitrary wffs, so no problem arises.
[^14]: Here "theorem" refers to a theorem of metalogic.
[^15]: Most mathematical logic textbooks adopt this method.
[^16]: Derivable from the axioms.

