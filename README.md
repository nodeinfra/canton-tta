# canton-tta

Reference deployment for taking the **Canton private synchronizer** through Korea's TTA
[Blockchain Reliability Verification](https://www.tta.or.kr/eng/contents?contentId=316&key=361)
(BRV, 블록체인 신뢰성 검증), funded by the Canton Foundation Development Fund
([proposal #419](https://github.com/canton-foundation/canton-dev-fund/pull/419)).

BRV evaluates a permissioned chain against the NCSC 「국가ㆍ공공기관 도입을 위한 블록체인 암호기술
가이드라인」 (Blockchain Cryptographic Technology Guideline for Adoption by National & Public
Institutions, 2020.12). The result attaches to the Canton private synchronizer software, not to
any single operator. This repository publishes the self-built deployment, configuration, and
tooling so other teams can stand up the same stack and reproduce its metrics.

## Status

| Milestone | Scope | Status |
|---|---|---|
| [M1](https://github.com/canton-foundation/canton-dev-fund/issues/814) | Kickoff and TTA engagement | Delivered, in review |
| [M2](https://github.com/canton-foundation/canton-dev-fund/issues/815) | BRV result issued; verified stack published | Not started |
| [M3](https://github.com/canton-foundation/canton-dev-fund/issues/816) | Institutional adoption of the verified synchronizer | Not started |

## Documents

- [Reference-deployment outline](docs/reference-deployment-outline.md): the stack to be verified and the metrics-reproduction plan
- [NDA carve-out plan](docs/nda-carve-out.md): what is and is not open-sourced, as confirmed with TTA

## Planned contents

Published at Milestone 2, once the stack has been verified:

```
deploy/      deployment and topology scripts (node init, synchronizer bootstrap)
config/      pinned Canton runtime configs (participant, sequencer, mediator)
host/        OS, JVM, and Postgres tuning
bench/       benchmark and fault-injection harness, built on the upstream Canton performance suite
tests/       reliability and security test harness (TTA test contents removed)
docs/        reproduction guide and engineering post-mortem
```

## License

[Apache License 2.0](LICENSE). Copyright Nodeinfra.
