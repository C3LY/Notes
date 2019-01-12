# Summary (up to L6-Code Reusing)

## The basics

* What is a problem specification

  * A high level external description of **what** the task is

* Implementation

  * How you are carrying out the task

  _CHECK DEFINITION ON WORKSHEET 7_

> An algorithm is an **ordered** list of basic operations, for which every valid input determines a finite sequence of operations to be performs and halts. It produces some output

Difference between an algorithm and a procedure/programming languages

Algorithms are for human-human communication

Programming languages are for human-computer communication

> Turing Complete - any computation can be written in this language

Bounded iteration - ```for``` - is redundant as it can be written as a ```while``` loop.

------

### Developing an algorithm

* Top Down approach
  * Tackle sub-problems
* Bottom Up solving
  * Examine simple instances

##### Sequential Search

######FOR LOOP

**input**: Array A[1...n], item M

**output**: true, if M in A, false otherwise FOUND ← false

```pseudocode
FOUND ← false
for i ← 1 to n do
	if A[i]= M then
    	FOUND ← true
 return FOUND
```

###### WHILE LOOP

```pseudocode
PTR ← 1
while not FOUND and PTR <= n do
	if A[PTR]= M then
		FOUND ← true
PTR ← PTR +1
return FOUND
```

#### Selection Sort

**Input**: Array A[1...n]

**Output**: Array A sorted

_check this out on the powerpoint_

```pseudocode
for i←1 to (n-1) do
	MINPTR ← i
	for j ← (i + 1) to n do
		if A[j] < A[MINPTR] then
		MTR ← j
		A[i] ↔ A[MINPTR]
return A
```

 

#### BubbleSort

**Input**: Array A[1...n]

**Output**: Array A sorted

```pseudocode
for i←1 to (n-1) do
	//maintains A[(n-i + 1)..n]
	for j ← 1 to (n-1) do
		//bubbles up largest element in A[1...(n-i + 1)]
		if A[j]>A[j+1] then
			A[j] ↔ A[j+1]
```

_Because of invariant last iteration of loop unnecessary - as swapping itself (Stop one before the end, what happens for an empty array)_

##### Partial Correctness

* for every legal input, if the algorithm original halts then the output satisfies the required relationship with the original input
  * Dealing when it terminates

##### Total Correctness

* for every legal input, Halts every time and the output satisfies the required relationship with the original input every time

## Assertions

maths statements about the program variables at a checkpoint

> ASSERTIONS ARE TRUE AND WILL ALWAYS BE TRUE

Invariant - something that doesn't change

Initial assertions: captures requirements on legal inputs

Final assertion: Determines properties of data output

Loop assertions: Must be true every time control goes through the loop

####Example:

**Input**: Array[1..n]

**Output**: largest...

```pseudocode
↤[INITIAL PROP] {n ≥ 1}
PTR ←  1
CMAX ← A[PTR]
//assert: {CMAX = A[1]}
while PTR ≠ n do
	↤[LOOP PROP] //assert: {CMAX is largest element in A[1...PTR]}
	PTR ← PTR + 1
	if A[PTR] > CMAX then
		CMAX ← A[PTR]
↤[FINAL PROP] //assert:{CMAX is largest element in A}
return CMAX
```

> Never write a loop, without knowing why it will terminate, for every possible input

#### Example:

**Input:** number ≥ 0

**Output:**: k*k

```pseudocode
//assert: k >= 0
x ← 0
y ← 0
//assert: y = x * k
while x ≠ k do
	//assert: y = x *k 			the loop invariant
	y ≠ y + k
	x ≠ x + 1
//assert: y = x * k amnd x = k
return Y
//assert: k * k returned
```

* The loop invariant [y=x*k] shows how all variables are linked together - **it uses all the variables in the code**

> Good to have a metric -reducing each time and doesn't go negative - the _gap_ between PTR and n reduces

Floyd-Hoare logic {Pre} C {Post}

_WHAT IS THE DEFINITION OF AN INVARIANT? WHAT IS THE INVARIANT THEOREM_

###### Invariant in a **while** loop

> State or use the loop invariance theorem

```pseudocode
← Inv
While Bool do
	← Inv
	Body
← Inv and not Bool
```



>```SUM = 1+…+ PTR``` can be written as $\sum_{PTR}^{i=1} {2i}=1+...+PTR$

###### Invariant in a **for** loop

For _i_ ← 1 **to** n **do** Body

Suppose Inv( _i_ ) is a mathematical statement about _i_

Example : $$SUM = \sum^{I}_{k=1}{A[i]}$$

* If Inv(0) is true before the For-statement starts
* If {Inv( _i_ )} Body {Inv( _i_+1 )}
  * Inv( _i_ )  is preserved by the Body
* Then
  * **when** the for-loop terminates the property Inv(n) is true

```pseudocode
⇐ [inv(0)]
for i <- 1 to n do
	Body
	⇐[Inv(i)]
⇐[Inv(n)]
```

