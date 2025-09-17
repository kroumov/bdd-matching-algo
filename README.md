# Hungarian Algorithm for Biomedical Data Design

## This Jupyter Notebook provides a practical implementation of the Hungarian Algorithm, a combinatorial optimization algorithm that solves the assignment problem in polynomial time. 

This project focuses on matching doctors to residency positions.

## What is the Assignment Problem?

The assignment problem is a fundamental concept in combinatorial optimization. It seeks to find a one-to-one mapping between two sets of equal size (e.g., a set of doctors and a set of residency positions) to minimize the total cost or maximize the total value of the assignments.

## How the Algorithm Work
The standard Hungarian algorithm is designed to solve the assignment problem for a balanced, square cost matrix (n workers to n jobs). To adapt it for the medical residency matching problem, which is inherently unbalanced (m doctors to n residency positions, where m > n), the problem must be transformed.

This is achieved through the following procedure:

Matrix Expansion: The original m x n preference matrix, where rows represent doctors and columns represent residency programs, is transformed into an n x n square matrix. This is necessary because the algorithm requires an equal number of agents and tasks.

Column Duplication: For residency programs with multiple available slots (e.g., a program has k positions), the corresponding column in the preference matrix is duplicated k-1 times. Each duplicate column is an identical copy, representing an additional, identical slot at the same program.

Introduction of Dummy Rows: To complete the square matrix, a set of (n - m) dummy rows are added. These rows represent hypothetical "unassignment" options for the surplus doctors.

Cost Assignment for Dummy Placeholders: The cost (or rank value) assigned to a doctor being matched to a dummy position is not arbitrary. It is systematically derived from the doctor's composite qualification score-a quantitative metric aggregating relevant criteria such as academic performance (e.g., GPA), scores on standardized exams (e.g., USMLE), strength of letters of recommendation, and assessed personal qualities. This could be any stats. A higher qualification score  ("lottery number") results in a lower cost (or higher preference rank) for the dummy assignment. Consequently, a more highly qualified doctor incurs a greater penalty for being unassigned, making them less likely to be matched to a dummy slot and thus more likely to receive a real residency position in the optimal assignment.

The algorithm's goal is to subtract values from rows and columns to create a matrix full of zeros. If we can assign each worker to a job with a cost of zero in this new matrix, we've found the optimal assignment for the original matrix. In essence, the algorithm is configured to minimize the total cost of the assignment, which now includes the penalty of leaving a highly qualified doctor unmatched, ensuring an optimal and equitable distribution of available residency positions. 

### How to Use This Program

Run the Program: Execute the Python script resident_hospital_problem.py in your preferred Python environment (Jupyter Notebook, Google Colab, or local Python installation).
Follow the Interactive Setup: The program will guide you through importing three required CSV files:

File 1: Doctor-Residency Rankings (preferences matrix)

File 2: Number of Positions per Residency

File 3: Doctor Statistics (for lottery number calculation)


Choose Import Method: For each file, select your preferred import option:

Option 1: Import from raw GitHub URL

Option 2: Import from local file path

## Interpret the Results: 

The final output of the notebook will be the optimal assignment of doctors to residencies and the total cost (or value) of this assignment.Key Components of the Code
Bipartite Graph Representation: The problem is represented as a bipartite graph, with one set of vertices representing doctors and the other representing residencies. The edges between them contain weights corresponding to the cost of an assignment.
Cost Matrix: The algorithm operates on a square cost matrix where each element C(i, j) represents the cost of assigning doctor i to residency j.
Implementation: The notebook contains a Python implementation of the Hungarian Algorithm, which includes steps such as row reduction, column reduction, and finding the optimal solution through a series of augmenting paths.DependenciesThis notebook requires a standard Python environment with the following libraries:numpy, scipy (for a pre-built implementation, if you choose to compare your manual implementation to a library solution)matplotlib (optional, for visualizing the data or results)You can install these dependencies using pip:

```bash
pip install numpy scipy matplotlib
