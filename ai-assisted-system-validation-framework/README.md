# AI-Assisted Server Validation Framework (Experimental)

A modular, lab-scale framework for exploring hardware validation workflows, observability-driven debugging, and optional LLM-assisted failure interpretation in server systems.

> Note: The framework is intended for **research and experimentation purposes only** and is not tied to any production system or vendor-specific infrastructure.

---

## Design Goals

- Modular and extensible validation framework design
- Deterministic execution for reproducibility
- Clear separation between execution, observability, and analysis
- Structured logging for traceable debugging workflows
- Optional LLM-assisted post-processing for experimental analysis only
- Framework-agnostic hardware abstraction

---

## System Structure

The framework is organized into independent modules representing logical responsibilities in a hardware validation workflow.

```
testcase/     → Test scenario definition and execution flow orchestration  
capability/   → Component-level hardware validation logic  
api/          → Hardware abstraction layer
tool/         → Low-level execution utilities
logging/      → Structured event logs and trace collection  
report/       → Structured result generation (JSON / HTML)  
analysis/     → Optional post-execution LLM-assisted interpretation
config/       → Declarative YAML-based test definitions  
utils/        → Shared helper utilities  
```

**Layering Principle**: The framework enforces a strict layered architecture with downward-only dependencies to ensure deterministic execution and clear separation of concerns.

**Layer Rule**: Each layer only calls downward — testcases → capabilities → APIs → tools.

Post-processing modules (logging, reporting, analysis) operate on per-iteration execution artifacts and do not influence runtime control flow or subsequent test behavior.

---

## Validation Execution Model

### Validation Workflows

#### 1. System Initialization Checks
- Basic subsystem readiness checks 
- Device discovery and enumeration validation 
- Resource availability verification  

#### 2. Stress-Based Experiments
- CPU / memory / I/O stress execution  
- Resource contention observation  
- System stability evaluation under load  

#### 3. Reboot-Based Experiments
- Repeated execution across reboot cycles  
- Detection of intermittent or state-dependent behaviors  
- Boot consistency verification


### Execution Lifecycle

Each test run follows a deterministic lifecycle:

- Setup phase
- Execution phase
- Validation phase
- Cleanup phase

---

## LLM-assisted Analysis (Experimental)

The framework includes an optional module for post-execution failure interpretation using LLMs.

### Workflow

1. Collect structured logs from test execution  
2. Extract key failure signals  
3. Build summarized analysis context  
4. Send context to LLM API  
5. Generate interpretive insights

### Reasoning Strategy (Experimental)
The analysis module adopts a hierarchical reasoning strategy to enhance robustness:

1. Primary LLM‑assisted analysis is executed on structured logs.
2. If the primary output is insufficient or unavailable, a secondary LLM serves as fallback.
3. If both LLM layers fail or are unreachable, a rule‑based heuristic system delivers minimal deterministic output.

This ensures the system produces consistent structured analysis results.

The LLM is used for:

- Failure hypothesis generation  
- Debugging suggestions  

> This module operates strictly on post-execution data and does not influence runtime execution or control flow.

### Example Output (Illustrative)

```
**AI Root Cause (Hypothesis)**

The analysis suggests a potential instability in the NIC’s PCIe link training process. The device appears unable to maintain a stable Gen4 link under repeated validation runs, with observed AER correctable errors indicating possible signal integrity degradation.

**P0 Critical Recommendations (Suggestions)**

- Replace NIC with a known-good unit
- Inspect PCIe slot for physical damage or contamination
(Full recommendations are provided in the iteration-level report output.)
```
P0 recommendations in the Summary Report are intentionally limited to the most critical actions, while complete troubleshooting guidance remains available in Iteration Reports.

---

## Observability & Output Model

All execution outputs are captured in structured form:

- Raw execution logs
- Structured test results
- Per-run artifacts (JSON / HTML)
- Aggregated summaries across runs (JSON / HTML)

The system is designed so that test execution can be fully reconstructed from logs and artifacts.

All outputs are written to `framework/logs/`:

|File                       |Description                         |
|---------------------------|------------------------------------|
|`{test}_iteration_{N}.log` |Per-iteration raw log               |
|`{test}_iteration_{N}.json`|Structured validation + AI results  |
|`{test}_iteration_{N}.html`|Human-readable iteration report     |
|`{test}_summary.json`      |Aggregated summary across iterations|
|`{test}_summary.html`      |Summary report with AI root cause   |
|`{test}.log`               |Global execution trace              |

This two-layer reporting model separates:
- Iteration-level debugging
- System-level aggregation

---

## Roadmap

- [ ] observability integration
- [ ] Historical trend analysis
- [ ] Multi-node orchestration
- [ ] Enhanced AI-assisted RCA 

---

## Compliance Note

This project is an independent experimental framework created for research and educational purposes only.

It does not:

- Represent any proprietary system
- contain internal validation infrastructure
- depend on confidential production data
