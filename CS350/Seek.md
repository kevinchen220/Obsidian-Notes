---
dg-publish: true
---
# Seek
### A seek consists of four phases
1. Speedup - Accelerate arm to max speed or halfway point
2. Coast - At max speed
3. Slowdown - stops arm near destination
4. Settle - adjusts head to actual desired track
Very short seeks dominated by settle time (~1ms)
Short (200-400 cycles) seeks dominated by speedup

## Details
Head switch times comparable to short seek times
* May also require head adjustments
> [!question] Why do settles take longer for writes than for reads
> * If read strays from track, we can catch the error
> * If write strays from track, we overwritten other [[tracks]]

The disk controller circuit keeps table of pivot motor power
* **Maps the seek distance to the power and time needed** to move that distance
* 

