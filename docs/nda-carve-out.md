# NDA carve-out plan

This plan sets out what this project will publish, what it will cite publicly, and what stays
confidential under TTA's terms. Nodeinfra proposed these categories to TTA, and TTA confirmed
them in writing on 2026-09-23. The one change TTA asked for is marked below. A redacted copy of
TTA's reply is attached to the
[Milestone 1 issue](https://github.com/canton-foundation/canton-dev-fund/issues/814).

## 1. Published: open source under Apache 2.0

TTA confirmed that all of the following can be published. Everything here is Nodeinfra-authored.
None of it reproduces TTA evaluation material.

| Artifact | Contents | Released |
|---|---|---|
| Deployment and configuration scripts | Node initialization, synchronizer topology and bootstrap | M2 |
| Host tuning | OS, JVM, and Postgres settings | M2 |
| Pinned Canton runtime configs | Participant, sequencer, and mediator configuration at a fixed Canton version | M2 |
| Benchmark harness | TPS measurement and fault-injection tooling, built on the upstream Canton performance suite, plus the reproduction procedure | M2 |
| Test harness | Automated tests for the reliability and security criteria. **TTA test item names, check items, and expected values are removed before release.** | M2 |
| Engineering post-mortem | Problems found during verification, the fixes, and deployment lessons | M2 |
| Reference-deployment outline and this plan | [outline](reference-deployment-outline.md) | M1 |

## 2. Cited publicly: press releases, blog posts, talks

After the verification is complete, we may state:

- That the Canton private synchronizer obtained TTA Blockchain Reliability Verification
- The issue date
- Headline figures, such as TPS and the number of BFT node faults tolerated
- The **names** of the guideline requirement areas verified (for example consensus and fault
  tolerance, key management, smart-contract security, privacy). We name the areas only, never
  how each one was tested.

**Change requested by TTA:** the test report number is **not** cited publicly.

**Conditions set by TTA:**

- Press releases and blog posts go to TTA for review by its external-relations team before
  publication.
- The test report itself is never distributed.

## 3. Confidential: TTA-confidential, never published

TTA confirmed that the following stay confidential:

- The full submission package: application, system description, architecture documents,
  operating procedures
- TTA's evaluation checklist: the list of test items and their pass/fail criteria
- The mapping table between guideline requirements and test items
- Detailed test contents: procedures, inputs, pass/fail conditions, and test logs
- The test report itself, including per-item scores and results

## Comparison with the proposal

Every artifact that [proposal #419](https://github.com/canton-foundation/canton-dev-fund/pull/419)
commits to publish, and how this plan covers it:

| Artifact named in the proposal | TTA ruling (2026-09-23) | Where it is published | Release |
|---|---|---|---|
| Deployment and configuration scripts | Publishable | `deploy/`, `config/` | M2 |
| NUMA-aware host tuning | Publishable | `host/` | M2 |
| Postgres backing | Publishable (Postgres tuning values) | `host/`, `config/` | M2 |
| Pinned Canton 3.x runtime substrate | Publishable | `config/` (participant, sequencer, mediator) | M2 |
| Benchmark harness, built on the upstream Canton performance suite | Publishable, including fault injection and the reproduction procedure | `bench/` | M2 |
| Test harness, "subject to consultation with TTA" | **Cleared.** Publishable once TTA test item names, check items, and expected values are removed | `tests/` | M2 |
| Engineering post-mortem | Publishable | `docs/` | M2 |
| Reference-deployment outline | Not TTA material | [`docs/reference-deployment-outline.md`](reference-deployment-outline.md) | M1, published |
| NDA carve-out plan | Not TTA material | This document | M1, published |

Every artifact is covered, and the one conditional item in the proposal, the test harness, is
now cleared.

On what is cited publicly, the proposal already kept the result report confidential and said
the BRV result and headline metrics are citable "subject to prior consultation with TTA". TTA's
reply confirms exactly that. The report number was never part of the published surface. The
next section sets out how the Milestone 2 criterion, "TTA-issued BRV result, publicly
verifiable", is met under these terms.

## How the Milestone 2 result will be verified

TTA does not allow the report number to be cited or the report to be distributed, so
verification works as follows:

1. **Public announcement.** Nodeinfra publishes an announcement that the Canton private
   synchronizer obtained TTA BRV, with the issue date and headline figures. As TTA requires,
   the text is reviewed and approved by TTA's External Relations Department before publication.
2. **TTA's written approval.** TTA's approval of that text is attached, redacted, to the
   [Milestone 2 issue](https://github.com/canton-foundation/canton-dev-fund/issues/815),
   alongside the published announcement. It is TTA's own written confirmation of the result.
3. **Direct confirmation.** The Committee may also confirm the issuance directly with TTA; we
   will provide the TTA contact on request.
