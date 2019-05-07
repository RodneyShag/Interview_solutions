### Solution

Implement a directed graph and use DFS/BFS to detect a cycle.

A deadlock can occur if and only if we find a cycle.

### Similar Solution

From MIT's "Hacking a Google Interview"

How can we ensure that deadlock does not occur?

There are many possible answers to this problem, but the answer the interviewer will be looking for is this: we can prevent deadlock if we assign an order to our locks and require that locks always be acquired in order. For example, if a thread needs to acquire locks 1, 5, and 2, it must acquire lock 1, followed by lock 2, followed by lock 5. That way we prevent one thread trying to acquire lock 1 then lock 2, and another thread trying to acquire lock 2 then lock 1, which could cause deadlock (Note this approach is not used very often in practice).
