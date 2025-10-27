# A Beginner's Guide to High Performance Computing

*Having examined the foundational tools, concepts, and applications surrounding high performance computing, we can now turn our focus to the underlying key characteristics of HPC systems.*

---

## Inside the Hardware

To understand performance, it helps to know what's happening under the hood. Performance depends on several hardware layers that contribute to a system's computational efficiency.
- CPU Architecture: How many cores and threads does each processor have?
- Cache and Memory Hierarchy: How quickly can data be accessed or reused?
- Interconnects: How fast is the communication speed between nodes?
- Parallel File Systems: Is there shared storage capable of handling many users reading and writing data simultaneously?

## Job Schedulers

At the heart of every HPC environment is the job scheduler. Since an HPC system might have thousands of compute nodes and users running tasks simultaneously, a scheduler ensures that resources are allocated efficiently and fairly. Job schedulers such as [Slurm](https://slurm.schedmd.com/), [PBS](https://en.wikipedia.org/wiki/Portable_Batch_System), or [LSF](https://www.ibm.com/docs/en/spectrum-lsf/10.1.0?topic=lsf-session-scheduler) manage this process by queuing, prioritizing, and distributing workloads across available nodes, maximizing system utilization and minimizing idle time.

## Parallel Computing

Another defining feature of HPC is parallel computing, which allows many processors to work on different parts of a problem at the same time. Rather than a single processor completing tasks sequentially, hundreds or even thoasands of processors collaborate to solve complex problems faster. To make this coordination possible, developers rely on programming models such as [MPI (Message Passing Interface)](https://mpitutorial.com/) for distributed systems, [OpenMP](https://hpc-tutorials.llnl.gov/openmp/) for shared memory processing, and [CUDA](https://en.wikipedia.org/wiki/CUDA) for GPU acceleration.

## Data and Storage

In HPC, data management is just as critical as computation. Large scale scientific simulations and analyses can generate terabytes or even petabytes of data. Parallel file systems like [Lustre](https://www.lustre.org/) or [GPFS](https://en.wikipedia.org/wiki/GPFS) distribute data across multiple servers, allowing many users to read and write simultaneously. This design supports high throughput workflows and ensures that the data pipeline does not become a performance bottleneck.

## Resources
- [Intro to HPC: Scheduling Jobs](https://epcced.github.io/hpc-intro/13-scheduler/index.html): Overview and excercises to become more acquainted with job schedulers.
- [Program Parallel Computers](https://ppc.cs.aalto.fi/): Lecture notes and exercises from the Aalto University course CS-E4580 Programming Parallel Computers.
- [The Art of HPC](https://theartofhpc.com/): Conceptual and performance oriented overview of how systems work and interact.
- [RookieHPC](https://rookiehpc.org/): A website seeking to make HPC easier to learn.
- [HPC Beginner Learning Materials](https://www.reddit.com/r/HPC/comments/1odm910/hpc_beginner_learning_materials/): A reddit thread sharing beginner oriented HPC resources.
