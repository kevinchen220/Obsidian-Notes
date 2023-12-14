---
dg-publish: true
---
# Process Priority
## `p_nice`
User-settable weighting factor (-20, 20)
* Negative numbers give higher priority
## `p_estcpu`
Per-process estimated CPU usage
* Incremented whenever timer interrupt found process running
* Decayed every second while process runnable
$$
p_{estcpu} = \frac{2\times load}{2\times load +1}\times p_{estcpu} + p_{nice}
$$
* Where load is the sampled average of length of the the run queue plus short-term sleep queue over last minute
* **The higher the load, the less p_estcpu decreases**
Run queue is determined by p_usrpri/4 where
$$
p_{usrpri} = 50 + \frac{p_{estcpu}}{4}+2 \times p_{nice}
$$
* Clipped at 127
## `p_slptime`
`p_estcpu` is not updated when the thread is asleep
When the thread becomes runnable again
$$
p_{estcpu} = (\frac{2\times load}{2\times load +1})^{p_{slptime}} + p_{nice}
$$

