---
dg-publish: true
tags: CS370
---
# Probability and Bayesian Networks
## Uncertainty
Why is uncertainty important?
* Agents and humans don’t know **everything**
	* but need to **make decisions** anyways!
* Decisions are made in the **absence of information**
The best an agent can do:
* **Know** how uncertain it is, and act accordingly
## Probability
### Frequentist vs. Bayesian
##### Frequentist view:
* Probability of heads = # of heads / # of flips
* probability of heads **this time** = probability of heads (history)
* Uncertainty is **ontological:**
	* pertaining to the world
##### Bayesian view:
* Probability of heads **this time** = agent’s **belief** about flip
* Belief of agent A:
	* based on **previous experience** of agent A
* Uncertainty is **epistemological:**
	* pertaining to knowledge
### Probability Measure
If $X$ is a **random variable** (feature, attribute)
* it can take on values $x$, where $x \in Domain(X)$
* assume $x$ is discrete
$P(X)$ is the probability that $X=x$
**Joint probability** $P(x, y)$ is the probability that $X=x$ and $Y=y$ at the same time
### Axioms of Probability
**Axioms** are things we have to assume about probability
* $P(X) \geq 0$
* $\sum_xP(X=x) = 1.0$
* $P(a\lor b) = P(a)+P(b)$ if $a$ and $b$ are contradictory
	* can’t both be true at the same time
	* $P(win \lor lose) = P(win) + P(lose) = 1.0$
Some notes:
* probability between 0-1 is purely **convention**
* $P(a) = 0$ means you think a is **definitely false**
* $P(a) = 1$ means you think a is **definitely true**
* $0<P(a)<1$ means you have **belief** about the truth of $a$
	* It does **not** mean that $a$ is true to some degree, just that you are ignorant of its truth value
* Probability = measure of **ignorance**
### Independence
Describe a system with $n$ features: $2^{n-1}$ probabilities
![[Pasted image 20250418111454.png]]
* Use **independence** to reduce number of probabilities
	* e.g. radially symmetric dartboard, P(hit a sector)
		* $P(sector) = P(r, \theta)$ where $r=1, \cdots, 4$ and $\theta = 1, \cdots, 8$
		* 32 sectors in total - need to give 31 numbers
	* Assume **radial independence:** $P(r,\theta) = P(r)P(\theta)$
		* only need 7 + 3 = 10 numbers
![[Pasted image 20250418111706.png]]
![[Pasted image 20250418111712.png]]
### Conditional Probability
If $X$ and $Y$ are random variables, the
* $P(x|y)$ is the probability that $X=x$ **given** that $Y=y$
**Incorporate Independence:**
* $P(flies|is\_bird, has\_feathers) = P(flies|is\_bird)$
	* assuming all birds have feathers
**Product Rule (Chain Rule):**
* $P(flies, is\_bird) = P(flies | is\_bird)P(is\_bird) = P(is\_bird|flies)P(flies)$
**Leads to: Bayes’ Rule**
$$P(is\_bird|flies) = \frac{P(flies|is\_bird)P(is\_bird)}{P(flies)}$$
#### Sum Rule
We know
* $\sum_xP(X=x) = 1.0$ and therefore that $\sum_xP(X=x|Y) = 1.0$
This means that **(Sum Rule)**
$$\sum_xP(X=x,Y) = P(Y)$$
We call $P(Y)$ the **marginal** distribution over $Y$
#### Conditional Independence
$X$ and $Y$ are **independent** iff
* $P(X)=P(X|Y)$
* $P(Y)=P(Y|X)$
* $P(X, Y) = P(X)P(Y)$
* So learning $Y$ doesn’t influence beliefs about $X$
$X$ and $Y$ are **conditionally independent** give $Z$ iff
* $P(X|Z) = P(X|Y,Z)$
* $P(Y|Z)=P(Y|X, Z)$
* $P(X, Y|Z) = P(X|Z)P(Y|Z)$
* So learning $Y$ **doesn’t influence beliefs** about $X$ **if you already know $Z$**
	* **does not** mean $X$ and $Y$ are independent
### Expected Values
**Expected value** of a function on $X$, $V(X)$:
$$E(V) = \sum_{x\in Dom(X)}P(x)V(x)$$
where $P(x)$ is the probability of $X=x$
This is useful in **decision making**
* where $V(X)$ is the *utility* of situation $X$
**Bayesian decision making** is then
$$E(V(decision)) = \sum_{outcome}P(outcome|decision)V(outcome)$$
### Value of Independence
* Complete independence reduces both **representation** and **influence** from $O(2^n)$ to $O(n)$
* Unfortunately, complete mutual independence is **rare**
* Fortunately, most domains do exhibit a fair amount of **conditional independence**
* **Bayesian Networks** or **Belief Networks** encode this information
## Bayesian Networks
**Bayesian Networks** or **Belief Networks**
* Directed Acyclic Graph
* Encodes independencies in a graphical format
* Edges give $P(X_i|parents(X_i))$
#### Example
![[Pasted image 20250418114123.png]]
### Correlation and Causality
Directed links in Bayes’ net **$\approx$ causal**
* However, **not always** the case
In a Bayes net, it doesn’t matter
* But, some structures will be **easier to specify**
### Example
>[!example]-
>![[Pasted image 20250418115151.png]]
>![[Pasted image 20250418115214.png]]
>![[Pasted image 20250418115228.png]]
>![[Pasted image 20250418115236.png]]

A **Bayesian Network** or BN over variables $\{X_1, X_2, \cdots, X_N\}$ consists of:
* a **DAG** whose nodes are the variables
* a set of **Conditional Probability Tables** (CPTs) giving $P(X_i|Parents(X_i))$ for each $X_i$
**Example probability tables** for the Coffee Bayes Net:
![[Pasted image 20250418120522.png]]
>[!example]- Another Example
>![[Pasted image 20250418120727.png]]

### Semantics of a Bayes’ Net
>[!tldr] The structure of the BN means that:
>every $X_i$ is **conditionally independent** of all its **non-descendants** given its parents:
>$$ P(X_i|S, Parents(X_i)) = P(X_i|Parents(X_i))$$
>for any subset $S \subseteq NonDescendants(X_i)$

The BN defines a **factorization** of the **joint probability** distribution
* The joint distribution is formed by multiplying the conditional probability tables together
$$P(X_1, X_2, \cdots, X_n) = \prod_i P(X_i|parents(X_i))$$
### Constructing Belief Networks
To represent a domain in a belief network, you need to consider:
* What are the **relevant variables**?
	* What will you observe?
		* this is the **evidence**
	* What would you like to find out?
		* this is the **query**
	* What other features make the model simpler?
		* these are the other variables
* What **values** should these variables take?
* What is the **relationship** between them?
	* this should be expressed in terms of **local influence**
* How does the value of each variable **depend on its parents**?
	* this is expressed in terms of the **conditional probabilities**
#### Three Basic Bayesian Networks
![[Pasted image 20250418134600.png]]
* Database and Test B independent if Report is observed
![[Pasted image 20250418134625.png]]
* Test B and Test A independent if COVID is observed
![[Pasted image 20250418134653.png]]
* Malfunction and COVID are independent if Test B is not observed
### Updating Belief: Bayes’ Rule
Agent has a **prior belief** in a **hypothesis**, $h, P(h)$
* Agent observes some **evidence** $e$ that has a **likelihood** given the hypothesis: $P(e|h)$
The agent’s **posterior belief** about $h$ after observing $e, $P(h|e)$ is given by **Bayes’ Rule:**
$$P(h|e)=\frac{P(e|h)P(h)}{P(e)}=\frac{P(e|h)P(h)}{\sum_h P(e|h)P(h)}$$
* Useful when we have **causal knowledge** and want to do **evidential reasoning**
### Probabilistic Inference
#### Simple Forward Inference (Chain)
![[Pasted image 20250418143030.png]]
###### Computing marginal requires simple forward propagation of probabilities
* $P(B) = \sum_{m,c}P(M=m, C=c, B)$
	* **marginalization - sum rule**
* $P(B) = \sum_{m,c}P(B|m, c)P(m|c)P(c)$
	* **chain rule**
* $P(B)=\sum_{m,c}P(B|m, c)P(m)P(c)$
	* **independence**
* $P(B) = \sum_mP(m)\sum_cP(c)P(B|m,c)$
	* **distribution of product over sum**
###### Same idea when evidence $COVID = true$ “upstream”
* $P(R|c) = \sum_{m,b}P(R,b,m|c)$
	* **marginalization**
* $P(R|c) = \sum_{m,b}P(R|b,m,c)P(b|m,c)P(m|c)$
	* **chain rule**
* $P(R|c) = \sum_{m,b}P(R|b)P(b|m,c)P(m)$
	* **independence** and **conditional independence**
###### With multiple parents the evidence is “pooled”
![[Pasted image 20250418143958.png]]
$$
\begin{align*}
P(Fev) &= \sum_{Flu, M, TS, ET}P(Fev, Flu, M, TS, ET)\\
&= \sum_{Flu, M} P(Fev|M, Flu) \left[\sum_{TS}P(Flu|TS)P(TS)\right]\left[\sum_{ET}P(M|ET)P(ET)\right]
\end{align*}
$$
###### Also works with “upstream” evidence
$$
\begin{align*}
P(Fev|ts, \overline m) &= \sum_{Flu}P(Fev, Flu|\overline m, ts)\\
&= \sum_{Flu}P(Fev|Flu, \overline m, ts)P(Flu|\overline m, ts)\\
&= \sum_{Flu}P(Fev|Flu, \overline m)P(Flu|ts)
\end{align*}
$$
#### Simple Backward Inference
When evidence is downstream of query, then we must reason “backwards”.
* This requires Bayes’ rule
![[Pasted image 20250418145011.png]]
$$
\begin{align*}
P(B|r) &= P(r|B)P(B)/P(r) \propto P(r,B) \text{ (proportional to the joint probability)}\\
P(r, B) &= P(r|B)P(B) \text{ (chain rule)}\\
&= \sum_{m,c}P(m,c,B,r)\\
&= \sum_{m, c}P(m)P(c|m)P(B|m, c)P(r|B, m, c) \text{ (marginalization)}\\
&= \sum_{m,c}P(m)P(c)P(B| m, c)P(r|B) \text{ (independence and conditional independence)}
\end{align*}
$$
Normalizing constant is $\frac{1}{P(r)}$, but this can be computed as $$P(r) = \sum_bP(r, b)$$
### Variable Elimination
More general algorithm:
* applies sum-out rule repeatedly
* distributes sums
#### Factors
a **factor** is a representation of a function from a tuple of random variables into a number
* We will write factor $f$ on variables $X_1, \cdots, X_j$ as $f(X_1, \cdots, X_j)$
* We can assign some or all of the variables of a factor
	* this is **restricting** a factor:
		* $f(X_1 = v_1, X_2, \cdots, X_j)$, where $v_1 \in dom(X_1)$, is a factor on $X_2, …, X_j$
		* $f(X_1=v_1, X_2=v_2, \cdots, X_j=v_j)$ is a number that is the **value of $f$** when each $X_i$ has value $v_i$
The former is also written as $f(X_1, X_2, \cdots, X_j)_{X_1=v_1}$, etc.
##### Multiplying Factors
The **product** of factor $f_1(X, Y)$ and $f_2(Y, Z)$, where $Y$ are the variables in common, is the factor $(f_1\times f_2)(X, Y, Z)$ defined by:
$$(f_1\times f_2)(X, Y, Z) = f_1(X, Y)f_2(Y, Z)$$
##### Summing out variables
We can **sum out** a variable, say $X_1$ with domain $\{v_1, \cdots, v_k\}$, from factor $f(X_1, \cdots, X_j)$, resulting in a factor on $X_2, \cdots, X_j$ defined by:
$$\sum_{X_1}f(X_1, X_2, \cdots, X_j) = f(X_1 = v_1, \cdots, X_j) + \cdots + f(X_1 = v_k, \cdots, X_j)$$
#### Evidence
If we want to compute the posterior probability of $Z$ given evidence $Y_1=v_1\land \cdots \land Y_j=v_j$:
$$
\begin{align*}
P(Z|Y_1=v_1, \cdots, Y_j = v_j) &= \frac{P(Z, Y_1=v_1, \cdots, Y_j = v_j)}{P(Y_1=v_1, \cdots, Y_j = v_j)}\\
&=\frac{P(Z, Y_1=v_1, \cdots, Y_j = v_j)}{\sum_ZP(Z, Y_1=v_1, \cdots, Y_j = v_j)}
\end{align*}
$$
The computation reduces to the **joint probability** of $P(Z, Y_1=v_1, \cdots, Y_j = v_j)$, **normalize** at the end
* can also restrict the query variable
	* e.g. compute: $P(Z=z| Y_1=v_1, \cdots, Y_j = v_j)$
#### Probability of a conjunction
Suppose the variables of the belief network are $X_1, \cdots, X_n$
* To compute $P(Z, Y_1=v_1, \cdots, Y_j = v_j)$, we **sum out the variables other than query $Z$ and evidence $Y$**
	* $Z_1, \cdots, Z_k = \{X_1, \cdots, X_n\} - \{Z\} - \{Y_1, \cdots, Y_j\}$
* We order the $Z_i$ into an **elimination ordering** $Z_1, \cdots, Z_k$
$$
\begin{align*}
P(Z, Y_1=v_1, \cdots, Y_j = v_j) &= \sum_{Z_k}\cdots\sum_{Z_1}P(X_1, \cdots, X_n)_{Y_1=v_1, \cdots, Y_j = v_j}\\
&= \sum_{Z_k}\cdots\sum_{Z_1}\prod_{i=1}^nP(X_i|parents(X_i))_{Y_1=v_1, \cdots, Y_j = v_j}
\end{align*}
$$
##### Computing sums of products
Computation in belief networks reduces to **computing the sums of products**
* How can we compute $ab+ac$ efficiently?
	* **Distribute** out the $a$ giving $a(b+c)$
* How can we compute $\sum_{Z_1}\prod_{i=1}^nP(X_i|parents(X_i))$ efficiently?
	* Distribute out those factors that don’t involve $Z_1$
#### Variable Elimination Algorithm
To compute $P(Z|Y_1=v_1\land \cdots \land Y_j=v_j)$:
* Construct a **factor for each conditional probability**
* **Restrict** the observed variables to their observed values
* **Sum out** each of the other variables according to some **elimination ordering:**
	* for each $Z_i$ in order starting from $i=1$:
		* collect all factors that contain $Z_i$
		* multiply together and sum out $Z_i$
		* add resulting new factor back to the pool
* **Multiply** the remaining factors
* **Normalize** by dividing the resulting factor $f(z)$ by $\sum_Zf(Z)$
##### Summing our a Variable
To sum out a variable $Z_j$ from a product $f_1, \cdots, f_k$ of factors:
* **Partition** the factors into
	* those that don’t contain $Z_j$, say $f_1, \cdots, f_i$,
	* those that contain $Z_j$, say $f_{i+1}, \cdots, f_k$
We know:
$$\sum_{Z_j}f_1\times \cdots \times f_k = f_1 \times \cdots \times f_i \times \left(\sum_{Z_j}f_{i+1}\times \cdots \times f_k\right)$$
* **Explicitly construct** a representation of the rightmost factor $\left(\sum_{Z_j}f_{i+1}\times \cdots \times f_k\right)$
* **Replace** the factors of $f_{i+1}, \cdots, f_k$ by the new factor
##### Notes on Variable Elimination
* Complexity is **linear** in number of variables, and **exponential** in the size of the largest factor
* When we create new factors: sometimes this **blows up**
* Depends on the **elimination ordering**
* For **polytrees:**
	* work outside in
* For general BNs this can be hard
* simply **finding** the optimal elimination ordering is NP-hard for general BNs
* inference in general is NP-hard
#### Variable Ordering
##### Polytrees
![[Pasted image 20250418165015.png]]
* eliminate **singly-connected** nodes $(D, A, C, X_1, \cdots, X_k)$ first
* Then no factor is ever larger than original CPTs
	* if you eliminate $B$ first, a **large factor** is created that includes $A, B, C, X_1, \cdots, X_k$
##### Relevance
![[Pasted image 20250418184906.png]]
Certain variables have **no impact**
* In ABC network above, computing $P(A)$ **does not require** summing over $B$ and $C$
![[Pasted image 20250418185005.png]]
Can restrict attention to **relevant variables:**
* Given query $Q$ and evidence $\textbf{E}$, **complete** approximation is:
	* $Q$ is relevant
	* if any node is relevant, its parents are relevant
	* if $E \in \textbf{E}$ is a descendent of a relevant variable, then $E$ is relevant
**Irrelevant variable:** a node that is not an ancestor of a query or evidence variable
* This will only remove irrelevant variables, but may not remove them all
### Probability and Time
![[Pasted image 20250418214157.png]]
* A node repeats over **time**
* **Explicit** encoding of time
* chain has length = amount of time you want to model
* **event-driven** times or **clock-driven** times
	* e.g. **Markov chain**
#### Markov Assumption
$P(S_{t+1}|S_1, \cdots, S_t) = P(S_{t+1}|S_t)$
This distribution gives the **dynamics** of the Markov Chain
#### Hidden Markov Models (HMMs)
![[Pasted image 20250418214404.png]]
Add: observations $O_t$ 
* always observed, so the node is square
Observation function $P(O_t|s_t)$
* Given a sequency of observations $O_1, \cdots, O_t$, can estimate **filtering:**
	* $P(S_t|O_1, \cdots, O_t)$
* Or **smoothing**, for $k>t$
	* $P(S_k|O_1, \cdots, O_t)$
#### Speech Recognition
![[Pasted image 20250418214659.png]]
* **Observations:** audio features
* **States:** phonemes
* **Dynamics:** models
	* e.g. co-articulation
* **HMMs:** words
* Can build hierarchical models (e.g. sentences)
#### Dynamic Bayesian Networks (DBNs)
In general, any Bayesian network can repeat over time: **DBN**
* Many examples can be solved with **variable elimination**
* may become too complex with enough variables
* **event-drive** times or **clock-driven** times
#### Stochastic Simulation
**Idea:** probabilities $\iff$ samples
* Get probabilities from samples:
	* ![[Pasted image 20250418221911.png]]
* If we could **sample** from a variable’s (posterior) probability, we could **estimate** its (posterior) probability
##### Generating Samples from a distribution
![[Pasted image 20250418222206.png]]
For a variable $X$ with a discrete domain or a one-dimensional real domain:
* **Totally order** the values of the domain of $X$
* Generate the **cumulative probability distribution:**
	* $f(x) = P(X\leq x)$
* Select a value $y$ **uniformly** in the range $[0,1]$
* Select $x$ such that $f(x)=y$
### Forward Sampling in a Belief Network
* Sample the variables **one at a time;**
* Sample **parents** of $X$ **before** you sample $X$
	* Given values for the parents of $X$, sample from the **probability of $X$ given its parents**
* for samples $s_i, i=1, \cdots, N$:$$P(X=x_i)\propto \sum_{s_i}\delta(x_i)=N_{X=x_i}$$where $\delta(x_i) = 1$ if $X=x_i$ in $s_i$ and 0 otherwise
#### Example
![[Pasted image 20250418223034.png]]
* A: 2/3 based on first 7 samples
