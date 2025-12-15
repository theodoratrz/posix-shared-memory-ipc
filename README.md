# POSIX Shared Memory IPC System

A system programming project demonstrating **inter-process communication**
using **POSIX shared memory** and synchronization primitives.

The application follows a client–server style interaction model, where
multiple processes communicate through shared memory segments rather
than sockets or files.

## Key Concepts

- POSIX shared memory 
- Inter-process communication (IPC)
- Synchronization of shared resources
- Concurrent access control
- Low-level systems programming

## Problem Description

The project implements a variation of the **Salad Makers synchronization problem**:
![image](https://user-images.githubusercontent.com/61420354/199811994-98800ae4-4db8-40b0-aa40-0f5b413288ef.png)

- A **chef** process randomly selects two out of three ingredients
  (tomato, onion, pepper).
- Each **saladmaker** owns exactly one ingredient and waits for the other
  two to become available on the shared table.
- When a saladmaker has all required ingredients, it prepares a salad,
  which takes a random amount of time.
- Once ready, the salad is delivered, and the process repeats.

Only one saladmaker can proceed at a time, depending on the ingredients
selected by the chef.

## Architecture

- All processes communicate via a **shared memory segment**
- Shared data structures are protected using **POSIX semaphores**
- No network communication or files are used
- Synchronization ensures:
  - correct cooperation between processes
  - absence of race conditions
  - proper blocking and wake-up behavior

## Goals

- Demonstrate correct use of **POSIX shared memory**
- Coordinate independent processes using **semaphores**
- Ensure safe concurrent access to shared state
- Solve a classic synchronization problem correctly

## Compilation & Execution

### Start the Chef
 `./chef -n <numOfSalads> -m <restTime>`

  numOfSalads: number of salads to prepare
  restTime: chef resting time between selections

- Chef prints the id of the shared segment.

### Start a saladmaker
`./saladmaker -t1 <lb> -t2 <ub> -i <ingredient> -s <shmid>`  

  `lb`, `ub` minimum and maximum preparation time 
  
  `ingredient`:
  - `o` for onion
  - `p` for pepper
  - `t` for tomato

  `shmid` is the key for the shared memory segment
  
  Example: ```./saladmaker -t1 1 -t2 3 -i o -s 12345```
