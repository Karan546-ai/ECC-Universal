---
name: reverse-engineering
description: "Reverse engineer binaries, Electron applications, web bundles, and runtime behaviors using the local REA engine. Extract evidence-based APIs, data structures, and protocol specifications. Use when analyzing an existing app, understanding binary internals, decompiling JavaScript ASTs, or preparing for clean-room implementation."
metadata:
  origin: ECC
---

# Reverse Engineering Workflow (Powered by REA)

This skill provides a structured, evidence-backed workflow for analyzing closed-source applications, binaries, and web bundles using REA (Reverse Engineer Anything).

## When to Activate

- Analyzing a closed-source application, binary, or website feature to understand how it works
- Inspecting Electron desktop apps (`.asar`), Webpack/Vite bundles, or minified JavaScript
- Reverse engineering network protocols, undocumented APIs, or local IPC mechanisms
- Extracting data schemas and state machines from compiled code
- Preparing behavioral specifications for clean-room software recreation

## Core Principles

### 1. Evidence Provenance
Always distinguish between:
- **Observed**: Concrete data directly extracted from decompilation, symbol tables, or network traces.
- **Derived**: Facts calculated deterministically from observed data (e.g., hash algorithms, schema structures).
- **Inferred**: Hypotheses based on naming conventions or common library patterns.

### 2. Clean-Room Separation
Do not copy raw decompiled code verbatim into production repositories. The goal of reverse engineering is to extract the **behavioral specification, contract, and invariants**, allowing clean-room forward engineering.

---

## Step-by-Step Execution

### Step 1: Target Inspection & Reconnaissance
Identify the target application surface:
```bash
# Check file type and binary metadata
node integrations/rea/scripts/rea.mjs inspect <target-path>
```
1. If the target is an **Electron App**:
   - Extract `resources/app.asar` using REA's built-in ASAR extractor.
   - Locate main process (`main.js`) and renderer bundles.
2. If the target is a **Web Application**:
   - Trace bundle source maps or deobfuscate minified code using AST parsers.
3. If the target is a **Native Binary** (Mach-O, ELF, PE):
   - Check symbol tables, imported libraries, and string tables via REA's Hopper/Ghidra bridges.

### Step 2: Protocol & Data Model Extraction
- Identify data storage formats (SQLite schemas, LevelDB keys, JSON configuration).
- Map network requests and responses: headers, authentication tokens, payload schemas.
- Document IPC channels (Electron `ipcRenderer.send` / `ipcMain.handle`).

### Step 3: Compile the Reverse Engineering Report
Output a structured Markdown artifact (`REVERSE_ENGINEERING_REPORT.md`):
- **Executive Summary**: What the feature does.
- **Observed Wire Contracts**: Request/Response schemas.
- **State Machine**: Triggers, states, and side effects.
- **Cryptographic/Hashing Invariants**: Any specific algorithms observed.

### Step 4: Handoff to Clean-Room Synthesis
Transition directly to the `clean-room-synthesis` skill and `ecc:planner` to implement the capability from scratch.

---

## Anti-Patterns

- **Direct Code Plagiarism**: Copying proprietary decompiled code directly into production codebases without clean-room re-implementation.
- **Hallucinating Invariants**: Guessing how an undocumented API works without verifying the network trace or binary symbol.
- **Unbounded Tracing**: Attaching invasive tracers without filtering, causing massive token overflows and log pollution.
- **Ignoring Failure Handlers**: Only analyzing the happy path while ignoring error codes and boundary conditions.
