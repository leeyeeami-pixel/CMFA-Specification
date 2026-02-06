# CMFA-3000 — Common Fabric Packet Header
**Release Candidate Draft RC-0.1**  
Status: Normative Core Specification  
Issued by: CMFA Working Draft Group (CMFA-WDG)

---

## 1. Scope

This specification defines the mandatory packet header format used by
all communication across a CMFA-compliant fabric.

CMFA-3000 applies to:

- All Bricks (Compute, GPU, Memory, Storage, Power, Switch)
- All intra-fabric traffic (data, control, reflex, emergency)
- All CMFA switching/routing behavior (CMFA-3002 dependent)

This document is the foundational “wire protocol” of CMFA.

---

## 2. Design Principles

The CMFA Packet Header MUST enable:

- Capability-first addressing (not fixed device IDs)
- Deterministic reflex delivery under load
- Fault-domain isolation boundaries
- Hardware-forwardable minimal parsing
- Vendor-independent interoperability

CMFA packets MUST remain valid across:

- Single chassis fabrics
- Multi-chassis modular clusters
- Future optical or coherent transports

---

## 3. Packet Overview

All CMFA traffic is carried in fixed-format frames:


