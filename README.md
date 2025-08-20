# Haiti Telemedicine — Blockchain MVP
**Encrypted off-chain storage (Iagon) + on-chain integrity anchors (Cardano / CIP-83).**  
**Key rule:** *No PHI (personally identifiable health data) ever goes on-chain.*

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
flowchart LR
  A[Tablet capture: JSON, images, audio] --> B[Encrypt & bundle: ZIP + manifest.json (SHA-256)]
  B --> C{Connectivity available?}
  C -- "No" --> B
  C -- "Yes" --> D[Iagon upload: sharded & encrypted]
  D -->|file_id| E[Cardano anchor: CIP-83 encrypted metadata]
  E --> F[Audit & verify: hash match + restore drill]
