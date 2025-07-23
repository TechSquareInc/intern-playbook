# HPC Architecture

HPC architectures typically consist of a collection of interconencted computing resources configured to operate as a unified system. The architecture is designed to maximize performance, scalability, and reliability, enabling users to execute parallelized applications across thousands of processing cores. To support their design, HPC environments are organized into functional zones.

## Core Components of HPC Architecture

HPC environemnts are structured to support the execution of compute-intensive tasks at scale, and can be seperated into four key zones:

- **Access Zone:** Entry point for users and external systems.
- **Compute Zone:** Core computational processing resources. 
- **Data Storage Zone:** High performance and reliable data storage systems.
- **Managment Zone:** System coordination, orchestration, and observability. 

### Access Zone

The access zone serves as the primary interface between users and the HPC environment. It is responisble for authenticating users, facilitating secure remote access, and is used as the environment where users can submit and monitor jobs. It is composed of one or more nodes that allow users and administrators to access the system. At least one of these nodes will be the *login node* where users have access to shells to launch interactive or batch jobs. Some login nodes may also have specialized visualization hardware or software. There may also be one or more nodes allocated to data transfer which provides services to transfer data in or out of the HPC system and could also provide storage mounting services.

### Compute Zone

The compute zone consists of a pool of compute nodes connected by one of more high speed networks, and executes the computational workload submitted by users. Compute nodes generally have the same components of a laptop, desktop, or server, including CPUs, memory, disk space, and networking interface cards. However, they are architecturally tuned for the requirements of HPC workloads. In some HPC architecctures, a compute node may not have local disks and instead use data storage services or remote storage servers. Compute nodes may also be equipped with hardware accelorators to speede up specific applications. Compute nodes often utilize graphics processing units (GPUs) to accelerate modeiling and simulation or AI and machine learning model training.
