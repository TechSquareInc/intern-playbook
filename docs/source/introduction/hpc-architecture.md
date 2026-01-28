# HPC Architecture

HPC architectures typically consist of a collection of interconnected computing resources configured to operate as a unified system. The architecture is designed to maximize performance, scalability, and reliability, enabling users to execute parallelized applications across thousands of processing cores. To support their design, HPC environments are organized into functional zones.

## Core Components of HPC Architecture

HPC environments are structured to support the execution of compute-intensive tasks at scale, and can be separated into four key zones:

- **Access Zone:** Entry point for users and external systems
- **Compute Zone:** Core computational processing resources.
- **Data Storage Zone:** High performance and reliable data storage systems.
- **Management Zone:** System coordination, orchestration, and observability.

### Access Zone

The **access zone** serves as the primary interface between users and the HPC environment. It is responisble for authenticating users, facilitating secure remote access, and is used as the environment where users can submit and monitor jobs.

This zone is composed of one or more nodes that allow users and administrators to access the system. At least one of these nodes will be the **login node** where users have access to shells to launch interactive or batch jobs. Login nodes are where users access the cluster, login, edit files, view job results, and submit new jobs, but *are not* for running application workloads. Some login nodes may have specialized visualization hardware or software, and there may also be one or more nodes allocated to data transfer which provides services to transfer data in or out of the HPC system and could also provide storage mounting services.

### Compute Zone

The **compute zone** consists of a pool of compute nodes connected by one or more high speed networks, and executes the computational workload submitted by users. A **compute node** is a single system within a cluster that is used for computational taks. In essence, these nodes are the workhorses of a computing environment. They receive tasks, process data, and return results. Generally, computes nodes have the same components of a laptop, desktop, or server, including CPUs, memory, disk space, and network interface cards. However, they are architecturally tuned for the requirements of HPC workloads. In some HPC architectures, a compute node may not have local disks and instead use data storage services or remote storage servers. Compute nodes may also be equipped with hardware accelorators to speed up specific applications. Compute nodes often utilize graphics processing units (GPUs) to accelerate modeling and simulation or AI and machine learning model training.

### Data Storage Zone

The **data storage zone** is a dedicated area within the HPC infrastructure that is responsible for storing, managing, and accessing data associated with computational workloads. It comprises one or multiple high-speed parallel file systems that provide data storage services for user data.

The high-speed parallel file systems are designed to store very large data sets and provide fast access to data for reading and writing. Several different classes of storage systems may be present inside of the data storage zone. Typical classes of storage found within this zone include **Parallel File Systems** (PFSs) and archival file systems that support campaign storage and protect against data loss. HPC applications' initial data, intermediate results, and results are stored in the data storage zone and can be accessed during the application runtime and after the application's completion. Since HPC workloads can vary significatnly, a PFS is often required to support read-intensive and write-intensive applications with sequential and random-access patterns at speeds of up to terabytes per second.

### Management Zone

The complexity of HPC system requires a significant infrastructure to operate and manage it, which is collectively referred to as the **management zone.** The management zone is responsible for system administration, monitoring, and control of the HPC environment. It allows HPC system administrators to configure and manage the HPC system, including the configuration of compute nodes, storage, networks, provisioning, identity management, auditing, system monitoring, and vulnerability assesment. The management zone may consist of servers and network switches that enable various functions for operating the system with efficiency, effectiveness, and stability.

## HPC Architecture Overview

<iframe width="560" height="315" src="https://www.youtube.com/embed/6pbk-WV1SY8?si=faNR6YrBlso09Xlx" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---
## Resources
- [NIST SP 800-223 High-Performance Computing Security](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-223.pdf): Architecture, Threat Analysis, and Security Posture.
- [HPC Kitchen](https://www.youtube.com/playlist?list=PLZLVmS9rf3nNDHRo1Baz_JVQWDI0mTYyB): A series that goes over the basics of High Performance Computing concepts... in the kitchen.
