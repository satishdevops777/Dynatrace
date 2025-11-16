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

***🚨 Types of Dynatrace Problem Monitoring***
- Dynatrace automatically detects problems using its AI engine (Davis AI).
- A problem is any abnormal event affecting application performance, services, infrastructure, user experience, or availability.
- Dynatrace problems are typically grouped into the following major categories:
🟦 1. Availability Problems
  - Triggered when something becomes unavailable or down.
  - Examples: Host down, Process down, Service unreachable, Application unavailable (HTTP 5xx spike), Kubernetes node/Pod not running, Database connection failure
🔎 Davis AI identifies the root cause: who became unavailable, why, and the impact.

🟩 2. Performance Problems
- Triggered when a system is slow, degraded, or underperforming.
- Examples: High response time, Slow transactions, Backend service latency, Slow database queries, Frontend user actions taking longer than baseline, API endpoint performance regression
📌 Dynatrace uses baselines and anomaly detection to compare real vs expected performance.

🟧 3. Resource Exhaustion Problems
- Triggered when system resources are overused or nearing exhaustion.
- Examples: 
  - CPU Related: CPU saturation, High CPU usage by processes, Container CPU throttling
  - Memory-related: High memory usage, Memory leak detection, Out-of-memory (OOM) events
- Disk-related: Disk full / near full, Disk I/O bottleneck, High disk latency
- Network-related: High network traffic, Packet drops, Network saturation
🧠 Dynatrace correlates resource issues with affected services and processes.

🟪 4. Error & Failure Problems
- Triggered when error counts exceed the expected baseline.
- Examples: HTTP 5xx/4xx error spike, Java/Python/Node.js exceptions, Database query failures, Timeout errors, TCP connection resets, Failed service calls
🟠 Often tied to code issues, downstream failures, or infrastructure interruption.

🟫 5. Anomaly & Behavioral Problems
- Triggered when something behaves differently than the normal baseline.
- Examples: Sudden spike in traffic, Unexpected drop in requests, Anomalous user behavior, Sudden decrease in throughput, Unusual host reboot pattern, Traffic imbalance between nodes
💡 Davis AI detects anomalies using dynamic baselines, not fixed thresholds.

🟥 6. Security Problems (Dynatrace AppSec)
- Triggered by runtime vulnerabilities or attacks (if AppSec is enabled).
- Examples: Vulnerable third-party libraries, Runtime exploits, Suspicious API behaviour, Attack attempts on services, Log4j/remote execution vulnerabilities
🔐 These appear in the Security dashboard and problem feed.

🟨 7. Synthetic Monitoring Problems
- Triggered in Synthetic browser/API tests.
- Examples: Synthetic availability test failure, SLA violation for synthetic monitors, High synthetic response time, Step failure during script execution
🌍 Useful for global uptime and end-user monitoring.

🟩 8. Real User Monitoring (RUM) Problems
- Triggered when end-user experience degrades.
- Examples: High frontend JavaScript errors, Slow page load time, Rage clicks (user frustration), Session anomalies, High mobile app crash rate
📊 Dynatrace correlates frontend issues with backend failures.

🌀 9. Kubernetes/Container Problems
- Specific to cloud-native environments.
- Examples: Pod crash loops, Container restart storm, Node pressure (CPU/memory/disk), Pending Pods (insufficient resources), HPA misbehaviour, Service routing issues
⚙ Fully integrated with Kubernetes API + OneAgent data.

| **Problem Type**    | **Examples**              | **Area Impacted**   |
| ------------------- | ------------------------- | ------------------- |
| Availability        | Host/Service down         | Infra / Services    |
| Performance         | Slow response time        | Apps / Services     |
| Resource Exhaustion | CPU/Memory/Disk issues    | Host / Containers   |
| Errors & Failures   | 5xx, exceptions           | Code / Services     |
| Anomalies           | Traffic spikes, deviation | Behaviour / Trend   |
| Security (AppSec)   | Vulnerabilities           | Security            |
| Synthetic           | Failed tests              | Global availability |
| RUM                 | Frontend performance      | Users               |
| Kubernetes          | Pod/Node issues           | Cloud-native        |

***🌟 Dynatrace Monitoring Modes Explained (Full-Stack vs Infrastructure-Only)***
- Dynatrace uses OneAgent to monitor hosts.
- But your cost and features depend on which monitoring mode you choose.
- There are two modes:
  - Full-Stack Monitoring (default)
  - Infrastructure-Only Monitoring
- Each mode consumes a different number of Host Units (credits).
- Since OneAgent is licensed per host, bigger hosts ≠ same cost.
- Host size, RAM, and monitoring mode directly impact your license consumption.

🧭 Where to Check or Change Monitoring Mode
- You can view and modify monitoring mode from:
  - Settings → Monitoring → Monitoring Overview
- Inside Monitoring Overview:
  - You see all monitored hosts.
- Clicking Edit on any host shows:
  - Whether OneAgent is enabled or disabled
  - Whether the host uses Full-Stack or Infrastructure-Only monitoring
- You can switch modes anytime.

| **Feature / Capability**                            | **Full-Stack Monitoring**               | **Infrastructure-Only Monitoring**                  |
| --------------------------------------------------- | --------------------------------------- | --------------------------------------------------- |
| **License Consumption**                             | High (1 Host Unit for 16 GB RAM)        | Low (~0.3 Host Units for 16 GB RAM)                 |
| **Cost**                                            | More expensive                          | ~3× cheaper                                         |
| **Host-level metrics (CPU, Memory, Disk, Network)** | ✔ Yes                                   | ✔ Yes                                               |
| **Process Monitoring**                              | ✔ Full details                          | ✔ Limited (basic processes only)                    |
| **Service Monitoring**                              | ✔ Full visibility                       | ❌ Not collected                                     |
| **Application Performance Monitoring (APM)**        | ✔ Enabled                               | ❌ Disabled                                          |
| **Distributed Tracing (PurePath)**                  | ✔ Available                             | ❌ Not available                                     |
| **Code-Level Insights**                             | ✔ Deep code analysis                    | ❌ Not provided                                      |
| **Database Query Monitoring**                       | ✔ Full DB insights                      | ❌ Not available                                     |
| **Service Flow & Dependency Mapping**               | ✔ Available                             | ❌ Disabled                                          |
| **Davis AI Root Cause Analysis (full context)**     | ✔ Complete RCA                          | ❌ Only infra-level RCA                              |
| **Log Monitoring**                                  | ✔ Full context logs                     | ✔ Yes (limited context)                             |
| **Real User Monitoring (RUM)**                      | ✔ Available                             | ❌ Not available                                     |
| **Synthetic Monitoring Correlation**                | ✔ Full correlation                      | ✔ Limited                                           |
| **Container Monitoring**                            | ✔ Full container insight                | ✔ Basic container metrics                           |
| **Cloud Platform Auto-Discovery** (AWS, Azure, GCP) | ✔ Full resource + services              | ✔ Resource-only                                     |
| **Security Monitoring (AppSec)**                    | ✔ Vulnerability detection               | ❌ Not available                                     |
| **Use Case**                                        | Production, customer-facing systems     | Dev/Test, background services, cost-optimized nodes |
| **Best For**                                        | Applications needing full observability | Hosts needing only infra metrics                    |

🔍 How to Decide Which Mode to Use
- Choose Full-Stack Monitoring if:
  - You need application performance insights
  - You want PurePath distributed tracing
  - You want service-level RCA from Davis AI
  - You need user experience monitoring
  - Your workload is customer-facing or business-critical
- Choose Infrastructure-Only if:
  - You only need system performance (CPU/Mem/Disk/Network)
  - You mainly monitor databases, proxies, or background services
  - You want cheaper monitoring for dev/test environments
  - Most work happens inside containers and you use DDU-based app monitoring

🎯 Best Practice / Recommendation
- Before enabling hosts in Full-Stack:
  - Review what kind of observability you actually need
  - Check your Dynatrace license usage vs budget
  - Use Infra-only for non-critical hosts
  - Use Full-Stack selectively for application-tier servers
  - Document the reason behind each mode choice
- This avoids overspending and ensures value-driven monitoring.

***Note:***
- Full-Stack Monitoring = Complete application + infra observability
- Infrastructure-Only = Essential system-level monitoring at reduced cost

***⭐ Dynatrace Frequent Issue Feature***
- Dynatrace continuously detects problems across your environment.
- But if the same problem keeps happening repeatedly within a short time, Dynatrace prevents alert fatigue using a feature called Frequent Issue Detection.
🔵 What Is a Frequent Issue?
  - A Frequent Issue is a problem that:
  - Occurs repeatedly
  - Within a rolling one-week (7-day) window
  - Has similar intensity/severity across occurrences
  - When Dynatrace identifies that a problem keeps happening often, it classifies it as a Frequent Issue.

🔕 What Happens When a Problem Becomes a Frequent Issue?
- When a problem becomes a frequent issue:
  - It will still appear in the Dynatrace dashboard
  - You will no longer receive alerts for it (unless the severity becomes significantly worse)
  - Example: If CPU saturation keeps happening multiple times across the week:
    - Dynatrace tags it as a Frequent Issue
    - Alerts stop, because Dynatrace assumes you already know about it
    - The issue remains visible in the Frequent issues list
➡️ Important:
  - Just because you are no longer getting alerts does not mean the problem is solved.
🔥 When Will a Frequent Issue Trigger Alerts Again?
 - Dynatrace will alert again only if:
  - The severity gets worse
  - The issue escalates beyond the historical baseline
  - The pattern deviates significantly from the last week’s behaviour
- Example:
  - If CPU saturation goes from 80% spikes to 95% continuous load → new alert triggered.

## Cloud Automation


