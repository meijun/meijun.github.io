The following $\alpha \beta$ pruning algorithm looks clever, however, it has a tricky bug. Can you find where the bug is?

```python
def alpha_beta(state, alpha, beta):
    if state.finished():
        return state.calcScore()
    for next_state in state.next():
        alpha = max(alpha, -alpha_beta(next_state, -beta, -alpha))
        if alpha >= beta:
            break
    return alpha
```

Tips: This code is able to find the correct solution, but may be more time-consuming.
