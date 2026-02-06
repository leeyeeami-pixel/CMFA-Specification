# CMFA-3002 — Fabric Switching & Routing Rules
**Working Draft WD-0.1**  
Issued by: CMFA Working Draft Group (CMFA-WDG)

---

## 1. Scope

This specification defines mandatory switching and routing behavior
for CMFA fabric interconnects, including:

- Packet forwarding rules
- Capability-based routing semantics
- Priority and reflex preemption
- Loop prevention mechanisms
- Fault-domain containment and reroute
- Minimal requirements for CMFA switches

CMFA-3002 applies to:

- Fabric Switch Bricks
- Control Bricks responsible for routing tables
- All Bricks participating in multi-hop fabrics

---

## 2. Design Goals

CMFA routing MUST provide:

- Capability-first resource access
- Deterministic reflex event delivery
- Fault isolation and containment
- Multi-topology interoperability
- Low-latency intra-chassis transport
- Vendor-independent switching behavior

---

## 3. Supported Fabric Topologies

CMFA fabrics MAY be implemented as:

| Topology | Description |
|---------|-------------|
| Star    | Central switch/control brick hub |
| Mesh    | Multi-path brick-to-brick routing |
| Ring    | Cost-efficient chained fabric |
| Hybrid  | Hierarchical multi-layer fabrics |

Switch behavior MUST remain consistent across all topologies.

---

## 4. Addressing Model

CMFA does not route primarily by fixed device address.

Routing decisions are based on:

- **Destination Capability Code** (CMFA-3000)
- Optional Brick UUID extensions
- Fault Domain boundaries
- Priority class

Routing Key:


