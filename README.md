# Haiti Telemedicine — Blockchain MVP
**Encrypted off-chain storage (Iagon) + on-chain integrity anchors (Cardano / CIP-83).**  
**Key rule:** *No PHI (personally identifiable health data) ever goes on-chain.*

This project integrates with the Midnight Network.

---

## Background

Haiti continues to face some of the most severe health disparities in the Western Hemisphere. Rural communities are especially affected due to a combination of systemic challenges: a critical shortage of healthcare professionals (with more than **85% of Haitian medical graduates emigrating**), fragile infrastructure, and limited access to consistent medical services.

The problem is not only medical—it is also infrastructural and social. Persistent poverty, low health literacy, and a deep digital divide constrain access to innovation and care. Current conditions include:
- **60% of Haitians live below $3.65/day** (World Bank, 2023)
- **>40% of youth (15–24) are neither in school, training, nor employment** (UNDP)
- **<2% of schools have functional computer labs** and **rural internet access is <10%** (IHSI)

In response, the **Haitian Resource Development Foundation (HRDF)**—a 501(c)(3) nonprofit established in 1987—launched a telemedicine initiative in **Aquin**, a rural commune in Haiti’s southern peninsula. The pilot began on **May 19, 2025**, and operates across **five healthcare sites**: the Aquin Community Hospital (hub) and four rural satellite clinics. Phase I includes deployment of **Starlink internet**, **solar energy**, and computers, alongside training for frontline staff.

A key differentiator of the initiative is that it is **people-first**, not technology-first. Telemedicine is treated as a tool for dignity and equitable care, and is paired with an intentional sociological research-action approach that studies trust, cultural adaptation, and adoption dynamics.

### Research-driven design

At the center of the initiative is a guiding research question:

> **How do rural populations transition from traditional and empirical medicine to trusting and adopting modern telehealth technologies?**

The project follows an **action research** approach inspired by Kurt Lewin’s iterative cycle (observe → plan → act → evaluate), ensuring the model stays responsive to real community perceptions and barriers as adoption evolves.

### FIU collaboration

**Florida International University (FIU)**—the **fifth-largest university in the United States**—is collaborating on the academic and research components, including support from the **Robert Stempel College of Public Health & Social Work**. The collaboration focuses on sociological research design, ethical alignment (including IRB pathways where applicable), and co-authoring a scientific publication documenting rural health transitions and outcomes. The **State University of Haiti** contributes local academic support in survey design, cultural alignment, and field methodology.

### Why a blockchain MVP here

In low-connectivity environments, maintaining **privacy**, **data integrity**, and **trust** across clinics, institutions, and donors is difficult. This repository focuses on a practical building block: a privacy-preserving pipeline that keeps health data off-chain while still providing tamper-evident verification for audits, research traceability, and institutional accountability.

---

## 1) What this is 

In clinics with spotty internet, staff still need to collect visit data, keep it private, and prove later that nothing was altered.

This MVP lets teams:
- **Work offline** on tablets/phones.
- **Encrypt and store** visit bundles safely in **Iagon**’s decentralized network.
- **Stamp a tiny, private receipt** on the **Cardano** blockchain (an “anchor”) so anyone can verify the data wasn’t tampered with—without seeing private details.

**Why it matters:** Patients keep their privacy. Clinics get an audit trail. Donors and institutions get verifiable integrity.

---

## 2) Who this is for

- **Clinicians & coordinators** – a simple, step-by-step routine (capture → encrypt → upload → anchor).
- **IT/engineers** – scripts, APIs, and wallet tooling to automate the pipeline.
- **Partners & sponsors** – privacy-first architecture with verifiable integrity.

---

## 3) Key principles

- **Privacy first**: PHI stays off-chain. Only anonymous IDs, hashes, sizes, timestamps are anchored.
- **Offline-first**: everything works without internet; syncs when possible.
- **Tamper-evident**: each record’s cryptographic **hash** is anchored on Cardano.
- **Simplicity**: small scripts + a one-page SOP for field use.

---

## 4) How it works (at a glance)

```mermaid
flowchart LR;
  A["Tablet capture: JSON, images, audio"] --> B["Encrypt & bundle: ZIP + manifest.json (SHA-256)"];
  B --> C{"Connectivity available?"};
  C -->|No| B;
  C -->|Yes| D["Iagon upload: sharded & encrypted"];
  D -->|file_id| E["Cardano anchor: CIP-83 encrypted metadata"];
  E --> F["Audit & verify: hash match + restore drill"];
