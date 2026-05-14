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

The interesting thing about this problem is how much is hiding underneath what sounds like a simple operational question. Late bills don't automatically mean shutoff, and they shouldn't. Someone working two jobs who fell behind during a hard month is a fundamentally different situation than someone who could pay and hasn't. Getting that classification wrong has real consequences in both directions.

And the stakes aren't abstract. Shutting off power to someone on a medical device, or heat to a family during a cold snap, or air conditioning to an elderly person in an Austin summer isn't a billing error. It's a potentially life-threatening decision. The ethical constraints in this framework aren't afterthoughts. They're load-bearing.

Each of the four steps is a deep problem on its own. Classification has to distinguish ability to pay from willingness. Prioritization has to weigh recovery probability against the cost of being wrong. Crew assignment and route optimization sound like logistics, but they directly determine how many shutoffs are feasible in a given month, which affects everything upstream.

The question isn't just who to shut off. It's whether shutoff is even the right decision, and if so, for whom, in what order, at what cost.
