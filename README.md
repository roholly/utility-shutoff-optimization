# Utility Shutoff Optimization

**Domain:** Operations Research · Public Utility  
**Type:** Analytical framework and methodology design — no code implementation  

---

## The Problem

A power company must determine which delinquent accounts to shut off each month given limited crew capacity. Not every shutoff is equal. Some customers will pay eventually without disconnection, and shutoff crew time is consumed by travel. The question is not just who to shut off, but in what order, assigned to which crew, routed how.

---

## The Approach

A four-step analytical pipeline:

**Step 1: Classify Paying vs. Non-Paying Customers**  
Support vector machine (SVM) with RBF kernel and asymmetric class weighting, penalizing misclassification of paying customers more heavily, since disconnecting someone who would have paid is a worse outcome than skipping someone who won't.

**Step 2: Shutoff Prioritization**  
Logistic regression on customers classified as non-paying, predicting the probability that a shutoff results in payment recovery. Top N candidates selected based on monthly crew capacity.

**Step 3: Crew Assignment**  
Integer programming to optimally assign prioritized customers to crews, minimizing total travel distance while respecting capacity constraints.

**Step 4: Route Optimization**  
Network optimization to sequence each crew's visits, finding the minimum-cost route visiting all assigned customers exactly once before returning to dispatch.

---

## Constraints That Shaped the Design

Medical exemptions, winter moratorium protections, and active payment plans were excluded before any modeling began. The prioritization model was designed to be auditable and free of discrimination based on protected characteristics. These aren't afterthoughts. They're part of what makes an operational model deployable.

---

## What This Demonstrates

- End-to-end operational pipeline design: classify, prioritize, assign, route
- Combining classification, regression, and optimization in sequence
- Constraint design that reflects real regulatory and ethical requirements
- Thinking about what happens after the model, not just the output
