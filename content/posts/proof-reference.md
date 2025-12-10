---
title: "Proofs in Symbol, SQL and English"
date: 2025-12-10
draft: true
tags: ["math", "proofs", "SQL", "logic", "reference"]
---

# Proofs in Symbol, SQL and English

A personal reference

## DIRECT PROOF

### Goal

$P \to Q$

### SQL

Show:

```sql
-- No row has P but not Q
NOT EXISTS (
    SELECT 1 FROM t WHERE P AND NOT Q
);
```

### English

Assume P, show Q follows.

---

## CONTRAPOSITIVE

### Goal:

$
P \to Q
$

Prove instead:

$
\neg Q \to \neg P
$

### SQL:

Show:

```sql
-- No row has NOT Q and P
NOT EXISTS (
    SELECT 1 FROM t WHERE NOT Q AND P
);
```

### Reason

Same WHERE clause, different viewpoint.
Usually much easier.

---

## CONTRADICTION

### Goal

Prove (P).

Assume ¬P and show this leads to impossible conditions.

SQL analogy:

```sql
-- We assume a row exists that contradicts something fundamental
SELECT * FROM impossible_view;
-- contradiction is like a query returning rows when it never should
```

Example impossible condition:

```sql
WHERE x = 5 AND x = 7;
```

Contradiction = WHERE FALSE.

---

## CASE SPLIT

### Goal:

Prove R.

Check both cases:

* when P is true
* when P is false

SQL:

```sql
SELECT * FROM A WHERE P
UNION ALL
SELECT * FROM A WHERE NOT P;
```

If conclusion R holds in both branches, you're done.

---

## EQUIVALENCE PROOF

To prove (P \leftrightarrow Q):

Prove *two implications*:

$
P \to Q \quad \text{and} \quad Q \to P.
$

SQL:

```sql
-- check no row is P and NOT Q
NOT EXISTS (SELECT 1 WHERE P AND NOT Q)
AND
-- check no row is Q and NOT P
NOT EXISTS (SELECT 1 WHERE Q AND NOT P)
```

---

## EXISTENCE PROOF

### Goal:

$
\exists x,\ P(x)
$

SQL:

```sql
EXISTS (SELECT 1 FROM table WHERE P)
```

You literally just provide a witness.

In maths:
"Let (x = 3). Then (P(x)) is clearly true."

---

## UNIVERSAL PROOF

To show:

$
\forall x,\ P(x)
$

SQL:

```sql
NOT EXISTS (SELECT 1 FROM table WHERE NOT P)
```

This one is absolutely *fundamental*.
Nearly every Lean proof uses this shape.
