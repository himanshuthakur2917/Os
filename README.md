# OS Lab – Question & Answer Bank (Experiments 1–16)

---

## EXPERIMENT 1 — MS-DOS Internal & External Commands

### Basic Concept Questions

**Q1. What is MS-DOS?**
**A:** MS-DOS stands for **Microsoft Disk Operating System**. It is a text-based operating system where you type commands to do tasks instead of clicking icons. Microsoft introduced it in 1981. Even today, Windows has a similar tool called the **Command Prompt (cmd)**.

---

**Q2. How do you open the Command Prompt in Windows?**
**A:** Click the **Start button**, type `cmd`, and press Enter. A black window opens showing something like `C:\>`. This is called the **command prompt**.

---

**Q3. What is the difference between Internal and External Commands?**
**A:**
| Feature | Internal Commands | External Commands |
|---|---|---|
| Stored in | System memory (RAM) during boot | Stored as separate files on disk |
| Can be seen/deleted? | No (they are hidden in memory) | Yes (they exist as `.exe` files) |
| Examples | DATE, TIME, DIR, COPY, DEL, MD | FORMAT, TREE, ATTRIB, CHKDSK |

> Simply put: Internal commands are **built-in** to the OS. External commands are **separate programs**.

---

**Q4. What does the `DATE` command do?**
**A:** It shows or changes the current date of the computer.
- `DATE /t` → just shows the date
- `DATE` → shows the date and asks you to enter a new one

---

**Q5. What does the `MKDIR` or `MD` command do?**
**A:** It **creates a new folder (directory)**.
- `MD Tutorial` → creates a folder named "Tutorial" in the current location
- `MD D:\Folder1\Folder2` → creates nested folders on D drive

---

**Q6. What is the purpose of the `CD` command?**
**A:** `CD` stands for **Change Directory**. It moves you into a different folder.
- `CD tutorial` → goes inside the "tutorial" folder
- `CD..` → goes one folder back (like pressing Back)
- `CD\` → goes all the way back to the root drive (like `D:\`)

---

**Q7. What does `COPY CON` do?**
**A:** It creates a **new text file** directly from the keyboard. You type the content, then press `Ctrl+Z` (or F6) to save it.
- Example: `COPY CON myfile.txt` → then type text → press Ctrl+Z to save

---

**Q8. What does the `TYPE` command do?**
**A:** It **displays the content** of a text file on screen.
- Example: `TYPE myfile.txt` → shows what is written in myfile.txt

---

**Q9. What is the `DIR` command used for?**
**A:** It **lists all files and folders** inside the current directory (like File Explorer, but in text).

---

**Q10. What does the `DEL` command do?**
**A:** It **deletes one or more files**.
- `DEL myfile.txt` → deletes that specific file
- `DEL *.jpg` → deletes all jpg image files

---

**Q11. What is the `RENAME` command?**
**A:** It **changes the name** of a file.
- `RENAME abc.txt bd.txt` → renames abc.txt to bd.txt

---

**Q12. What does the `RMDIR` or `RD` command do?**
**A:** It **deletes (removes) an empty folder**.
- `RMDIR c:\test` → removes the folder named "test" from C drive

---

**Q13. What does the `COPY` command do?**
**A:** It **copies a file** to another location or with a new name.
- `COPY abc.txt mnp.txt` → makes a copy of abc.txt named mnp.txt

---

**Q14. What is the `FORMAT` command (External)?**
**A:** It **prepares a disk** for use by creating a new file system on it. Warning: It erases all data on that disk.

---

**Q15. What does `ATTRIB` do (External)?**
**A:** It sets or shows file **attributes** like:
- `+H` → Hide a file
- `+R` → Make it Read-only
- `+A` → Archive attribute

---

**Q16. What is `CHKDSK` used for?**
**A:** It **checks the hard disk for errors** and tells you if any files are damaged or the disk has bad sectors.

---

**Q17. What does the `TREE` command do?**
**A:** It shows all **folders and sub-folders** in a graphical tree structure from the given drive.

---

**Q18. What is `DELTREE`?**
**A:** It **deletes a folder along with all files and sub-folders** inside it (more powerful than `RMDIR` which only deletes empty folders).

---

## EXPERIMENT 2 — FCFS CPU Scheduling

### Basic Concept Questions

**Q1. What is CPU Scheduling?**
**A:** The CPU can run only one process at a time. **CPU Scheduling** decides which process gets to use the CPU next, and in what order. The goal is to keep the CPU busy and complete processes efficiently.

---

**Q2. What is FCFS Scheduling?**
**A:** **FCFS = First Come, First Served.** The process that arrives first gets the CPU first — just like a queue at a shop. No process can cut in line.

---

**Q3. What is Burst Time?**
**A:** **Burst Time** is the total time a process needs the CPU to complete its work. For example, if Process P1 needs 24 ms of CPU, its burst time = 24.

---

**Q4. What is Waiting Time?**
**A:** **Waiting Time** is the total time a process spends waiting in the ready queue before it gets the CPU.
- **Formula:** `Waiting Time(n) = Waiting Time(n-1) + Burst Time(n-1)`
- The first process always has Waiting Time = 0 (no one is before it).

---

**Q5. What is Turnaround Time?**
**A:** **Turnaround Time** is the total time from when a process arrives to when it finishes.
- **Formula:** `Turnaround Time = Waiting Time + Burst Time`

---

**Q6. Explain the FCFS example from the program: P0=24, P1=3, P2=3.**

| Process | Burst Time | Waiting Time | Turnaround Time |
|---|---|---|---|
| P0 | 24 | 0 | 24 |
| P1 | 3 | 24 | 27 |
| P2 | 3 | 27 | 30 |

- Average Waiting Time = (0 + 24 + 27) / 3 = **17**
- Average Turnaround Time = (24 + 27 + 30) / 3 = **27**

---

**Q7. What is the main problem with FCFS?**
**A:** If a long process comes first, all short processes have to wait a long time. This is called the **Convoy Effect**. For example, P0 has burst time 24, so P1 and P2 have to wait unnecessarily.

---

**Q8. What does `wt[0] = 0` mean in the code?**
**A:** The first process in FCFS does not wait at all — it gets the CPU immediately. So its waiting time is set to 0.

---

**Q9. How is average waiting time calculated in the code?**
**A:** The code adds up all waiting times (`wtavg`) and at the end divides by the number of processes (`n`): `wtavg / n`.

---

**Q10. What are the arrays used in the FCFS program and what do they store?**
**A:**
- `bt[20]` → stores Burst Time of each process
- `wt[20]` → stores Waiting Time of each process
- `tat[20]` → stores Turnaround Time of each process
- `wtavg`, `tatavg` → store running totals to compute averages

---

**Q11. Is FCFS preemptive or non-preemptive?**
**A:** FCFS is **non-preemptive**. Once a process starts running, it runs until it finishes. No one can take the CPU away from it in between.

---

## EXPERIMENT 3 — SJF Scheduling (Non-Preemptive)

### Basic Concept Questions

**Q1. What is SJF Scheduling?**
**A:** **SJF = Shortest Job First.** The process with the **smallest burst time** gets the CPU next. It's like serving the customer who needs the least time first.

---

**Q2. Why is SJF better than FCFS?**
**A:** SJF gives the **minimum average waiting time** among all non-preemptive algorithms. Short processes don't have to wait behind long ones.

---

**Q3. What is Non-Preemptive SJF?**
**A:** Once a process starts running, it **cannot be stopped** in the middle, even if a shorter process arrives. The scheduler only picks the shortest job when the CPU is free.

---

**Q4. How does the program sort processes in SJF?**
**A:** The program uses a **bubble sort** to arrange processes in ascending order of burst time. The process with the smallest burst time moves to the front.

---

**Q5. Explain the SJF example: P0=6, P1=8, P2=7, P3=3**

After sorting by burst time:
| Process | Burst Time | Waiting Time | Turnaround Time |
|---|---|---|---|
| P3 | 3 | 0 | 3 |
| P0 | 6 | 3 | 9 |
| P2 | 7 | 9 | 16 |
| P1 | 8 | 16 | 24 |

- Average Waiting Time = (0+3+9+16)/4 = **7**
- Average Turnaround Time = (3+9+16+24)/4 = **13**

---

**Q6. What is the role of the `temp` variable in the sorting part of the code?**
**A:** `temp` is a **temporary holder** used during swapping. When two values are swapped, one must be saved temporarily so it's not lost:
```
temp = bt[i]; bt[i] = bt[k]; bt[k] = temp;
```
This is classic swap logic.

---

**Q7. What is the `p[]` array used for in the SJF code?**
**A:** The `p[]` array stores the **original process IDs**. When burst times are sorted and swapped, process IDs are also swapped so we know which ID belongs to which burst time after sorting.

---

**Q8. What is the disadvantage of SJF?**
**A:** The biggest problem is **Starvation** — long processes may never get CPU time if short ones keep arriving. Also, in real systems, we don't always know the burst time in advance.

---

**Q9. What is the difference between FCFS and SJF waiting time in the example above?**
**A:** In FCFS order (P0,P1,P2,P3 with burst 6,8,7,3), average waiting would be higher. SJF reorders to P3,P0,P2,P1 giving average waiting time of just **7**, which is better.

---

**Q10. In the SJF code, why is `wt[0] = 0`?**
**A:** After sorting, the shortest job is at index 0. It runs first, so it has **no waiting time** — hence `wt[0] = 0`.

---

## EXPERIMENT 4 — Priority Scheduling

### Basic Concept Questions

**Q1. What is Priority Scheduling?**
**A:** In Priority Scheduling, each process is assigned a **priority number**. The process with the **highest priority** runs first. Processes are sorted by priority before execution.

---

**Q2. What does "higher priority number = higher priority" mean?**
**A:** It depends on the system definition. In most systems, **lower number = higher priority** (e.g., priority 1 runs before priority 5). The sorting determines which gets CPU first.

---

**Q3. How is waiting time calculated in Priority Scheduling?**
**A:** Same as other algorithms:
`Waiting Time(n) = Waiting Time(n-1) + Burst Time(n-1)`
But processes are **sorted by priority first** before calculating.

---

**Q4. What is the difference between Priority Scheduling and SJF?**
**A:** In SJF, processes are sorted by **burst time** (shortest first). In Priority Scheduling, processes are sorted by their **priority number**. Priority can be based on anything (memory needs, process type, deadline, etc.).

---

**Q5. What is the problem with Priority Scheduling?**
**A:** **Starvation** — Low priority processes may wait forever if high priority ones keep arriving. The solution is **Aging** (gradually increase priority of waiting processes).

---

**Q6. What is Aging in Priority Scheduling?**
**A:** Aging means **slowly increasing the priority of processes that have been waiting for a long time**, so they eventually get the CPU. This prevents starvation.

---

**Q7. Is Priority Scheduling preemptive or non-preemptive?**
**A:** It can be **both**:
- **Non-preemptive**: Once started, a process runs to completion.
- **Preemptive**: If a higher-priority process arrives, the current one is paused.

---

**Q8. What are `bu[]` and `ct[]` arrays in the code?**
**A:**
- `bu[]` → stores **current remaining burst time** (gets decremented)
- `ct[]` → stores the **original burst time** (kept for final output display)

---

## EXPERIMENT 5 — Round Robin Scheduling

### Basic Concept Questions

**Q1. What is Round Robin Scheduling?**
**A:** In Round Robin, every process gets the CPU for a **fixed time** called the **Time Quantum (or Time Slice)**. After the time is up, it moves to the back of the queue and the next process runs. This continues in a circular manner.

---

**Q2. What is a Time Quantum?**
**A:** Time Quantum is the **maximum time** a process is allowed to run in one turn. For example, if time quantum = 3ms, no process can run for more than 3ms at a time without being paused.

---

**Q3. How does Round Robin handle a process that finishes before the time quantum ends?**
**A:** If a process completes before its time quantum runs out, the CPU is **immediately given to the next process** without waiting for the quantum to expire.

---

**Q4. Explain the Round Robin example: P1=24, P2=3, P3=3, Time Quantum=3**

| Process | Burst Time | Waiting Time | Turnaround Time |
|---|---|---|---|
| P1 | 24 | 6 | 30 |
| P2 | 3 | 4 | 7 |
| P3 | 3 | 7 | 10 |

- Average Turnaround Time = (30+7+10)/3 = **15.67**
- Average Waiting Time = (6+4+7)/3 = **5.67**

---

**Q5. What is the logic behind `Waiting Time = Turnaround Time - Burst Time` in the code?**
**A:** The code calculates turnaround time first (when each process finishes). Then:
`Waiting Time = Turnaround Time - Original Burst Time`
This is simpler than tracking each wait step in Round Robin.

---

**Q6. What does `bu[i] = bu[i] - t` do in the code?**
**A:** When a process gets the CPU for one time slice but isn't finished, we subtract the time quantum from its remaining burst time:
`Remaining Burst = Current Burst - Time Quantum`
This tracks how much time the process still needs.

---

**Q7. What happens if `bu[i] <= t` in the code?**
**A:** If the remaining burst time is **less than or equal to the time slice**, the process finishes in this turn. Its turnaround time is recorded and `bu[i]` is set to 0 (done).

---

**Q8. What is the advantage of Round Robin?**
**A:** Round Robin is **fair** — every process gets equal CPU time. It is widely used in time-sharing systems (like when multiple people use the same computer).

---

**Q9. What is the effect of choosing a very large time quantum?**
**A:** If the time quantum is very large, Round Robin behaves like **FCFS** — each process runs to completion before the next one starts.

---

**Q10. What is the effect of choosing a very small time quantum?**
**A:** If the time quantum is very small, **context switching** (switching between processes) becomes too frequent and wastes CPU time.

---

**Q11. What is Context Switching?**
**A:** When the CPU switches from one process to another, it must **save the current process state and load the new one**. This is called a context switch. It takes time and adds overhead.

---

## EXPERIMENT 6 — Banker's Algorithm (Deadlock Avoidance)

### Basic Concept Questions

**Q1. What is a Deadlock?**
**A:** A **deadlock** is a situation where two or more processes are waiting for each other to release resources, but none of them ever does. They are stuck forever — like two cars facing each other on a narrow road, each waiting for the other to back up.

---

**Q2. What is the Banker's Algorithm?**
**A:** The **Banker's Algorithm** is used to **avoid deadlocks**. Before giving a resource to a process, the OS checks whether doing so will keep the system in a **safe state**. If yes, resources are given; if no, the process must wait.
It is named after a bank that checks if giving out a loan will leave it able to handle future withdrawals.

---

**Q3. What is a Safe State?**
**A:** A system is in a **safe state** if there exists at least one order (safe sequence) in which all processes can finish without any deadlock. If no such order exists, the system is in an **unsafe state**.

---

**Q4. What are the key data structures in the Banker's Algorithm?**
**A:**
- **Available[j]** → Number of available instances of resource type Rj
- **Max[i][j]** → Maximum instances process Pi can ever need of resource Rj
- **Allocation[i][j]** → Currently allocated instances of resource Rj to process Pi
- **Need[i][j]** → How many more instances process Pi may still need = Max[i][j] − Allocation[i][j]

---

**Q5. What is the Safety Algorithm?**
**A:** The safety algorithm checks if the system is in a safe state:
1. Start with `Work = Available` and `Finish[i] = False` for all processes
2. Find a process where `Finish[i] = False` AND `Need[i] <= Work`
3. If found: add its allocation back (`Work = Work + Allocation[i]`), set `Finish[i] = True`
4. Repeat until all processes finish (safe) or no process can proceed (unsafe)

---

**Q6. What does `Need[i][j] = Max[i][j] - Allocation[i][j]` mean?**
**A:** It means: if a process may need at most 6 units of a resource and it already has 2 allocated, then it may still **need** 6 − 2 = **4 more**.

---

**Q7. What is the safe sequence in the output of Experiment 6?**
**A:** The program finds: Process 2 → Process 3 → Process 4 → Process 1. All processes can be completed in this order, so the system is in a **safe state**.

---

**Q8. What is the `finish[]` array used for in the code?**
**A:** `finish[i]` tracks whether process `i` has been "executed" (finished) during the safety check. It starts as `'n'` (not done) and is changed to `'y'` (done) once the process can complete.

---

**Q9. What does `goto A` do in the code?**
**A:** After each process finishes, the code jumps back to the beginning (label `A`) to check remaining processes again. This repeats until all processes are done (count == n).

---

**Q10. What does "count != n" check in the code?**
**A:** If `count` (number of processes that could finish) is not equal to `n` (total processes), it means not all processes could be executed — the algorithm loops again to try. When `count == n`, all processes finished = safe state.

---

## EXPERIMENT 7 — Banker's Algorithm (Deadlock Prevention)

### Basic Concept Questions

**Q1. What is the difference between Deadlock Avoidance and Deadlock Prevention?**
**A:**
- **Avoidance** (Exp 6): Dynamically checks at runtime if granting a resource keeps the system safe. (Banker's Algorithm)
- **Prevention** (Exp 7): Breaks one of the necessary conditions for deadlock to happen in the first place (like resource ordering or pre-allocation)

---

**Q2. What are the 4 necessary conditions for a Deadlock?**
**A:** All four must be true simultaneously for deadlock to occur:
1. **Mutual Exclusion** – Only one process can use a resource at a time
2. **Hold and Wait** – A process holds one resource and waits for another
3. **No Preemption** – Resources cannot be forcibly taken from a process
4. **Circular Wait** – A cycle of processes, each waiting for the next

Prevention eliminates at least one of these conditions.

---

**Q3. What does Experiment 7's code do?**
**A:** It sorts processes by their required time (shortest first) and checks if each one can be accommodated with available resources. It finds a **safe sequence** — the order in which jobs can run.

---

**Q4. What is a Safe Sequence?**
**A:** A safe sequence is an **ordered list of processes** such that each process can get its required resources, finish, and release resources that the next process in line can use.

---

**Q5. In the output of Experiment 7, what is the safe sequence?**
**A:** With jobs A=1, B=4, C=2, D=3 and available resources=20:
**Safe Sequence: A → C → D → B**
Each job finishes and releases resources before the next one needs them.

---

**Q6. How does the program sort jobs in Experiment 7?**
**A:** It sorts jobs by their **time requirement in ascending order** (smallest first) using a bubble sort, similar to SJF scheduling.

---

## EXPERIMENT 8 — FIFO Page Replacement

### Basic Concept Questions

**Q1. What is a Page Fault?**
**A:** When a program needs a page that is **not currently in memory (RAM)**, the OS must load it from disk. This event is called a **page fault**. Fewer page faults = better performance.

---

**Q2. What is Page Replacement?**
**A:** When memory (RAM) is full and a new page must be loaded, the OS must **remove (replace) an existing page** to make room. The algorithm that decides which page to remove is called a page replacement algorithm.

---

**Q3. What is FIFO Page Replacement?**
**A:** **FIFO = First In, First Out.** The page that was loaded into memory **the earliest** is replaced first — like a queue where the first person to enter is the first to leave.

---

**Q4. What are Frames?**
**A:** **Frames** are the fixed slots in RAM that hold pages. For example, 3 frames means only 3 pages can be in memory at any time.

---

**Q5. Explain FIFO with the reference string: 2,3,2,1,5,2,4,5,3,2,5,2 with 3 frames.**

Step by step (page fault = PF):
| Page | Frames | Page Fault? |
|---|---|---|
| 2 | 2,-1,-1 | Yes (PF) |
| 3 | 2,3,-1 | Yes (PF) |
| 2 | 2,3,-1 | No (hit) |
| 1 | 2,3,1 | Yes (PF) |
| 5 | 5,3,1 | Yes (PF) – replaces 2 |
| 2 | 5,2,1 | Yes (PF) – replaces 3 |
| 4 | 5,2,4 | Yes (PF) – replaces 1 |
| 5 | 5,2,4 | No (hit) |
| 3 | 3,2,4 | Yes (PF) – replaces 5 |
| 2 | 3,2,4 | No (hit) |
| 5 | 3,5,4 | Yes (PF) – replaces 2 |
| 2 | 3,5,2 | Yes (PF) – replaces 4 |

**Total Page Faults = 6** (but the code outputs 6 as well – this matches)

---

**Q6. What is the `top` variable in the FIFO code?**
**A:** `top` is a **circular pointer** that points to which frame slot gets replaced next. It starts at 0, and after each replacement it increments. When it reaches `frsize` (3), it resets to 0 — making it circular (FIFO order).

---

**Q7. What does `flag1` and `flag2` track in the FIFO code?**
**A:**
- `flag1` → tracks whether the page is **already in memory** (page hit)
- `flag2` → tracks whether the page was placed in an **empty frame**
If both are 0, it means the frame is full and we must replace → page fault counted.

---

**Q8. What is Belady's Anomaly?**
**A:** **Belady's Anomaly** is a strange behavior in FIFO where **increasing the number of frames sometimes increases page faults**. This does not happen in LRU or Optimal algorithms.

---

## EXPERIMENT 9 — LRU Page Replacement

### Basic Concept Questions

**Q1. What is LRU Page Replacement?**
**A:** **LRU = Least Recently Used.** The page that **has not been used for the longest time** is replaced first. The idea is: if a page hasn't been used recently, it probably won't be needed soon.

---

**Q2. How does LRU differ from FIFO?**
**A:** FIFO removes the **oldest loaded page**, regardless of when it was last used. LRU removes the **page not used for the longest time** — this is more intelligent and usually gives fewer page faults.

---

**Q3. Explain LRU with reference string: 2,3,2,1,5,2,4,5,3,2,5,2 with 3 frames**

LRU Output:
| Step | Page | Frames | PF? |
|---|---|---|---|
| 1 | 2 | 2,-1,-1 | Yes |
| 2 | 3 | 2,3,-1 | Yes |
| 3 | 2 | 2,3,-1 | No |
| 4 | 1 | 2,3,1 | Yes |
| 5 | 5 | 2,5,1 | Yes (replaces 3 – LRU) |
| 6 | 2 | 2,5,1 | No |
| 7 | 4 | 2,5,4 | Yes (replaces 1 – LRU) |
| 8 | 5 | 2,5,4 | No |
| 9 | 3 | 3,5,4 | Yes (replaces 2 – LRU) |
| 10 | 2 | 3,5,2 | Yes (replaces 4 – LRU) |
| 11 | 5 | 3,5,2 | No |
| 12 | 2 | 3,5,2 | No |

**Total Page Faults = 4** ✓ (better than FIFO's 6!)

---

**Q4. What does the `fs[]` array do in the LRU code?**
**A:** `fs[]` (frame status) marks which frames were recently used. The program looks **backward** in the reference string to find which page in the current frames was used **least recently** — that one gets replaced.

---

**Q5. Why does LRU generally perform better than FIFO?**
**A:** LRU considers **actual usage history**, not just arrival order. A page that was used recently is more likely to be needed again soon (locality of reference). FIFO ignores this.

---

**Q6. What is Locality of Reference?**
**A:** Programs tend to **access the same pages repeatedly** in a short time. LRU takes advantage of this — frequently used pages stay in memory.

---

## EXPERIMENT 10 — Optimal Page Replacement

### Basic Concept Questions

**Q1. What is the Optimal Page Replacement Algorithm?**
**A:** The Optimal algorithm replaces the page that **will not be used for the longest time in the future**. It gives the **minimum number of page faults** possible.
It is also called OPT or Bélády's Algorithm.

---

**Q2. Is the Optimal Algorithm practically used?**
**A:** **No.** It requires knowing the **future** reference string in advance, which is impossible in real operating systems. It is used only as a **benchmark** to compare how well other algorithms perform.

---

**Q3. What does `count[cnt]` track in the Optimal code?**
**A:** For each page in a frame, `count[cnt]` counts **how many steps in the future** until that page is used again. The page with the **highest count** (farthest future use) is replaced.

---

**Q4. Optimal example with reference string 1,2,3,4,1,2,5,1,2,3,4,5 and 3 frames gives how many faults?**
**A:** **7 page faults** as shown in the output. Even this "best possible" algorithm still has 7 faults for this sequence with 3 frames.

---

**Q5. Compare FIFO, LRU, and Optimal for the same reference string?**
**A:** Generally: **Optimal ≤ LRU ≤ FIFO** in terms of page faults. Optimal always gives the least, Optimal is theoretical, LRU is practical and close to optimal.

---

## EXPERIMENT 11 — FCFS Disk Scheduling

### Basic Concept Questions

**Q1. What is Disk Scheduling?**
**A:** The disk head must move to different **tracks (cylinders)** to read/write data. Multiple requests may be waiting. **Disk Scheduling** decides the order in which these requests are served to minimize the total head movement (seek time).

---

**Q2. What is Seek Time?**
**A:** **Seek Time** is the time taken by the disk head to move from its current position to the requested track. Less movement = less seek time = faster disk access.

---

**Q3. What is FCFS Disk Scheduling?**
**A:** Requests are served in the **order they arrive**, no matter how far apart the tracks are. It is fair but can result in a lot of unnecessary head movement.

---

**Q4. Explain the FCFS example: Initial head = 50, Queue = 90, 120, 35, 122, 38, 128, 65, 68**

| Move | From → To | Distance |
|---|---|---|
| 1 | 50 → 90 | 40 |
| 2 | 90 → 120 | 30 |
| 3 | 120 → 35 | 85 |
| 4 | 35 → 122 | 87 |
| 5 | 122 → 38 | 84 |
| 6 | 38 → 128 | 90 |
| 7 | 128 → 65 | 63 |
| 8 | 65 → 68 | 3 |
| **Total** | | **482** |

**Average Seek Time = 482 / 8 = 60.25**

---

**Q5. What does `abs(queue[j+1] - queue[j])` calculate?**
**A:** It calculates the **absolute distance** between two consecutive track positions. We use `abs()` because distance is always positive, whether moving left or right.

---

**Q6. What is the main disadvantage of FCFS disk scheduling?**
**A:** It can cause the disk head to **jump back and forth** unnecessarily (like in the example: 120 → 35 → 122 — it goes all the way back just to come back again). This wastes time.

---

## EXPERIMENT 12 — SSTF Disk Scheduling

### Basic Concept Questions

**Q1. What is SSTF Disk Scheduling?**
**A:** **SSTF = Shortest Seek Time First.** The disk head moves to the **nearest pending request** next, not the one that arrived first. This reduces total head movement compared to FCFS.

---

**Q2. How is SSTF better than FCFS?**
**A:** SSTF picks the **closest track** to service next, so the head doesn't jump all over the disk. This reduces total seek time significantly.

---

**Q3. What is the disadvantage of SSTF?**
**A:** **Starvation.** If requests keep arriving near the current head position, far-away requests may never get served. This is unfair.

---

**Q4. Explain the SSTF example: Queue = 10,17,2,15,4, Head = 3**

Distance from head (3): |10-3|=7, |17-3|=14, |2-3|=1, |15-3|=12, |4-3|=1

After sorting by distance: 2(dist 1), 4(dist 1), 10(dist 7), 15(dist 12), 17(dist 14)

**Total Seek Time = 14, Average = 2.8**

---

**Q5. What does `t[i] = abs(head - queue[i])` compute in the SSTF code?**
**A:** It computes the **distance of each track from the current head position**. The track with the smallest distance is served next.

---

**Q6. Compare FCFS vs SSTF in terms of total seek time.**
**A:** SSTF almost always has **less total seek time** than FCFS. But SSTF can cause starvation. FCFS is fair but slow. Neither is ideal for all cases.

---

## EXPERIMENT 13 — Shell Script: Display Lines Between Line Numbers

### Basic Concept Questions

**Q1. What is a Shell Script?**
**A:** A **shell script** is a text file containing a series of Linux/Unix commands that run automatically when the script is executed. It is like a batch file in Windows.

---

**Q2. What is the `cat` command used for in the shell?**
**A:**
- `cat > filename` → creates a new file (type content, press Ctrl+D to save)
- `cat filename` → displays the contents of a file

---

**Q3. What is the `sed` command?**
**A:** `sed` stands for **Stream Editor**. It processes text from a file line by line. It can search, replace, delete, or extract specific lines.

---

**Q4. What does the command `sed -n $s,$n\p $fname` do?**
**A:** It **prints lines from line number `$s` to line number `$n`** in the file `$fname`.
- `-n` → suppress default output (only print what we tell it to)
- `$s,$n\p` → print from line `$s` to line `$n`

---

**Q5. What are the variables `fname`, `s`, and `n` in the script?**
**A:**
- `fname` → name of the file entered by the user
- `s` → starting line number
- `n` → ending line number
These are read from the user using `read` command.

---

**Q6. What does `read` do in a shell script?**
**A:** `read` takes **input from the user** and stores it in a variable. For example, `read fname` waits for the user to type a filename and stores it.

---

## EXPERIMENT 14 — Shell Script: Delete Lines Containing a Word

### Basic Concept Questions

**Q1. What does this shell script do?**
**A:** It deletes all lines in one or more files that **contain a specified word**. This is done using `sed` with the delete command.

---

**Q2. What does `/os/d` mean in the sed script?**
**A:** It means: **find every line that contains the word "os" and delete it (`d`)**.
- `/os/` → matches lines containing "os"
- `d` → delete those lines

---

**Q3. What is a sed script file?**
**A:** A sed script file contains sed commands in a separate file. It is run using `sed -f scriptfile inputfile`. This is useful when the sed command is long.

---

**Q4. What is the `vi` editor used for in the experiment?**
**A:** `vi` is a **text editor** in Linux used to create and edit files. `vi filename` opens the file for editing.

---

**Q5. Can `sed` modify the original file directly?**
**A:** By default, `sed` only prints modified output on screen. To save changes back to the file, you use the `-i` flag: `sed -i '/word/d' filename`

---

## EXPERIMENT 15 — Paging Technique for Memory Management

### Basic Concept Questions

**Q1. What is Paging?**
**A:** **Paging** is a memory management technique where:
- **Physical memory (RAM)** is divided into fixed-size blocks called **frames**
- **Logical memory (process memory)** is divided into equal-size blocks called **pages**
- Each page is mapped to a frame using a **page table**

This avoids fragmentation and allows non-contiguous memory allocation.

---

**Q2. What is a Page Table?**
**A:** A **page table** is a mapping that tells the OS: "Page number X of this process is stored in Frame number Y of RAM." It translates logical addresses to physical addresses.

---

**Q3. What is the formula to convert a Logical Address to a Physical Address?**
**A:**
`Physical Address = (Frame Number × Page Size) + Offset`
- `Frame Number` = found in the page table using the page number
- `Offset` = position within the page

---

**Q4. In the program example: Memory=1000, Page size=100, Process 2 accesses page 3, offset 60. What is the physical address?**
**A:**
- Number of frames = 1000/100 = **10**
- Page table of P2: frame numbers are 1, 4, 5, 7, 3
- Page 3 of P2 → Frame 7 (index 3 in the page table)
- Physical Address = 7 × 100 + 60 = **760** ✓

---

**Q5. What does `nop = ms/ps` calculate in the code?**
**A:** `nop` = number of pages = **total memory size ÷ page size**.
Example: 1000 / 100 = 10 pages available in memory.

---

**Q6. What is `rempages` used for?**
**A:** `rempages` tracks **how many frames are still free**. As each process is allocated pages, `rempages` decreases. If a process needs more pages than available, "Memory is Full" is printed.

---

**Q7. What is the difference between a Page and a Frame?**
**A:**
- **Page** → a block of the **process's logical memory**
- **Frame** → a block of **physical RAM** where a page is stored
They are the **same size**, but pages exist in the process's view and frames exist in hardware RAM.

---

**Q8. What is External Fragmentation and does Paging solve it?**
**A:** External fragmentation is wasted space **between** allocated memory blocks. **Paging eliminates external fragmentation** because frames can be anywhere in RAM — they don't need to be contiguous.

---

**Q9. What is Internal Fragmentation? Does Paging cause it?**
**A:** Internal fragmentation is wasted space **inside** an allocated page when the process doesn't fill the entire page. **Paging can cause internal fragmentation** in the last page if the process size isn't a perfect multiple of the page size.

---

## EXPERIMENT 16 — Contiguous File Allocation

### Basic Concept Questions

**Q1. What is Contiguous File Allocation?**
**A:** In **contiguous allocation**, a file is stored in a **sequence of consecutive disk blocks**. The OS just needs to know the **starting block** and the **length** (number of blocks) of each file.

---

**Q2. What does the array `f[50]` represent in the code?**
**A:** `f[50]` is an array of 50 disk blocks. `f[i] = 0` means block `i` is **free**. `f[i] = 1` means block `i` is **occupied** by a file.

---

**Q3. In the example: starting block = 14, length = 3. What happens?**
**A:** Blocks 14, 15, and 16 are checked. Since they are free (f[i]=0), they are allocated (f[i]=1) and displayed:
```
14  1
15  1
16  1
File is allocated to disk
```

---

**Q4. Why is the file NOT allocated when starting block = 14, length = 1 is requested again?**
**A:** Block 14 is already allocated (`f[14] = 1`). Since the required block is not free, the file **cannot be allocated** and "The file is not allocated" is printed.

---

**Q5. What is the advantage of Contiguous Allocation?**
**A:**
- **Simple** – only start block and length needed
- **Fast** – disk head doesn't need to jump around; blocks are next to each other
- Supports both **sequential** and **direct (random) access**

---

**Q6. What are the disadvantages of Contiguous Allocation?**
**A:**
- **External Fragmentation** – over time, free space becomes scattered in small pieces that can't be used for large files
- **File size must be known in advance** – if a file grows, it may not fit in its current location
- Finding a contiguous free space of the right size is hard (**allocation problem**)

---

**Q7. What does the `count` variable check in the code?**
**A:** `count` counts how many blocks in the requested range are **free**. If `count == length`, all needed blocks are free and the file can be allocated. If `count < length`, some blocks are occupied, so allocation fails.

---

**Q8. What does the `goto x` statement do in the code?**
**A:** It asks the user if they want to allocate another file. If yes (input = 1), it **jumps back to label `x`** and repeats the allocation process for a new file.

---

# 🔁 Quick Revision Summary Table

| Exp | Topic | Key Concept | Key Formula |
|---|---|---|---|
| 1 | MS-DOS Commands | Internal vs External commands | — |
| 2 | FCFS Scheduling | First come first served | WT(n) = WT(n-1) + BT(n-1) |
| 3 | SJF Scheduling | Shortest burst runs first | Sort by BT, then WT formula |
| 4 | Priority Scheduling | Highest priority runs first | Sort by priority, then WT formula |
| 5 | Round Robin | Fixed time slice per process | WT = TAT - BT |
| 6 | Banker's (Avoidance) | Check safe state before allocation | Need = Max - Allocation |
| 7 | Banker's (Prevention) | Safe sequence, sort by need | — |
| 8 | FIFO Page Replace | Oldest page replaced first | Count page faults |
| 9 | LRU Page Replace | Least recently used replaced | Count page faults |
| 10 | Optimal Page Replace | Farthest future use replaced | Minimum possible faults |
| 11 | FCFS Disk Schedule | Serve in arrival order | Total seek = sum of distances |
| 12 | SSTF Disk Schedule | Serve nearest track first | Sort by distance |
| 13 | Shell Script (sed) | Print lines between numbers | `sed -n $s,$n\p` |
| 14 | Shell Script (sed) | Delete lines with a word | `/word/d` |
| 15 | Paging | Page table maps logical to physical | PA = Frame × PageSize + Offset |
| 16 | Contiguous Allocation | File in consecutive disk blocks | Check all blocks free |
