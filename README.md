# Dynatrace

***What is Dynatrace***
- Dynatrace is a unified observability platform built for modern, cloud-native, distributed environments — supporting infrastructure, applications, user experience, security, business analytics and more in one     solution. 
- It is offered by Dynatrace, Inc., an American publicly-traded tech company originally founded in 2005 in Austria. 
- The platform uses a proprietary AI engine (called “Davis”) to do root-cause analysis, anomaly detection, dependency mapping and more. 
- It supports hybrid environments: on-premises + cloud + multi-cloud, containerised microservices (e.g., Kubernetes) and traditional workloads. 

***Key Components & How It Works***

****Here’s a breakdown of major architectural pieces:****
- OneAgent: A lightweight agent you install on your hosts/containers etc. It auto-discovers processes, services, dependencies, collects metrics/traces/logs. 
- Smartscape / topology mapping: Dynatrace builds a live map of your entire stack (services, containers, hosts, network dependencies) to show relationships automatically. 
- Davis AI engine: The AI component that sifts through huge volumes of telemetry, finds anomalies, correlates across metrics/logs/traces, surfaces root-causes, and reduces alert noise. 
- Unified observability data platform: It brings together metrics + logs + traces + user experience data + business events. 
- Platform integrations & extensions: Dynatrace supports cloud platforms (AWS, Azure, Google), container orchestration (Kubernetes), open standards (OpenTelemetry), and gives you an app-extension ecosystem.

## Infrastructure Observability
***Host Performance Data***
- Host Performance Data refers to all the system-level metrics collected from a physical server or virtual machine (VM). These metrics help you understand how healthy, efficient, and stable a host is.
- In observability tools, host performance data is the foundation for detecting issues, bottlenecks, and resource limitations.
  
| **Category**                  | **Metrics**                       | **Description / Purpose**                                          |
| ----------------------------- | --------------------------------- | ------------------------------------------------------------------ |
| **CPU Metrics**               | CPU usage (%)                     | Shows how much CPU is actively used; helps detect saturation.      |
|                               | CPU load average                  | Indicates system load over 1/5/15 min; helps detect overload.      |
|                               | System time, user time, idle time | Shows CPU time spent in kernel mode, user mode, and idle.          |
|                               | Steal time                        | Measures CPU cycles stolen by hypervisor (important in cloud VMs). |
|                               | CPU throttling (containers)       | Indicates if containers are hitting CPU limits.                    |
| **💡 Purpose**                |                                   | Detects CPU bottlenecks, thread issues, hotspots.                  |
| **Memory Metrics**            | Total memory                      | Total RAM available.                                               |
|                               | Memory used / free                | Detects memory pressure or low free memory.                        |
|                               | Buffer/cache memory               | Shows memory used for caching; often reused by the OS.             |
|                               | Swap in/out rate                  | High swap indicates memory shortage.                               |
|                               | Memory page faults                | Indicates heavy memory paging; possible memory contention.         |
| **💡 Purpose**                |                                   | Identifies memory leaks, insufficient RAM, excessive swapping.     |
| **Disk Metrics**              | Disk I/O read/write throughput    | Measures bytes/sec read/written.                                   |
|                               | IOPS                              | Number of I/O operations per second.                               |
|                               | Disk latency                      | Time taken for I/O operations; high latency = slow disk.           |
|                               | Disk usage percentage             | Helps detect full/near-full disks.                                 |
|                               | File system usage                 | Tracks usage per mount point.                                      |
| **💡 Purpose**                |                                   | Diagnoses slow apps due to disk latency or full disks.             |
| **Network Metrics**           | Network throughput (in/out)       | Bytes transmitted/received per second.                             |
|                               | Packet rate                       | Number of packets sent/received.                                   |
|                               | Dropped packets                   | Indicates network congestion or NIC issues.                        |
|                               | TCP errors / retransmissions      | High values mean network instability.                              |
|                               | Connection counts                 | Tracks number of active connections.                               |
| **💡 Purpose**                |                                   | Helps detect bandwidth issues, saturation, packet loss.            |
| **Process/Service Metrics**   | Running/stopped processes         | Shows active system processes.                                     |
|                               | Per-process CPU/memory usage      | Identifies heavy resource-consuming services.                      |
|                               | High-consuming processes          | Quickly find the root cause of spikes.                             |
|                               | Threads count                     | Helps detect thread leaks or issues.                               |
| **💡 Purpose**                |                                   | Diagnose runaway services, leaks, or misbehaving processes.        |
| **Host Availability Metrics** | Up/down status                    | Shows if host is reachable and running.                            |
|                               | Host restart events               | Detects unexpected reboots or crashes.                             |
|                               | Kernel version                    | Useful for patching/security compliance.                           |
|                               | OS version                        | Required for compatibility and visibility.                         |
|                               | Uptime                            | Helps track stability and maintenance cycles.                      |
| **💡 Purpose**                |                                   | Important for SLAs, uptime monitoring, and operations.             |

***🌐 How Dynatrace Uses Host Performance Data***

- In Dynatrace, host performance data is collected using OneAgent, which automatically provides:
  - Full host health overview
  - Smartscape topology mapping
  - Correlation with processes, services, and user actions
  - AI-based anomaly detection (Davis AI)
  - Root-cause analysis

Example:
- If CPU spikes, Dynatrace tells you which process caused it and which service request led to the spike — not just showing graphs.
