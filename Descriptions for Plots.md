## Status_Comparison 

When `T_i = 0.5` The number of cooperators drops significantly at beginning of the match because of two reasons. The first reason is that many cooperators are turning into defectors very quickly. The second reason is that some cooperators die even before turning into defectors. The number of dead agents also rise substantially at beginning of the match. The number of defectors increases at a much slower rate because many defectors die in a few matches after the defect. Eventually, all the agents die because there are not enough cooperators to provide reinforcement: defectors and dead agents do not reinforce others during interactions. 

When `T_i = 0.75`, the number of cooperators and defectors eventually comes. to an equilibrium: all the defectors are dead.  Since we have a relatively high survival threshold, namely 0.75, the defectors do not successfully sabotage the entire network. There is about 70 percent of cooperators survive. The number of defectors increases slightly at beginning of the match, but soon drops and eventually declines to zero. 

## TotalReinforcement_Comparison 

In the total reinforcement graph, `Maximum Possible Reinforcement` shows the total reinforcement when assuming that all alive agents are cooperators. 

When `T_i = 0.5`, total reinforcement for cooperators drops significantly because more cooperators are facing defecting neighbors and there are more dead agents in the network. Total reinforcement for defectors does not increase considerably. One possible explanation is that the number of defectors is relatively small, so the total reinforcement is also smaller. 

When `T_i = 0.75`, total reinforcement for cooperators drops because some cooperators meet dead or defecting agents. However, when defectors are dead,  total reinforcement for cooperators remains at a steady level. 

## AverageReinforcement_Comparison

When `T_i = 0.5`, We can see that although the average reinforcement for defectors is higher at the first few matches, it drops considerably. In match 7, the average reinforcement of defectors is lower than that of cooperators. Although the average reinforcement of defectors fluctuates, it is below that of cooperators. The average reinforcement of cooperators slowly drops at the beginning because the number of cooperators receiving full reinforcement is still high. But the average reinforcement for cooperators starts dropping more rapidly after match 20. 

When `T_i = 0.75`, the change in average reinforcement for defectors fluctuates more violently because at a higher survival threshold, agents are dying at a more rapid pace. The average reinforcement for cooperators remains at a stable level. 

## Fear_Comparison 

When `T_i = 0.5`, the average fear emotion for defectors rises exponentially at first but then levels off at around 0.25. The average fear emotion for cooperators slowly increases until match 35, and then increases significantly.  Both the cooperators and defectors have about 0.5 fear emotion value at the end of the simulation. 

When `T_i = 0.75`, the average fear emotion for defectors rises significantly before match 5 but fluctuates violently afterward. The line plot for defectors ends at about match 17 because after it all defectors are dead. The average fear emotion for cooperators remains steady. 

## Happiness_Comparison 

When `T_i = 0.5`, the average happiness emotion for defectors rises slightly at first but soon drops significantly before leveling off at around -0.25. For cooperators, average happiness increases slightly at first and then drops slowly.  

When `T_i = 0.75`, the average happiness emotion for defectors drops significantly and fluctuates before coming to an end at match 17. The average happiness emotion remains steady for cooperators. 

## Anger_Comparison 

When `T_i = 0.5`, the average anger emotion for both defectors and cooperators drops slightly at beginning of the simulation, but both start increasing. Average anger emotion for defectors increases at a higher rate than that of cooperators. The average anger emotion for both cooperators and defectors terminates at around 0.5. 

When `T_i = 0.75`, average anger emotion increases and fluctuates before ending at match 17.  The average anger emotion remains steady for cooperators. 

## Sadness_Comparison 

When `T_i = 0.5`, the average sadness emotion for both cooperators and defectors increases, but that of defectors increases at a faster rate. The average sadness emotion for both cooperators and defectors terminate at around 0.5. 

When `T_i = 0.75`, average sadness emotion increases and fluctuates before ending at match 17.  The average sadness emotion remains steady for cooperators. 

## Surprise_Comparison

When `T_i = 0.5`, the average surprise emotion for both cooperators and defectors remains at -1 for the first five matches when there are no dead agents. After match five, the average surprise emotion for both cooperators and defectors increases, but that of defectors increases more rapidly, because defectors are having more dead neighbors than cooperators do. The average surprise emotion for both cooperators and defectors is 1 at the end of the simulation. 

When `T_i = 0.75`, the average surprise emotion of defectors fluctuates significantly, while that of cooperators remains steady. 

## Disgust_Comparison

When `T_i = 0.5`, the average disgust emotion for both cooperators and defectors remains at -1 for the first five matches when there are no dead agents. After match five, the average disgust emotion for both cooperators and defectors increases, but that of defectors increases more rapidly, because defectors are having more dead neighbors than cooperators do. The average disgust emotion for both cooperators and defectors is around 0.5 at the end of the simulation. 

When `T_i = 0.75`, the average disgust emotion of defectors fluctuates significantly, while that of cooperators remains steady. 

