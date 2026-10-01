# Architecture decision notes

These notes summarize how I reason about services encountered during guided labs and exam preparation. They are **conceptual examples**, not deployed customer systems or proof that every option was tested in my account.

## 1. Private access is not one feature

| Requirement | Candidate mechanism | Why it matters |
| --- | --- | --- |
| A VM without an external IP must call supported Google APIs | Private Google Access | Allows access to Google APIs and services through Google's network; it does not provide general internet access. |
| A private VM must initiate connections to the public internet | Cloud NAT | Provides outbound translation without assigning an external IP to the VM; it is not an inbound access path. |
| Two VPCs must exchange private traffic | VPC Network Peering | Connects networks privately, subject to routing and non-transitive peering behavior. |
| A service must accept user traffic | Load balancer and suitable backends | Ingress and backend health are separate decisions from NAT or API access. |

**Decision rule:** Start with the traffic path and destination. “Private” by itself does not identify the correct service.

Related labs: [networking and scaling](LABS.md#networking-and-scaling).

## 2. Match the runtime to the operational model

| Situation | Starting point | Check before deciding |
| --- | --- | --- |
| Containerized request-driven service with minimal infrastructure management | Cloud Run | Request model, startup behavior, scaling, and integration needs |
| Multiple containerized services needing Kubernetes APIs and orchestration | GKE / GKE Autopilot | Workload requirements, cluster responsibility, networking, and scaling controls |
| VM-based workload that needs repeatable instances | Managed instance group | Instance template, health checks, autoscaling signal, and update strategy |

**Decision rule:** Kubernetes is powerful but should not be the default answer simply because an application is containerized.

Related labs: [applications and Kubernetes](LABS.md#applications-and-kubernetes).

## 3. Pick data services by workload, not product name

| Workload shape | Candidate service | Key question |
| --- | --- | --- |
| Relational application database | Cloud SQL | Do managed relational features meet scale and availability needs? |
| Globally distributed relational transactions | Spanner | Is global consistency and horizontal scale actually required? |
| Large analytical SQL scans | BigQuery | Is this an analytics workload rather than operational transactions? |
| High-throughput key/range access to wide-column data | Bigtable | Does the access pattern fit row-key design? |
| Document-oriented application data | Firestore | Does the document model fit the app's queries and consistency needs? |

**Decision rule:** First classify transactional versus analytical use, then data model, scale, latency, and operations.

Related labs: [databases and analytics](LABS.md#databases-and-analytics).

## 4. Separate identity, secrets, keys, and retention

| Control | Its job | Not a substitute for |
| --- | --- | --- |
| IAM and service accounts | Decide who or what can access a resource | Encryption key management |
| Secret Manager | Store and deliver application secrets | Identity and authorization design |
| Cloud KMS | Manage cryptographic keys and key operations | Secret storage or network isolation |
| Bucket Lock | Enforce a Cloud Storage retention policy | General access control |
| Log Analytics | Investigate events and operational signals | Preventive security controls |

**Decision rule:** A security requirement often needs several layers. Choose each layer for the risk it actually addresses.

Related labs: [foundations and identity](LABS.md#foundations-and-identity), [security and operations](LABS.md#security-and-operations).

---

The next step is to validate selected decisions in original, reproducible projects and attach code and test evidence. Until then, these notes document understanding, not production experience.
