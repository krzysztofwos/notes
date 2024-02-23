$$
Q^*(s, a) = r + \gamma max_{a^\prime}(Q^*(s^\prime, a^\prime))
$$

| Symbol                   | Description                                                                  |
| ------------------------ | ---------------------------------------------------------------------------- |
| $Q^*(s, a)$              | The value of taking action $a$ in state $s$                                  |
| $r$                      | Reward                                                                       |
| $\gamma$                 | Discount factor                                                              |
| $\max_{a'}(Q^*(s', a'))$ | The maximum possible value of the next state $s'$ given the best action $a'$ |
