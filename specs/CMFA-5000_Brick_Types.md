# CMFA-5000 — Brick Type Classification & Lifecycle
**Release Candidate Draft RC-0.1**  
Status: Normative Core Specification  
Issued by: CMFA Working Draft Group (CMFA-WDG)

---

## 1. Scope

This specification defines the mandatory Brick classification system
for all CMFA-compliant modular hardware units.

CMFA Bricks are the fundamental compute organs of a CMFA system.

CMFA-5000 defines:

- Brick class taxonomy
- Required capabilities per class
- Brick lifecycle state machine
- Hot-plug participation rules
- Minimal compliance behavior

This specification applies to all hardware modules attached to a CMFA fabric.

---

## 2. Brick Definition

A **Brick** is a self-contained modular compute or service unit that:

- Attaches to the CMFA fabric via a Fabric Port
- Advertises capabilities (CMFA-5001)
- Communicates exclusively via CMFA packets (CMFA-3000)
- Participates in reflex safety behavior (CMFA-4000)

A Brick is not a PCIe peripheral.

A Brick is a **fabric-native autonomous module**.

---

## 3. Mandatory Brick Properties

All Bricks MUST implement:

| Property | Requirement |
|---------|-------------|
| Brick UUID | Globally unique identity |
| Capability Descriptor | Advertised services |
| Heartbeat Emission | Health monitoring |
| Reflex Event Reception | Emergency response |
| Hot-Plug Awareness | Presence events |
| Fault Domain Compliance | Isolation enforcement |

---

## 4. Standard Brick Classes

CMFA defines the following mandatory Brick Classes.

---

### 4.1 Class 0x01 — Compute Brick

General-purpose CPU execution node.

**Required Capabilities:**

- 0x0001 (General Compute)
- Reflex event handling

**Responsibilities:**

- Execute workloads dispatched by Control Brick
- Provide local scheduling resources
- Support throttling and isolation

---

### 4.2 Class 0x02 — GPU Brick

Accelerator brick optimized for AI and graphics.

**Required Capabilities:**

- 0x0002 (GPU Acceleration)

**Mandatory Reflex Support:**

- Thermal shutdown reflex (CMFA-4000)
- Quarantine compliance

GPU Bricks MUST halt execution on Emergency Kill.

---

### 4.3 Class 0x03 — Memory Brick

Fabric-attached pooled memory module.

**Required Capabilities:**

- 0x0003 (Memory Pool)

Memory Bricks MUST provide:

- Low-latency caching service
- Optional coherency extensions (future)

Memory Bricks MUST reject traffic if quarantined.

---

### 4.4 Class 0x04 — Storage Brick

Fabric-native storage provider.

**Required Capabilities:**

- 0x0004 (Storage Service)

Storage Bricks MAY implement:

- NVMe-over-CMFA mapping
- Distributed replication

Storage Bricks MUST prioritize reflex packets over IO traffic.

---

### 4.5 Class 0x05 — Switch Brick

Fabric routing and forwarding module.

**Required Capabilities:**

- Capability Forwarding Table support
- Reflex preemption queues

Switch Bricks MUST comply with CMFA-3002 routing rules.

---

### 4.6 Class 0x06 — Power Brick

Power negotiation, enforcement, and emergency cutoff authority.

**Required Capabilities:**

- 0x00FF (Power Control)

Power Bricks MUST implement:

- Emergency Kill enforcement
- Power-domain isolation

Power Bricks are the final safety authority.

---

### 4.7 Class 0x07 — Control Brick

System-level coordinator and policy brain.

**Required Capabilities:**

- Capability Registry Authority
- Routing Seed Distribution
- Quarantine Assignment

Control Bricks MAY run orchestration software,
but reflex safety MUST function without OS dependency.

---

## 5. Brick Lifecycle State Machine

All Bricks MUST implement the following lifecycle:


