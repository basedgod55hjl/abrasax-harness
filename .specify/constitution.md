# ABRASAX Constitution — abrasax-harness

Spec-Driven Development constitution. Every feature in this repo is built
under these principles. Version 1.0, ratified by Kairos 2026-11-08.

## 1. Truth before claims
No capability is reported as working without a live check. Every plan,
task, and convergence report cites the evidence: command output, hash,
port probe, or test result. "Seems to work" is not a status.

## 2. One source of truth
Paths resolve from ABRASAX_ROOT (C:\abrasax). No hardcoded machine paths
in new code. Registries (MODEL_REGISTRY, AGENT_REGISTRY) are the canonical
inventory; code that needs a model or a port consults them or the .env.

## 3. Verify at full scale
Samples are not proof. Whole-file hashes, full extraction round-trips,
and end-to-end chats are the acceptance standard. A smoke test that passes
by luck is a bug to find (see the tile bitstream incident).

## 4. Secrets never transit
Tokens and keys live in .env or protected storage. They never appear in
source, logs, prompts, or commit messages. Credentials pasted in chat are
treated as compromised.

## 5. Bind before you ship
Repos carry BOND manifests signed by the TPM-sealed soul; releases are
hash-verified. Anything pushed without a BOND is incomplete.

## 6. Safe defaults, honest limits
CPU-first unless the hardware supports it (measured, e.g. MXFP4 has no
sm_75 kernels). Degradation is graceful: one wedged model must not take
the stack down; supervisors restart, guards protect the important path.

## 7. Document the drift
Every significant change lands in the journal (DOC/KAIROS_BUILD_*.md)
and the relevant registry. The system must explain what changed and why.
