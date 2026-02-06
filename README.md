# CMFA Specification

Welcome to the **CMFA (Composable Modular Fabric Architecture) Specification** repository.

CMFA is a modular, AI-first hardware architecture standard designed for composable, scalable computing systems. This repository contains the official specification, development roadmap, and contribution guidelines.

# ⚡ CMFA Standard Draft Set

This document outlines the current CMFA draft standards for modular, AI-first computing architecture.

---

## [CMFA-3000 — Fabric Packet Header](specs/CMFA-3000_Fabric_Packet_Header.md)

**Description:**  
Defines the base frame and packet header for communication between Bricks over the CMFA Fabric.

**Key Points:**  
- Standardized frame structure  
- Header fields for addressing, type, and length  
- Ensures compatibility across different Fabric implementations  

---

## [CMFA-3002 — Switching & Routing Rules](specs/CMFA-3002_Switching_Routing.md)

**Description:**  
Defines rules for forwarding packets, routing, and handling priorities within the CMFA Fabric.

**Key Points:**  
- Packet forwarding mechanisms  
- TTL (Time-to-Live) handling  
- Priority preemption rules  
- Fault domain definitions for reliability and isolation  

---

## [CMFA-5000 — Brick Classes](specs/CMFA-5000_Brick_Classes.md)

**Description:**  
Defines standard classes for Bricks to ensure interoperability across CMFA systems.

**Key Points:**  
- Power classes (e.g., low, medium, high)  
- Fabric classes (e.g., bandwidth, latency)  
- Thermal classes (cooling requirements)  
- Role classes (Compute, Memory, Storage, Network, I/O)  

---

## [CMFA-5001 — Brick Descriptor & Discovery](specs/CMFA-5001_Brick_Descriptor_Discovery.md)

**Description:**  
Defines how Bricks announce themselves and integrate into the CMFA resource graph.

**Key Points:**  
- Standardized Brick descriptor format  
- Automatic discovery protocol  
- Dynamic registration to the Fabric resource graph  
- Compatibility rules for heterogeneous modules  

---

## ⚡ CMFA Logo / Icon

![CMFA Icon](specs/diagrams/cmfa_icon.png)  

*Note: Replace `cmfa_icon.png` with your official CMFA logo or desired icon.*


## 🚀 Join the CMFA Community!

CMFA is an open vision for the next generation of modular computing. Got ideas for new modules, Fabric improvements, or cool use cases? Jump in and help us make CMFA better for everyone!


## 📄 Contents

- [CMFA Whitepaper v0.1.1](CMFA_Whitepaper_v0.1.1.md) — Full specification in Markdown
- [Roadmap](ROADMAP.md) — Project development plan and future milestones
- [Contribution Guidelines](CONTRIBUTING.md) — How to contribute to CMFA
- [Diagrams](specs/diagrams/) — Architecture and module diagrams (placeholders)

## 📌 Features

- Modular Compute, Memory, Storage, Network, and I/O Bricks  
- High-speed composable Fabric interconnect  
- Hot-plug support and dynamic module configuration  
- Designed for AI workloads, HPC, cloud-edge, and custom PCs  

## 🚀 Getting Started

1. Clone the repository:

```bash
git clone https://github.com/leeyeeami-pixel/CMFA-Specification.git
cd CMFA-Specification
