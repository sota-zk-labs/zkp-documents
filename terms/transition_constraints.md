---
comments: true
---
# Transition Constraints

Transition constraints specify that any two consecutive state tuples evolved in accordance with the state transition function.
It is a list of multivariate polynomials that captures the transition of each register.

For example, given two continuous state: $X=(x_0,\dots,x_{w-1})$ and $Y = (y_0,\dots,y_{w-1})$, the transition constraint is:
$p(x_0,\dots, x_{w-1},y_0,\dots, y_{w-1}) = 0$
