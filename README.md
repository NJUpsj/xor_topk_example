# XOR-TOPK: Supplementary Working Example

Due to the strict page limit of *IEEE Embedded Systems Letters*, incorporating a full step-by-step working example table into the main manuscript is impractical. We provide this detailed example to clearly illustrate the execution flow of **Algorithm 2 (XOR-TOPK-MERGE: Generalized Variant)** and assist in understanding the proposed XOR-based recovery mechanism.

## Numerical Example for $k=4$

This example demonstrates how two sorted sequences $A$ and $B$ are merged into a single sorted top-$k$ sequence $S$ using bitwise XOR operations instead of a second comparison stage.

| Step | Operation | Expression | Result |
| :--- | :--- | :--- | :--- |
| **Input** | Initial Sequences | $A=(9,6,5,3)$, $B=(8,7,6,4)$ | -- |
| **1** | Compute $m$ | $m = k/2$ | $m=2$ |
| **2** | Construct $C$ | $c_1 = \max(a_1, b_2)$ <br> $c_2 = \max(a_2, b_1)$ | $C = (9,8)$ |
| **3** | Construct $D$ | $d_1 = \max(a_1, b_4)$ <br> $d_2 = \max(a_2, b_3)$ <br> $d_3 = \max(a_3, b_2)$ <br> $d_4 = \max(a_4, b_1)$ | $D = (9,6,7,8)$ |
| **4** | XOR Recovery $E$ | $e_1 = c_1 \oplus d_1 \oplus d_3$ <br> $e_2 = c_2 \oplus d_2 \oplus d_4$ | $E = (7,6)$ |
| **5** | Local Sort | Sort $C$ and $E$ independently | $C=(9,8)$, $E=(7,6)$ |
| **6** | Concatenate | $S = C \Vert E$ | **$S = (9,8,7,6)$** |

### Key Insight: How Step 4 Works
In Step 4, we recover the smaller half of the top-$k$ elements without using comparators. For example, for $c_1$ and $e_1$:
- $c_1 = \max(d_1, d_3) = \max(9, 7) = 9$
- $e_1 = \min(d_1, d_3) = \text{XOR3}(9, 9, 7) = 7$

By using bitwise XOR, the critical path latency is reduced compared to traditional comparator-based merging.

---
*This repository is part of the supplementary material for the paper: "XOR-TOPK: Efficient Top-K Selection Hardware Engine Based on Bitwise XOR Operation".*
