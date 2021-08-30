# Overview

This is a visulization for emotional equations in Perceptual System in EDA (Empathy-Driven Architecture). EDA is a cognitive architecture derived from Multi-A architecture. This assignment is a task within 2021 Summer Grinnell Mentored Advaced Project: Modeling Moral Reasoning. 

The implementation of emotional equations is in Cascading Failure scenario. The agent is networked in a lattice network with a length of 15 agents. Each agent has one of the three states: cooperator, defector, or dead agent. The simulation is conducted in discrete matches, whithin which there are four consecutive actions: interaction, evaluation of survival, status update, and emotion update. 

## 1. Interaction

At the beginning of the match, each agent must interact with all neighbors if they are still alive. During the interaction, the agent gets reinforcement based on its status and its neighbor’s status. Reinforcement received by the interaction is summarized in the following table where $V_i$ is the number of neighbors at the beginning of the simulation. 

| Reinforcement            | Agent Being a Cooperator | Agent Being a Defector |
| ------------------------ | ------------------------ | ---------------------- |
| Neighbor is a Cooperator | $1/V_i$                  | $2/V_i$                |
| Neighbor is a Defector   | $0$                      | $0$                    |
| Neighbor is Dead         | 0                        | 0                      |

One observation is that the highest reinforcement is achieved when a defector interacts with all neighbors who all happens to be cooperators. Also notice that if a neighbor is a defector or a dead agent, the agent receives no reinforcement at all no matter what its status is. 

## 2. Evaluation of Survival 

After interactions, each alive agent will have a total reinforcement received from interactions with its neighbors, which will determin if it will stay alive at end of the match. Survival Threshold is the value for determining whether the agent will stay alive. If the total reinforcement received during the match is higher than survival threshold, the agent survives; otherwise, the agent is dead. 

## 3. Status Update 

If a defector is surrounded mostly by cooperators, the agent is more likely to receive a higher reinforcement than its neighbors who are cooporators. During status update stage, there is a probability for a cooperating agent to change from a cooperator to a defector if it has a defecting neighbor who received higher reinforcement in current match. Defecting probability is the parameter for such probability, and it is set to 0.5 in this simulation. 

## 4. Emotion Update 

The final stage of a match is to update emotional values based on reinforcement and interactions during current match. There are six emotion values to update: fear, happiness, anger, sadness, surprise, and disgust. 

Common Variables:

- $r$: reinforcement received from an interaction 
- `a_happiness`, `a_anger`, `a_sadness`, `a_disgust` : parameters controlling the weight of previous emotion value and current one. 
- `r_exp`: expected reinforcement value for the match 
- `V_i`: number of neighbors at the beginning of the simulation
- `v_[t-1]`: number of neighbors from the previous match 

### Fear

`fear` is set to 1 at the beginning of match. For each interaction $fear -= 2/V_i$ if reinforcement of the interaction is positive. 

### Happiness

`happiness = happiness_prev * a_happiness +
(1 - a_happiness) * happiness_curr`

Variables:

- `happiness_prev`: happiness value from previous match 
- `a_happiness`: a parameter controlling the weight of current and previous happiness value 
- `happiness_curr`: happiness value for interactions in current match

At the beginning of each match, $happiness_{curr}$ is set to zero. For each interaction, $happiness_{curr} += 1$ if $r > 0$ , else  $happiness_{curr} -= 1$. 

### Anger

`anger = a_anger * anger_marker + (1 - a_anger) * anger_curr`

- `a_anger`: a parameter controlling the weight of current and previous anger value 
- `anger_marker`: a value calculated from anger value from the previous match 
- `anger_curr`: anger value for interactions in current match

At the beginning of each match, `anger_curr` is set to 1. For each interaction, if $r >= r_{exp}$, `anger_curr -= 2/v_i` . 

If anger value from previous match is positive, `anger_marker = 1`, else `anger_marker = 0`. 

### Sadness 

`sadness = a_sadness * sadness_marker + (1 - a_sadness) * sadness_curr`

- `a_sadness`: a parameter controlling the weight of current and previous sadness value 
- `sadness_marker`: a value calculated from sadness value from the previous match 
- `sadness_curr`: sadness value for interactions in current match

At the beginning of each match, `sadness_curr` is set to 0. For each interaction, `sadness_curr -= 1/v_i`  if  `r > 0`, else  `sadness_curr += 1/v_i`  

If sadness value from previous match is positive, `sadness_marker = 1`, else `sadness_marker = 0`. 

### Surprise

`surprise = 2 * (vi - v_[t-1]) / vi - 1`

- `v_[t-1]`: number of neighbors from the previous match 
- `V_i`: number of neighbors at the beginning of the simulation

For each match, surprise is updated according to the above formula. 

### Disgust

`disgust = a_disgust * disgust_marker + (1 - a_disgust) * surprise`

- `a_disgust`: a parameter controlling the weight of current and previous disgust value 
- `surprise`: surprise emotion value
- `disgust_marker`: a value calculated from disgust value from the previous match 

If `disgust_prev` from previous match is positive, `disgust_marker = 1`, else `disgust_marker = -1`. 

# Result

Because of setup of the experiment, if there is a defecting neighbor at beginning of the simulation, every agent will defect and die eventually. Cascading failure happens because each cooperating agent tends to defect to emulate a higher immediate reinforcement, but eventually it will die because its could not receive any reinforcement from its neighbors who also choose to defect. Eventually the entire network is dead. A evolution of a network with a defecting agent sitting at the center is below. 

| Match 0                                                      | Match 17                                                     | Match 29                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image-20210829165904030](assets/image-20210829165904030.png) | ![image-20210829165937882](assets/image-20210829165937882.png) | ![image-20210829170021392](assets/image-20210829170021392.png) |

The proportion of agents that are cooperators, defectors, and dead are shown below. 

![image-20210829171547352](assets/image-20210829171547352.png)

Total and average reinforcement at each match is also plotted. Maximum possible reinforcement is the total reinforcement for the entire network if all the alive agents cooperate. 

![image-20210829171813396](assets/image-20210829171813396.png)

![image-20210829171825181](assets/image-20210829171825181.png)

The evolutions of emotional values are also shown below. 

![image-20210829184055649](assets/image-20210829184055649.png)

![image-20210829184104735](assets/image-20210829184104735.png)

![image-20210829184114167](assets/image-20210829184114167.png)

![image-20210829184124889](assets/image-20210829184124889.png)

![image-20210829184136845](assets/image-20210829184136845.png)

![image-20210829184148592](assets/image-20210829184148592.png)















