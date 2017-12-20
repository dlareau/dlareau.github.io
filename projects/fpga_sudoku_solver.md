---
layout: project_page
title: FPGA Constraint (Sudoku) Solver
category: fpga_sudoku_solver
---

This was a project for one of the graduate courses I took at CMU. 

We were tasked with implementing something in both hardware and software and analyzing the performance benefits of each. Our group chose to implement a Sudoku solver with the thought that it would represent the general category of constraint solving. With the amount of time we were given to do this task, I will admit that we weren't able to produce terribly clean or well implemented code, but it definitely works. 

You can find the code on [Github](https://github.com/dlareau/643_final_project). The file of particular note is sudoku.sv, the rest is mostly Vivado configurations and other I/O code. 

Our implementation creates 81 "cells" which each receive the current state of other cells in their row, column, and 3x3 grid. Each cell then uses this information in parallel to decide what its possible values can be. Once there is only one possible value left for a cell, "it fills itself in" and then in the next clock cycle other cells are able to use that cell's data for their own calculations. This solution is limited to puzzles that don't require "guessing", although with more time we had ideas for how each cell could have their own stack for guessing and backtracking. 

We were able to solve nearly any puzzle of a 9x9 format in 3 clock cycles after the initial state was populated. A much lower number than we expected. 