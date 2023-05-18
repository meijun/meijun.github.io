In UCB CS188 course Pacman project, we should give some heuristics to search efficiently. Heuristics are easy to find. For example, the two trivial heuristics are always zero and the true minimum cost to the goal. The former is easy to compute but without boosting the searching efficiency. The latter is very hard to compute (actually it’s our original searching problem), but it gives the best searching efficiency. Thus, a good heuristic is a trade-off between the heuristic computing time and the approximate accuracy.

Here I give my way to find a good heuristic:
- Relax the problem to ensure admissive and make it efficient to compute.
- Check the consistency.

In the relaxing step, we can relax the problem to make it efficient to solve, for example, by the greedy algorithm, by dynamic programming, etc. The relaxing is to ignore some restrictions in the original problem. But be careful, we should relax the problem slightly, to approximate accurately. The relaxing can ensure admissive.

In the checking step, we should make sure our heuristic is consistent. The consistency is defined as heuristic "arc" cost <= actual arc cost for each arc, formally:

$$\forall (u,v) \in E, h(u)-h(v)\leq cost(u, v)$$

For the grid search problem, every arc cost is $1$, so we should check whether $h(u)-h(v)\leq 1$ for every grid point $u$ and its neighbour $v$. If we use Manhattan distance as the heuristic, it's consistent, since the Manhattan distance cannot decrease more than $1$ in one move. It's no hurt to the consistency if the heuristic increases in any move.
