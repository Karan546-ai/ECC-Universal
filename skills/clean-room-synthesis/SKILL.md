---
name: clean-room-synthesis
description: "Transform reverse-engineered specifications and evidence into unencumbered, production-ready software using clean-room engineering principles and TDD. Use when building a clean-room reimplementation, cloning a feature with legal safety, or modernizing proprietary software."
metadata:
  origin: ECC
---

# Clean-Room Synthesis Workflow

This skill bridges the gap between Reverse Engineering (REA) and Forward Engineering (ECC). It takes behavioral specifications and evidence reports, and guides the creation of clean, legally compliant, test-driven production code.

## When to Activate

- Re-implementing a feature based on a reverse-engineering report or API specification
- Building an open-source or interoperable alternative to a proprietary protocol or service
- Modernizing a legacy compiled binary into a cloud-native service
- Ensuring strict copyright separation between decompiled assets and new implementation

## Core Principles

### 1. Functional Equivalence without Source Contamination
The clean-room engineer operates solely on the functional specification (the "Room"). No proprietary code snippets, comments, or decompiled ASTs are ever merged into the destination repository.

### 2. Spec-Driven TDD (Test First)
Every behavioral requirement and invariant identified during reverse engineering is first encoded as a failing test case.

---

## Synthesis Pipeline

```text
[Reverse Engineering Spec] 
       ↓
[Phase 1: Architecture Blueprint] -> ecc:architect defines interfaces and domain models
       ↓
[Phase 2: Failing Test Suite (RED)] -> ecc:tdd-guide writes unit/integration tests
       ↓
[Phase 3: Clean Implementation (GREEN)] -> ecc:code-architect builds clean logic
       ↓
[Phase 4: Security & Verification] -> ecc:security-reviewer & verification loops
```

### Phase 1: Architecture Blueprinting
1. Review the input specification (`REVERSE_ENGINEERING_REPORT.md` or OpenSpec capability).
2. Invoke `ecc:architect` to design idiomatic interfaces in the target language (e.g., TypeScript, Python, Go, Rust).
3. Ensure high cohesion, loose coupling, and immutability.

### Phase 2: Test Suite Formulation (RED)
1. Write contract tests validating request/response schemas.
2. Write unit tests for state machine transitions.
3. Verify that all tests fail before writing production code.

### Phase 3: Clean Implementation (GREEN)
1. Write minimal, elegant code to satisfy the tests.
2. Refactor for performance, readability, and maintainability.
3. Verify test coverage meets or exceeds 80%.

### Phase 4: Security & Quality Audit
1. Run `ecc:security-reviewer` to ensure no security flaws were introduced.
2. Run `ecc:code-reviewer` to ensure compliance with repository coding standards.

---

## Anti-Patterns

- **Source Code Leakage**: Pasting decompiled code strings into comments, tests, or documentation.
- **Skipping RED Phase**: Writing code before validating that tests actually catch regressions.
- **Over-Fitting to Legacy Quirks**: Replicating broken legacy bugs unless explicitly required for backwards compatibility.
- **Lack of Provenance**: Failing to record which behavioral requirement drove a specific test case.
