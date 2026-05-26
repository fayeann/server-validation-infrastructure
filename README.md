# Server Validation Infrastructure

A server validation infrastructure repository combining reusable system validation framework, AI-assisted log analysis, and system diagnostics case studies.

---

## Background

This repository reflects a T-shaped engineering approach:

- **Breadth** — end-to-end server validation framework covering environment provisioning，bring-up verification, concurrent stress testing, optional power-cycle iteration, AI-assisted log analysis and report generation across multiple components(E.g., CPU, Memory, NIC, USB, Drive, PCIe).

- **Depth** — NIC driver-level/register-level diagnostics, NIC subsystem architecture evolution, and complex cross-domain problem solving, documented as engineering case studies.

-----

# Repository Structure

## ai-assisted-system-validation-framework/

A Python-native, modular validation framework for server bring-up and stress validation workflows. Features LLM-based log analysis and RCA with rule-based fallback.

→ See architecture, usage, and AI analysis examples from [README.md](./ai-assisted-system-validation-framework/README.md).

> Note: The implementation of this framework is maintained separately in a private repository.

---

## system-diagnostics/

### Low-level Diagnostics & Features

- [NIC Diagnostics Beyond Standard Driver Paths](./system-diagnostics/nic-diagnostics-beyond-standard-driver-paths.md)
- [NIC Silent Failure Observability via Netlink and Devlink](./system-diagnostics/nic-silent-failure-netlink-devlink-observability.md)

---

### Subsystem Architecture Evolution

- [NIC Diagnostic Subsystem Evolution](./system-diagnostics/nic-diagnostic-subsystem-evolution.md)

---

### Complex Cross-domain Problem Solving


---

# License

MIT License