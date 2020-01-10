# Objective

Model concurrent systems with Promela using shared variables and message passing. Use SPIN to prove properties of concurrent systems.

# Reading

  * [spin.md](https://bitbucket.org/byucs329/byu-cs-329-lecture-notes/src/master/spin/spin.md)
  * [spinroot.com](http://spinroot.com/spin/whatispin.html)

# Problems

## 1. Download and Install SPIN (10 points)

Download and install SPIN. Create a screen shot showing it working on the machine. See [Spin](https://wiki.cs.byu.edu/cs-486/tools) for help.

## 2. Prove Mutual Exclusion (30 points)

Model the following mutual exclusion algorithm with Promela (25 points) and prove its *correctness* or *incorrectness* with SPIN (5 points).

```c
/*
R. W. Doran and L. K. Thomas.  Variants of the software solution to
mutual exclusion.  Information Processing Letters 10(4--5):206--208,
1980.

Process A                           Process B
  1. A_needs := true;                    B_needs :=  true;
  2. if B_needs then begin               if A_needs then begin
  3.   if turn = 'B' then begin            if turn = 'A' then begin
  4.     A_needs := false;                   B_needs := false;
  5.     wait until turn = 'A';              wait until turn = 'B';
  6.     A_needs := true;                    B_needs := true;
  7.   end;                                end;
  8.   wait until !B_needs;                wait until !A_needs;
  9. end;                                end;
 10. CRITICAL SECTION                    CRITICAL SECTION
 11. turn := 'B';                        turn := 'A';
 12. A_needs := false;                   B_needs := false;
 13. NON-CRITICAL SECTION                NON-CRITICAL SECTION
*/
```

## 3. Farmer Crosses River (30 points)

Write a Promela model for the below problem (25 points) and use SPIN to find a solution (5 points). 

*A farmer wants to cross a river and take with him a wolf, a goat, and a cabbage. There is a boat that can fit himself plus either the wolf, the goat, or the cabbage. If the wolf and the goat are alone on one shore, the wolf will eat the goat. If the goat and the cabbage are alone on the shore, the goat will eat the cabbage. How can the farmer bring the wolf, the goat, and the cabbage across the river?*

## 4. Elevator Design (30 points)

This problem is Exercise 5.5 in Principles of Model Checking (page 321). Consider an elevator system that services `N > 0` floors numbered `0` through `N-1`. There is an elevator door at each floor with a call-button and an indicator light that signals whether or not the elevator has been called. The system must have the following properties:

  1. Any door on any floor is never open when the elevator is not present
  2. A requested floor will be served eventually
  3. The elevator repeatedly returns to floor 0
  4. When the top floor is requested, the elevator serves it immediately and does not stop on any floor on the way up

**Part 1** (4 points) Identify which properties relate to *safety* and which properties relate to *liveness*.

**Part 2** (12 points) Create a Promela model for the elevator. 

**Part 3** (12 points) Add assertions to prove the safety properties hold in the model. 

# Submission

Submit the URL for the pull request to [canvas.byu.edu](http://canvas.byu.edu). Be sure that the files are clearly organized so that it is easy for the grader to grade. Include the command used in SPIN for the verification in an obvious comment in each Promela file.
