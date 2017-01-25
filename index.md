# Homework 0

## About Me
My name is Quico Spaen. I am a third year PhD student in the department of Industrial Engineering & Operations Research at UC Berkeley as well as a MSc student in Computer Science. My research focuses on algorithms for combinatorial optimization and Machine Learning. Currently I am working on solving a medical imaging problem in neuroscience with algorithms from combinatorial optimization and on the development of Bayesian optimization methods for Deep Learning. Furthermore, I am interested in transportation related topics.

In my free time I enjoy cycling, other outdoor activities, and good food.

[LinkedIn](https://www.linkedin.com/in/quicospaen)

## Parallel algorithms in combinatorial optimization: Branch-and-bound
Combinatorial optimization involves finding the best solution from a countable (typically finite) set. In most cases, the set consists of the set or subset of the integer numbers. Combinatorial optimization is typically much harder than continuous (convex) optimization. Within combinatorial optimization there are many famous problems such as the [Travelling Salesperson Problem (TSP)](https://www.wikiwand.com/en/Travelling_salesman_problem).

To solve difficult problems such as TSP, a common approach is to use a branch-and-bound  algorithm. This a tree-search algorithm where at each node in the tree a continuous version of the problem is solved. The continuous version gives a lower bound on the objective of the best solution. If the continuous solution at a node is integer, then the algorithm terminates stops searching this branch. If the solution is not integer (for example `x=4.5`), the algorithm branches the tree and restricts the variables (branch 1: `x <= 4`, branch 2: `x >=5`). This restricts the set of solutions for each branch. Furthermore, branches are pruned when the lower bound for a branch is worse than the best integer solution found (the branch cannot contain a better solution). This continues until the tree is fully explored and the optimal solution has been found.

Originally, branch-and-bound was used as a sequential algorithm. However, it is inherently a parallel algorithm. At any given time, a large number of nodes need to be explored. Instead of exploring these nodes sequentially, this can be done in parallel. To do this efficiently, very efficient solvers have been developed to solve sparse systems of linear equations. Solving these systems is necessary to find the continuous solution at each of the nodes.

A major challenge in parallelizing this algorithm are the global decisions that should be made by the algorithm. Challenging coordination decisions include but are not limited too:
- Which nodes should be processed first? Depth-first or Breadth-first?
- How should the best solution value be communicated?
-
For many of these questions heuristic solutions have been developed based on extensive experimental analysis.
