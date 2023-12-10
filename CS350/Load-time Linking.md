# Load-time Linking
> [!tldr] Linked adjusts addresses of symbols
> ![[Pasted image 20231209131348.png]]

## Idea
* Link when process is executed, not at compile time
	* Adjust references within program

## Problems
* How to enforce protection?
* How to move once already in memory?
* What if no contiguous free region fits program?