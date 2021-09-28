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

If anger value from previous match is positive, `anger_marker = 1`, else `anger_marker = 0`. 

### Sadness 

`sadness = a_sadness * sadness_marker + (1 - a_sadness) * sadness_curr`

- `a_sadness`: a parameter controlling the weight of current and previous sadness value 
- `sadness_marker`: a value calculated from sadness value from the previous match 
- `sadness_curr`: sadness value for interactions in current match

At the beginning of each match, `sadness_curr` is set to 0. For each interaction, `sadness_curr -= 1/v_i`  if  `r > 0`, else  `sadness_curr += 1/v_i`  

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

If `disgust_prev` from previous match is positive, `disgust_marker = 1`, else `disgust_marker = -1`. 

# Result

Because of setup of the experiment, if there is a defecting neighbor at beginning of the simulation, every agent will defect and die eventually. Cascading failure happens because each cooperating agent tends to defect to emulate a higher immediate reinforcement, but eventually it will die because its could not receive any reinforcement from its neighbors who also choose to defect. Eventually the entire network is dead. A evolution of a network with a defecting agent sitting at the center is below for `T_i = 0.5`. 

| Match 0                                                      | Match 17                                                     | Match 29                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image-20210829165904030](assets/image-20210829165904030.png) | ![image-20210829165937882](assets/image-20210829165937882.png) | ![image-20210829170021392](assets/image-20210829170021392.png) |

To play around with parameters, we choose three values for `Ti`, which controls the survival threshold of agents in the network. 

- `Status Graph` describes the proportion of agents beging cooporators, defectors, or dead agents throughout the matches. 
- `Total Reinforcement Graph` illustrate the total reinforcement received by all cooporators, defectors. Maximum possible reinforcement is achieved when assuming that all agents in the network are cooporators. 
- `Average Reinforcement Graph` illustrate the average reinforcement received by all cooporators, defectors. Maximum possible reinforcement is achieved when assuming that all agents in the network are cooporators. 
- `Average Fear Graph`  is the graph of average fear emotion versus matches 
- `Average Happiness Graph`  is the graph of average happiness emotion versus matches 
- `Average Sadness Graph`  is the graph of average sadness emotion versus matches 
- `Average Surprise Graph`  is the graph of average surprise emotion versus matches 
- `Average Disgust Graph`  is the graph of average disgust emotion versus matches 

| Graph                    | $T_i = 0.25$                                                 | $T_i = 0.5$                                                  | $ T_i = 0.75$                                                |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Status Graph             | ![image-20210901131415849](assets/image-20210901131415849.png) | ![image-20210901131347784](assets/image-20210901131347784.png) | ![image-20210901131445693](assets/image-20210901131445693.png) |
| Total Reinforcement      | ![image-20210901131653255](assets/image-20210901131653255.png) | ![image-20210901131717549](assets/image-20210901131717549.png) | ![image-20210901131521842](assets/image-20210901131521842.png) |
| Average Reinforcement    | ![image-20210901131918936](assets/image-20210901131918936.png) | ![image-20210901131843657](assets/image-20210901131843657.png) | ![image-20210901131949567](assets/image-20210901131949567.png) |
| Average Fear Graph       | ![image-20210901132528914](assets/image-20210901132528914.png) | ![image-20210901132335852](assets/image-20210901132335852.png) | ![image-20210901132224535](assets/image-20210901132224535.png) |
| Average Happiness Graph  | ![image-20210901132555523](assets/image-20210901132555523.png) | ![image-20210901132417434](assets/image-20210901132417434.png) | ![image-20210901132608030](assets/image-20210901132608030.png) |
| Average Anger Emotion    | ![image-20210901132749619](assets/image-20210901132749619.png) | ![image-20210901132818476](assets/image-20210901132818476.png) | ![image-20210901132733687](assets/image-20210901132733687.png) |
| Average Sadness Emotion  | ![image-20210901133025993](assets/image-20210901133025993.png) | ![image-20210901132936825](assets/image-20210901132936825.png) | ![image-20210901133214816](assets/image-20210901133214816.png) |
| Average Surprise Emotion | ![image-20210901133150461](assets/image-20210901133150461.png) | ![image-20210901133133181](assets/image-20210901133133181.png) | ![image-20210901133230569](assets/image-20210901133230569.png) |
| Average Disgust Emotion  | ![image-20210901133159955](assets/image-20210901133159955.png) | ![image-20210901133010189](assets/image-20210901133010189.png) | ![image-20210901133239639](assets/image-20210901133239639.png) |

