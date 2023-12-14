---
dg-publish: true
---
# Priority Donation
## Direct Priority Change
##### Thread priority changed to thread which immediately depends on it
* H depends on L so L’s priority = max(L, H)
## Indirect Priority Change
##### Thread priority changed to thread which indirectly depends on it
H depends on M which depends on L
* L’s priority = max(L,M,H)
