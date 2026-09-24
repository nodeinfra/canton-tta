# Reference-deployment outline

This outline covers the deployment that will go through TTA Blockchain Reliability Verification
(BRV), and how anyone can reproduce its metrics. The full stack is published here at
Milestone 2, after verification. What is published and what stays confidential is set out in the
[NDA carve-out plan](nda-carve-out.md).

## 1. Verification target

- **Product:** Canton Private Synchronizer (the product name on the TTA application)
- **Evaluation basis:** NCSC 「국가ㆍ공공기관 도입을 위한 블록체인 암호기술 가이드라인」 (2020.12)
- **Scope:** the synchronizer as upstream Canton ships it. We change no protocol behavior.
  Any gap-closing work is on the configuration and deployment side. Any protocol-side
  finding goes upstream through the standard Canton CIP and release process.

## 2. Topology

| Component | Count | Role |
|---|---|---|
| Sequencer (BFT ordering) | 4 | Total-order sequencing; tolerates f = 1 faulty node |
| Mediator | 3 | Transaction confirmation (commit/abort decision) |
| Participant | 4 | Hosts parties; validates and commits its view of each transaction |
| Postgres | 1 per node | Persistent storage for each Canton node |

Each node runs on its own host. Nodes are spread across locations, so losing one whole location
is a scenario we test.

## 3. Stack

| Layer | Choice |
|---|---|
| Canton runtime | Canton 3.5.x open source; the exact patch release is fixed at submission |
| JVM | OpenJDK, latest LTS supported by the pinned Canton release (currently 25), with heap/GC settings published under `host/` |
| Database | PostgreSQL, latest major release supported by the pinned Canton release (currently 18), with tuning published under `host/` |
| OS / host | Ubuntu Server, latest LTS (currently 26.04); NUMA-aware CPU and memory pinning; kernel, network, and file-descriptor tuning |
| Infrastructure | Cloud-hosted verification environment |

Versions are chosen when the environment is submitted to TTA and do not change after that.
At Milestone 2, every version above is pinned in the published configs, so anyone re-running
the stack gets exactly what was verified.

## 4. Metrics-reproduction plan

The benchmark harness is Nodeinfra-authored. It builds on the upstream
[Canton open-source performance benchmark suite](https://github.com/digital-asset/canton/blob/main/performance/README-xfer.md)
and ships at Milestone 2 as `bench/`.

**What it measures**

- **Throughput:** sustained transactions per second at a fixed offered load, plus a separate
  run to find maximum throughput
- **Latency:** end-to-end processing time through the synchronizer, from submission through
  ordering and confirmation to commit at the participants involved. Reported as mean, p50,
  p95, and max.
- **Fault tolerance:** throughput and liveness while sequencer nodes crash, while a whole
  location is lost, and while the sequencer quorum is lost and then restored

**How a third party reproduces it**

1. Provision hosts to the published topology and apply `host/` tuning.
2. Deploy the pinned runtime with `deploy/` and `config/`.
3. Run `bench/` at the documented load profile, with repeated runs for each measurement.
4. Run the fault-injection scenarios in `bench/` and record behavior during and after each fault.
5. Compare against the headline metrics published after BRV issuance.

The reproduction guide under `docs/` lists the exact commands, load parameters, and run counts.

## 5. Milestone 2 deliverables

- Deployment and configuration scripts (`deploy/`, `config/`)
- Host tuning (`host/`)
- Pinned Canton runtime configs for participant, sequencer, and mediator
- Benchmark and fault-injection harness (`bench/`)
- Test harness, with TTA test contents removed (`tests/`)
- Engineering post-mortem: findings, fixes, and deployment lessons
