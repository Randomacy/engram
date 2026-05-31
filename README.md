# Engram

**Open biosignal dataset preservation and sharing, built on Sia.**

Engram is a client-side React application for preserving and sharing scientific EEG datasets. Researchers upload their recordings, receive a content-addressed object key, and cite it in published papers. No data passes through a server. No institution controls access.

Built on the [Sia Storage SDK](https://github.com/SiaFoundation/web) and [indexd](https://github.com/SiaFoundation/indexd) as part of a [Sia Foundation Small Grant](https://forum.sia.tech/c/grants/proposed/).

---

## Why Engram

EEG datasets are routinely lost. Lab servers fail. Institutional accounts lapse. GitHub cannot store files that large, so researchers publish only the processed output — the raw recordings, the only part useful for replication, are never shared.

Engram stores raw biosignal data on the Sia decentralised storage network. Every dataset is identified by a cryptographic content hash. The researcher holds the keys. No platform can make a unilateral deletion decision.

---

## How it works

1. **Sign in with ORCID** — the persistent researcher identifier used across academic publishing
2. **Upload an EEG file** — EDF, BDF, or GDF format
3. **Anonymisation** — patient name, date of birth, and recording date are zeroed from the file header client-side before upload. No raw subject data leaves the browser
4. **Storage** — the anonymised file is uploaded directly to Sia via `@siafoundation/indexd-js`. No data transits a server
5. **Citation** — a content-addressed object key is returned. Cite it in papers. The reference is permanently verifiable
6. **Discovery** — anyone can search and retrieve datasets by object key with no account required
7. **Retraction** — researchers can remove a dataset from the discovery index at any time. The object key is deactivated immediately

---

## Stack

- **Frontend:** React, TypeScript
- **Storage:** [`@siafoundation/indexd-js`](https://github.com/SiaFoundation/web/tree/main/packages/indexd-js) via the hosted [sia.storage](https://sia.storage) indexer
- **EEG parsing:** client-side binary header manipulation (EDF/BDF format)
- **Identity:** ORCID OAuth 2.0 (read-only public profile)
- **Key management:** BIP-39 recovery phrase → Sia App Key, stored in browser secure storage

---

## Getting started

> **Note:** Active development begins Month 1 of the grant period. Build instructions will be updated as the codebase is populated.

```bash
git clone https://github.com/Randomacy/engram
cd engram
npm install
npm run dev
```

Prerequisites:
- Node.js 18+
- A Sia account via [sia.storage](https://sia.storage) or a self-hosted indexd instance

---

## Roadmap

**Month 1**
- [ ] ORCID sign-in and onboarding flow
- [ ] BIP-39 recovery phrase generation and App Key derivation
- [ ] Client-side EDF/BDF header anonymisation
- [ ] Dataset upload pipeline with packed metadata objects
- [ ] Researcher dashboard with object keys and pin state

**Month 2**
- [ ] Dataset retraction
- [ ] Public discovery interface — search by modality, task, equipment, license
- [ ] Self-population with MIC's openly-licensed imagined speech EEG corpus
- [ ] Documentation and self-hosting guide
- [ ] Public open-source release

---

## Supported formats

| Format | Description |
|---|---|
| EDF | European Data Format — standard for clinical EEG |
| BDF | BioSemi Data Format — 24-bit extension of EDF |
| GDF | General Data Format — used in BCI research |

EMG, fNIRS, and MEG support planned post-grant.

---

## License

MIT — see [LICENSE](LICENSE)

---

## About

Engram is built by [Jackie Tan Yen](https://www.linkedin.com/in/jackietanyen/) as part of research to build neural intent decoders for people with disabilities.

Supported by a Sia Foundation Grant (hopefully).
