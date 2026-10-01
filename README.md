# Google Cloud Hands-On Labs

A portfolio index of Google Cloud lab work I practiced while preparing for the Professional Cloud Architect certification. It focuses on what I worked with and learned, rather than presenting guided lab exercises as original production projects.

## Areas practiced

| Area | Hands-on work |
| --- | --- |
| Networking | VPCs, firewall rules, VPC peering, Private Google Access, Cloud NAT, load balancing, Cloud DNS, and managed instance group autoscaling |
| Compute and applications | Compute Engine VMs and persistent disks, Cloud Run, GKE, GKE Autopilot, deployments, networking, and autoscaling |
| Data and storage | Cloud Storage, Bucket Lock, Cloud SQL, BigQuery, Firestore, Spanner, and Bigtable |
| Identity, security, and operations | IAM, service accounts, Secret Manager, Cloud KMS, and Log Analytics |

See [LABS.md](LABS.md) for the individual lab names.

## How I approach an architecture task

1. Identify the non-negotiable requirements: security boundaries, availability, latency, compliance, and budget.
2. Rule out services that cannot meet those requirements.
3. Compare the remaining options on operational effort, scalability, and cost.
4. Validate the design with a small lab or test before claiming it is production-ready.

## Evidence and scope

The lab names in this repository were reconstructed from my study conversations and activity notes. Some guided labs were only partially completed or were not marked as passed by the lab platform; the list is **not** a list of earned Skill Badges. This repository currently contains documentation, not the original lab environments, source code, or deployable infrastructure. I will add reproducible projects and screenshots only when I have the underlying artifacts and have removed credentials, project IDs, and other sensitive data.

No exam dumps, paid course questions, or third-party lab instructions are included.
