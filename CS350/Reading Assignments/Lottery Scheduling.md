---
dg-publish: true
---
# Lottery [[Scheduling]]

> [!tldr] A randomized resource allocation mechanism

## Key Concepts
* Instead of assigning a fixed priority to each process, lottery scheduling assigns tickets to each process. 
	* Process with more tickets has a high probability of being selected
* Tickets are distributed among processes based on their desired share of resources
* Scheduler selects a winning ticket randomly, and the process holding that ticket gets the resource for a specified period
### Flexibility and Fairness
* Allows processes to influence their chances of obtaining resources by acquiring or relinquishing tickets
* All processes have a chance to win the lottery, ensuring fairness
### Advantages
* Provides better responsiveness and adaptability in a multi-user environment compared to [[Round Robin Scheduling]]
* Supports proportional-share resource allocation