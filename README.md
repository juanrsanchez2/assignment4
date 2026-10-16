# Assignment4
Advanced & Real-Time CPU Scheduling Simulator
## Link to main.cpp and README.md
https://github.com/juanrsanchez2/assignment4/blob/85f828ad23c94d74146d580d5752d82e91ba2216/main
https://github.com/juanrsanchez2/assignment4/blob/85f828ad23c94d74146d580d5752d82e91ba2216/README.md

## Overview of Assignment4
This program expands Assignment3 and the goal is to fix starvation with a technique called Aging, then compare scheduling performance metrics of RM, EDF.

## Workload
The simulation generates 1,000 processes using:
- Poisson arrival process with an arrival rate of 2
- Exponentially distributed service times averaging 1.0 ms
- The same generated processes for both scheduling algorithms

## Non-Preemptive Priority Scheduling with Aging
Each process gets an initial priority between 1 and 10(10 being the lowest). Processes waiting in the ready queue get their priority increased every 10 ms by decreasing their priority number. When the CPU becomes available, the highest priority is selected. If two processes have the same priority, the process with the smaller ID is selected first.

## Multilevel Feedback Queue (MLFQ)

MLFQ uses two queues:
- Q0: High-priority queue using Round-Robin scheduling with a 2 ms quantum
- Q1: Low-priority queue using First-Come, First-Served scheduling

New processes enter Q0. If a process uses its entire quantum and its not finished, it is demoted to Q1.
Processes in Q1 will only execute when Q0 is empty. Every 20 ms, priority boosting moves processes from Q1 back to Q0 so that indefinitely starvation does not happen.

## Part 2: Real-Time Scheduling Algorithms - Periodic Workload
The simulation uses three periodic tasks:
- Task 1: Period = 4 ms, Execution Time = 1 ms
- Task 2: Period = 6 ms, Execution Time = 2 ms
- Task 3: Period = 12 ms, Execution Time = 3 ms

Each task has a deadline equal to its period.

The hyperperiod is calculated using the least common multiple:

LCM(4, 6, 12) = 12 ms

Both scheduling algorithms simulate execution over one 12 ms hyperperiod.

### Rate-Monotonic Scheduling (RM)

Rate-Monotonic is a preemptive scheduling algorithm that assigns fixed priorities based on task periods.

Tasks with shorter periods receive higher priorities.

The priority order is:

1. Task 1 (4 ms)
2. Task 2 (6 ms)
3. Task 3 (12 ms)

Higher-priority tasks can preempt lower-priority tasks when they become ready.

### Earliest-Deadline-First Scheduling (EDF)

Earliest-Deadline-First is a preemptive scheduling algorithm that dynamically assigns priorities based on absolute deadlines.

The ready task with the earliest deadline is selected to execute.

Unlike RM, EDF priorities can change as new jobs arrive.
