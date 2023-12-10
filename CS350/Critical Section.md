# Critical Section
> [!tldr] Code that access a shared variable
> Must not be concurrently executed by more than one thread

> [!example]
> ```c
> int total = 0;
> void add() {
>   for (int i=0; i<N; i++) {
>     total++;
>   }
> }
> void sub() {
>   for (int i=0; i<N; i++) {
>     total--;
>   }
> }
> ```
> If one thread executes `add` and one executes `sub`, we won’t know the value for `total`

> [!question] Why does this happen
> ```c
> /* Thread 1 */
> void add() {
>   for (int i=0; i<N; i++) {
>     lw r9, 0(r8) /* total++ */
>     addi r9, 1
>     sw r9, 0(r8)
>   }
> }
> ```
> ```c
> /* Thread 2 */
> void sub() {
>   for (int i=0; i<N; i++) {
>     lw r9, 0(r8) /* total++ */
>     subi r9, 1
>     sw r9, 0(r8)
>   }
> }
> ```
> At the assembly level, these instructions are actually 3 different instructions
> * Different execution orders will result in different results



