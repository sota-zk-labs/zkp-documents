---
comments: true
---

# Gate

A constraint $q_i \cdot p(\dots)=0$ can be switched off for a particular row $i$ by setting $q_i=0$. In this case we sometimes refer to
a set of constraints controlled by a set of selector columns that are designed to be used together, as a **gate**.

Typically, there will be a **standard gate** that supports generic operations like field multiplication and division, and possibly also
**custom gates** that support more specialized operations.
