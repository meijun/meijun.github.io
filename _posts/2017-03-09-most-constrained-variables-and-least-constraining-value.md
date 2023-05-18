There are two important ordering methods for solving CSP problems using backtracking search:
- Minimum Remaining Values (MRV)
- Least Constraining Value (LCV)

The former is for ordering variables. It tells us that it's better to consider the variables with minimum remaining values, so it's also known as the most constrained variables method. The latter is for ordering values. After we decided to consider one variable, there are many values to consider. It tells us that it's better to consider the least constraining value firstly.

Most of the people believe that MRV leads the searching fail-fast, and LCV leads the searching succeed-fast. Choose the fail-fast variable but choose the succeed-fast value. Choose the most constrained variable but choose the least constraining value. It seems that the two ordering methods are not consistent, right?

Actually, this question confuses me a lot. After struggling hard, I believe the truth is in my mind now. Both methods want the searching end-fast. MRV leads the searching not only fail-fast but also succeed-fast. LCV leads the searching succeed-fast, but not fail-fast. When considering to choose variables, choosing the most constrained variable makes the searching tree thin, so it leads the searching end-fast. When considering to choose values, there are two cases. Suppose that we have $n$ values to consider, that means we have $n$ sub searching trees currently. If all the $n$ sub searching trees fail in the end, then it's no matter how we order the values. If one of the sub searching trees succeeds, it's better to consider this succeeding sub searching tree. We believe the least constraining value has the most probability to succeed, so we consider the least constraining value firstly, and so this leads succeed-fast.
