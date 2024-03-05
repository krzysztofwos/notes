Figure 7.3

![[Active Inference Textbook Figure 7.3.png]]

Figure 7.10

![[Active Inference Textbook Figure 7.10.png]]

Partially-Observable Markov (POM) Model

| Ontology Term                | Discrete Time | Description                                                                                                          |
| ---------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------- |
| Generative Model             |               | Living room in New Mexico                                                                                            |
| Observation                  | o             | Pixels coming from outside<br>- 10 pixels that are either 0 or 1<br>- Darker when raining, lighter when not          |
| Hidden state                 | s             | Raining or not (binary state)                                                                                        |
| Ambiguity                    | A             | 2x10 matrix<br>Maps observations to hidden state                                                                     |
| Transition                   | B             | 2x2 matrix<br>Staying raining, staying not raining, switching                                                        |
| Preference                   | C             | Over observations                                                                                                    |
| Prior<br>Empirical prior     | D             | Prior on it raining, e.g., \[1 0\] if we start sure it is raining, or \[0.5 0.5\] if we start unsure if it's raining |
| Affordance                   | E             | Go outside or not                                                                                                    |
| Policy                       | $\pi$         | Go outside or not<br>Single time step, no planning                                                                   |
| Action<br>Active States      | a             |                                                                                                                      |
| Generative Process           |               | Environment, the true probability distribution of raining or not                                                     |
| Non-Equilibrium Steady State |               |                                                                                                                      |

Features of the visual experience demonstrating that it is being generated

- no blind spot
- color in the periphery
- resolution in the periphery
- suppression of the saccades
