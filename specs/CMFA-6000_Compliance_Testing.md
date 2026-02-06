# CMFA-6000 — Compliance & Interoperability Test Suite
**Release Candidate Draft RC-0.1**  
Status: Normative Certification Specification  
Issued by: CMFA Working Draft Group (CMFA-WDG)

---

## 1. Scope

This specification defines mandatory compliance testing requirements
for CMFA implementations.

CMFA-6000 ensures that Bricks from different vendors
can interoperate in the same fabric.

It defines:

- Required conformance behaviors
- Minimal certification test cases
- Interoperability validation rules
- Safety reflex enforcement checks

---

## 2. Compliance Levels

CMFA defines three compliance tiers:

| Level | Name | Meaning |
|------|------|---------|
| L1 | Packet Compliance | Header + routing validity |
| L2 | Brick Compliance | Lifecycle + discovery |
| L3 | Reflex Safety Compliance | Emergency + quarantine |

A vendor MAY claim compliance only at levels fully passed.

---

## 3. Mandatory Test Categories

---

### 3.1 CMFA-3000 Packet Tests

All devices MUST pass:

- Magic validation
- Version handling
- CRC64 enforcement
- TTL decrement correctness
- Priority preemption marking

**Test Case P-01: Invalid CRC Drop**

- Inject corrupted header
- Device MUST drop packet

---

### 3.2 Capability Routing Tests (CMFA-3002)

**Test Case R-01: Capability Forwarding**

- Inject packet targeting GPU capability
- Switch MUST forward toward GPU Brick

**Test Case R-02: TTL Loop Prevention**

- Inject packet with TTL=1
- Packet MUST be dropped after hop

---

### 3.3 Brick Discovery Tests (CMFA-5001)

**Test Case D-01: Descriptor Availability**

- Brick inserted
- Descriptor MUST be readable within 100ms

**Test Case D-02: Capability Advertisement**

- Brick MUST register capability codes correctly

---

### 3.4 Lifecycle Tests (CMFA-5000)

**Test Case L-01: Hot Removal Handling**

- Remove Brick mid-traffic
- Fabric MUST reroute capability pool

**Test Case L-02: Quarantine Compliance**

- Mark Brick FaultDomain=0xFF
- Brick MUST reject workload packets

---

### 3.5 Reflex Safety Tests (CMFA-4000)

**Test Case S-01: Emergency Kill**

- Broadcast Priority=0xF kill packet
- All Power + Compute Bricks MUST halt workloads

**Test Case S-02: Reflex Preemption**

- Saturate fabric with IO traffic
- Reflex event MUST deliver within bounded latency

---

## 4. Certification Outputs

A compliant vendor MUST publish:

- Brick Descriptor File
- Capability Code List
- Compliance Tier Achieved
- Test Log Signature

---

## 5. Community Compliance Harness

CMFA encourages open-source test harness development:

- FPGA-based packet injectors
- Switch validation simulators
- Brick hot-plug emulators

Reference harness repository is under discussion.

---

## 6. Open Topics (RC Phase)

- Formal latency bounds for reflex delivery
- Cryptographic compliance signing
- Multi-vendor certification authority model

---

