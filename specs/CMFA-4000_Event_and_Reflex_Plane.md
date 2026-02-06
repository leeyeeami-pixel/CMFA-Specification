# CMFA-4000 — Event & Reflex Plane Specification
**Working Draft WD-0.1**  
Issued by: CMFA Working Draft Group (CMFA-WDG)

---

## 1. Scope

This specification defines the CMFA Event & Reflex Plane, including:

- Mandatory event classes and codes
- Reflex-priority delivery semantics
- Brick heartbeat and health monitoring
- Fault isolation triggers and emergency propagation
- System-wide reflex behavior independent of OS/software

CMFA-4000 applies to:

- All CMFA bricks
- Fabric switches forwarding reflex events
- Control bricks coordinating safety responses
- Power bricks enforcing shutdown and isolation

---

## 2. Design Goals

The Event & Reflex Plane MUST provide:

- Hardware-native safety responses
- Deterministic low-latency event delivery
- Autonomous fault containment
- Hot-plug awareness and lifecycle tracking
- Emergency shutdown propagation independent of workload traffic

CMFA systems MUST behave as:

> A reflexive organism, not a passive motherboard.

---

## 3. Event Plane Fundamentals

### 3.1 Event Packet Type

All reflex events MUST use CMFA-3000:

- Packet Type = `0x1` (Reflex Event)
- Priority MUST be ≥ `0x8`

Reflex events MUST preempt normal traffic.

---

### 3.2 Event Header Fields

Reflex events MUST populate:

- Event Class (8 bits)
- Event Code (8 bits)
- Fault Domain (8 bits)
- Priority (4 bits)

---

## 4. Mandatory Event Classes

CMFA defines standard Event Classes:

| Class ID | Name | Description |
|---------|------|-------------|
| 0x01 | Presence Events | Brick insertion/removal |
| 0x02 | Thermal Events | Temperature + cooling reflex |
| 0x03 | Power Events | Power budget, cutoff, surge |
| 0x04 | Fabric Health Events | Link errors, congestion |
| 0x05 | Fault Isolation Events | Quarantine triggers |
| 0x06 | Emergency Events | Global shutdown, kill |

---

## 5. Mandatory Event Codes

### 5.1 Presence Events (Class 0x01)

| Code | Meaning |
|------|---------|
| 0x01 | Brick Inserted |
| 0x02 | Brick Removed |
| 0x03 | Descriptor Updated |
| 0x04 | Capability Change Detected |

---

### 5.2 Thermal Events (Class 0x02)

| Code | Meaning |
|------|---------|
| 0x01 | Thermal Warning |
| 0x02 | Thermal Throttle Required |
| 0x03 | Thermal Critical |
| 0xFF | Emergency Thermal Shutdown |

---

### 5.3 Power Events (Class 0x03)

| Code | Meaning |
|------|---------|
| 0x01 | Power Budget Negotiation Required |
| 0x02 | Power Limit Enforced |
| 0x03 | Surge Detected |
| 0xFF | Emergency Power Cutoff |

---

### 5.4 Fabric Health Events (Class 0x04)

| Code | Meaning |
|------|---------|
| 0x01 | Link Degraded |
| 0x02 | Link Down |
| 0x03 | Congestion Alert |
| 0x04 | Loop Detection Trigger |

---

### 5.5 Fault Isolation Events (Class 0x05)

| Code | Meaning |
|------|---------|
| 0x01 | Fault Suspected |
| 0x02 | Quarantine Requested |
| 0x03 | Brick Isolated |
| 0x04 | Recovery Attempt |

---

### 5.6 Emergency Events (Class 0x06)

| Code | Meaning |
|------|---------|
| 0x01 | Emergency Stop Broadcast |
| 0x02 | System Kill Trigger |
| 0xFF | Global Shutdown Confirmed |

---

## 6. Reflex Priority Rules

Reflex events MUST obey:

| Priority | Reflex Level |
|---------|-------------|
| 0x8–0xA | Normal System Events |
| 0xB–0xD | Fault and Isolation Reflex |
| 0xE     | Critical Thermal/Power Reflex |
| 0xF     | Emergency Kill |

Priority 0xF MUST override all other fabric traffic.

---

## 7. Brick Heartbeat & Health Monitoring

### 7.1 Heartbeat Requirement

All bricks MUST emit a heartbeat event at a fixed interval:

- Default: every 250ms (configurable)

Heartbeat packet:

- Type = Reflex Event
- Class = Fabric Health (0x04)
- Code = 0x00 (Heartbeat)

---

### 7.2 Heartbeat Loss

If heartbeat is absent beyond threshold:

- Brick MUST be marked unhealthy
- Isolation trigger SHOULD occur

---

## 8. Fault Isolation Reflex

### 8.1 Isolation Trigger Sequence

When a fault event occurs:

1. Fault Suspected Event emitted
2. Control Brick assigns Fault Domain quarantine
3. Switches reroute traffic (CMFA-3002)
4. Power Brick may cut power if required
5. Brick enters Quarantine State

---

### 8.2 Quarantine Enforcement

A quarantined brick MUST:

- Reject normal workload packets
- Accept only diagnostic/control packets
- Maintain descriptor accessibility

---

## 9. Emergency Kill Propagation

### 9.1 Emergency Kill Packet

Emergency shutdown MUST use:

- Class = Emergency (0x06)
- Code = System Kill Trigger (0x02)
- Priority = 0xF

---

### 9.2 Mandatory Response

Upon receiving Emergency Kill:

- Switches MUST forward immediately
- Power Bricks MUST cut power to affected domains
- Compute/GPU bricks MUST halt workload execution

Emergency Kill MUST function even if:

- OS is unresponsive
- Workload traffic is saturated
- Partial fabric failure exists

---

## 10. Community Implementation Notes

### Example: Overheat Reflex

A GPU Brick detects critical temperature:

- Emits Thermal Critical (0x02/0x03)
- Priority escalates to 0xE
- Control Brick throttles workload routing
- If temperature continues rising:
  - Emergency Thermal Shutdown (0x02/0xFF)
  - Isolation + Power Cutoff

This occurs without OS involvement.

---

## 11. Compliance Requirements

All CMFA bricks MUST support:

- Mandatory event classes (0x01–0x06)
- Heartbeat emission + monitoring
- Emergency Kill reception + forwarding
- Fault isolation participation

Switches MUST support:

- Reflex preemption queues
- Emergency broadcast propagation

---

## 12. Open Questions (WD Phase)

Topics under active discussion:

- Secure event authentication
- Multi-level recovery policies
- Hardware watchdog integration
- Reflex event compression for dense fabrics

Community feedback is encouraged via GitHub Issues.

---

