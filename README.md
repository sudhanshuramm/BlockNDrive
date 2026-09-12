# 🔐 BlockNDrive

### Decentralized AI-Assisted Document Vault

BlockNDrive is a Web3 document vault designed to give users greater control, privacy, and verifiability over their digital documents.

Instead of relying entirely on a centralized cloud provider, BlockNDrive combines **client-side encryption, decentralized storage, blockchain verification, wallet-based identity, access control, and AI-assisted document risk analysis**.

> **Encrypt → Analyze → Store → Verify → Access**

---

## 🚀 What Problem Does BlockNDrive Solve?

Traditional document storage platforms require users to trust a centralized organization with their documents.

This creates several problems:

* 🔒 Users have limited control over their sensitive documents
* 🏢 Centralized storage creates a single point of failure
* 🔑 Access control is controlled by the storage provider
* 📄 It can be difficult to independently verify document integrity
* 🤖 Sensitive documents are often stored without intelligent risk classification
* 🔍 Users may not know whether a document contains highly sensitive information

BlockNDrive explores a decentralized approach where the user's wallet becomes their Web3 identity, documents are encrypted before storage, content is stored using IPFS/Filecoin infrastructure, and document metadata and integrity information can be registered on-chain.

---

# ✨ Key Features

### 🔐 Client-Side Encryption

Documents are encrypted in the browser before being uploaded.

BlockNDrive uses **AES-256/GCM-based encryption** for document protection.

The objective is to ensure that the original document is not simply uploaded as plaintext.

---

### 🦊 MetaMask Wallet Identity

Users can connect their MetaMask wallet and use their Ethereum address as their application identity.

The current application is designed around the **Ethereum Sepolia testnet**.

---

### ⛓️ Blockchain Document Registry

Document information can be associated with a deployed smart contract on Sepolia.

The blockchain layer provides a verifiable registry for document-related information such as:

* Document ID
* Owner address
* File CID
* File hash
* Metadata
* Risk score
* Timestamp
* Document status

This allows document integrity and ownership information to be independently verified.

---

### 📦 Lighthouse + IPFS/Filecoin Storage

Encrypted document data is uploaded through the Lighthouse Web3 storage SDK.

The storage layer uses:

* **Lighthouse**
* **IPFS**
* **Filecoin**

The application stores the resulting CID and uses it for decentralized content addressing.

---

### 🤖 AI-Assisted Document Analysis

BlockNDrive includes a document analysis service using Google's Gemini API when configured.

The system can analyze document information and classify files based on potential sensitivity.

Examples include:

* Cryptographic keys
* Seed phrases
* Wallet credentials
* API secrets
* Identity documents
* Financial documents
* Legal documents
* Academic records

The analysis produces information such as:

```text
Classification
Category
Sensitivity
Risk Score
Risk Level
Detected Entities
Compliance Flags
Reasoning
```

---

### 🔗 Chainlink CRE Integration

BlockNDrive is designed around **Chainlink Runtime Environment (CRE)** concepts for document risk analysis and metadata workflows.

The application includes a Chainlink CRE metrics/architecture interface and associates document analysis with CRE workflow information.

The project explores how verifiable off-chain computation can be incorporated into a decentralized document workflow.

---

### 🔑 Lit Protocol Access Control

BlockNDrive incorporates Lit Protocol-based access-control concepts for controlling access to encrypted document content.

The application supports Lit-related access payloads and shareable access links.

The intended model is:

```text
User Wallet
     ↓
Ownership Verification
     ↓
Lit Access Conditions
     ↓
Encrypted Document Access
```

---

### ☁️ Firebase Persistence

Firebase/Firestore is used as an application-side persistence layer for document records and activity information.

This allows the interface to maintain useful application metadata while blockchain and decentralized storage handle the Web3 portions of the system.

---

### 🗑️ Document Archive & Recovery

BlockNDrive includes document lifecycle management.

Users can:

* Archive documents
* Restore archived documents
* Permanently delete documents
* Perform batch archive operations
* Perform batch restore operations
* Perform batch permanent deletion

The application also maintains document activity information.

---

# 🏗️ Architecture

The high-level architecture is:

```text
                         ┌─────────────────────┐
                         │       User          │
                         │     Web Browser     │
                         └──────────┬──────────┘
                                    │
                                    ▼
                         ┌─────────────────────┐
                         │   BlockNDrive UI    │
                         │   React + TypeScript│
                         └──────────┬──────────┘
                                    │
                    ┌───────────────┼────────────────┐
                    │               │                │
                    ▼               ▼                ▼
             ┌───────────┐   ┌────────────┐   ┌─────────────┐
             │ MetaMask  │   │ AES-256    │   │ Gemini AI   │
             │   Wallet  │   │ Encryption │   │ Risk        │
             └─────┬─────┘   └─────┬──────┘   │ Analysis    │
                   │               │          └──────┬──────┘
                   │               │                 │
                   │               ▼                 ▼
                   │        ┌────────────────────────────┐
                   │        │       BlockNDrive API      │
                   │        │      Express + Node.js      │
                   │        └─────────────┬──────────────┘
                   │                      │
          ┌────────┴─────────┐            │
          │                  │            │
          ▼                  ▼            ▼
   ┌──────────────┐   ┌──────────────┐  ┌───────────────┐
   │ Ethereum     │   │ Lighthouse   │  │ Firebase      │
   │ Sepolia      │   │ IPFS/Filecoin │  │ Firestore     │
   │ Smart        │   │              │  │               │
   │ Contract     │   │              │  │               │
   └──────────────┘   └──────────────┘  └───────────────┘
          │
          ▼
   ┌──────────────┐
   │ Lit Protocol │
   │ Access       │
   │ Control      │
   └──────────────┘
```

---

# 🔄 Document Upload Flow

The intended document workflow is:

```text
1. User selects document
            ↓
2. Document processed in browser
            ↓
3. AES encryption
            ↓
4. Document metadata generated
            ↓
5. AI / CRE risk analysis
            ↓
6. Encrypted document uploaded
            ↓
7. Lighthouse stores content using IPFS/Filecoin
            ↓
8. CID + hash + metadata generated
            ↓
9. Document information registered on Sepolia
            ↓
10. Firestore stores application metadata
            ↓
11. User sees document in My Documents
```

---

# 🧠 Document Risk Analysis

BlockNDrive uses document characteristics and content samples to determine potential sensitivity.

Example risk categories include:

| Document Type             | Example Risk |
| ------------------------- | -----------: |
| Private key / seed phrase |  🔴 Critical |
| API credentials           |  🔴 Critical |
| Identity documents        |      🟠 High |
| Financial records         |    🟡 Medium |
| Legal agreements          |    🟡 Medium |
| Academic records          |       🟢 Low |
| General documents         |       🟢 Low |

The risk score is represented on a `0–100` scale.

Example:

```text
0 ─────────────── 49    LOW
50 ───────────── 79    MEDIUM
80 ───────────── 100   HIGH
```

---

# 🧩 Technology Stack

## Frontend

* React
* TypeScript
* Vite
* Tailwind CSS
* Lucide React
* Motion

## Web3

* Ethereum
* Sepolia Testnet
* Solidity Smart Contract
* ethers.js
* MetaMask

## Decentralized Storage

* Lighthouse
* IPFS
* Filecoin

## Privacy & Security

* AES-256/GCM encryption
* Lit Protocol
* Wallet-based identity
* Content hashes

## AI

* Google Gemini API
* Chainlink CRE workflow concepts

## Backend

* Node.js
* Express
* TypeScript
* dotenv
* esbuild

## Database / Persistence

* Firebase
* Firestore

---

# 📁 Project Structure

```text
BlockNDrive/
│
├── public/
│
├── src/
│   ├── components/
│   │   ├── Navbar
│   │   ├── UploadSection
│   │   ├── DocumentList
│   │   ├── DocumentDetailsModal
│   │   ├── ChainlinkCREModal
│   │   ├── WalletConnectModal
│   │   └── ...
│   │
│   ├── hooks/
│   │
│   ├── lib/
│   │   └── firebase
│   │
│   ├── services/
│   │   ├── blockchain
│   │   └── crypto
│   │
│   ├── constants/
│   │
│   ├── App.tsx
│   └── ...
│
├── scripts/
│
├── server.ts
├── package.json
├── vite.config.ts
├── tsconfig.json
├── firestore.rules
├── .env.example
└── metadata.json
```

---

# ⚙️ Getting Started

## 1. Clone the repository

```bash
git clone https://github.com/CryptoMYN/BlockNDrive.git
```

```bash
cd BlockNDrive
```

---

## 2. Install dependencies

The project currently uses npm-compatible package management.

```bash
npm install
```

If you use Bun:

```bash
bun install
```

---

## 3. Configure environment variables

Create a `.env` file:

```env
GEMINI_API_KEY=your_gemini_api_key
LIGHTHOUSE_API_KEY=your_lighthouse_api_key
APP_URL=http://localhost:3000
```

### Important

Never commit `.env` to GitHub.

Do not expose:

* API keys
* Private keys
* Wallet seed phrases
* Firebase secrets
* Authentication credentials

---

# ▶️ Run Locally

Start the development server:

```bash
npm run dev
```

The application will normally be available at:

```text
http://localhost:3000
```

---

# 🏭 Production Build

Build the frontend and backend:

```bash
npm run build
```

Then start the production server:

```bash
npm start
```

---

# 🧪 Development Commands

### Development

```bash
npm run dev
```

### Build

```bash
npm run build
```

### Production

```bash
npm start
```

### Type checking

```bash
npm run lint
```

### Preview Vite build

```bash
npm run preview
```

---

# 🌐 Network

BlockNDrive is currently configured around:

```text
Network: Ethereum Sepolia
Wallet: MetaMask
Storage: Lighthouse / IPFS / Filecoin
```

The application uses a deployed BlockNDrive smart contract on Sepolia.

---

# 🔒 Security Considerations

BlockNDrive is a prototype / hackathon-oriented decentralized application.

It should **not** currently be considered production-ready for storing highly sensitive real-world documents.

Before production deployment, the following should be independently audited and hardened:

* Smart contract security
* Encryption/key-management design
* Lit Protocol access conditions
* API authentication
* Firebase security rules
* Server-side secret handling
* IPFS gateway security
* Document metadata privacy
* AI data handling
* Wallet authentication
* Rate limiting
* File validation
* Malware scanning
* Secure deletion semantics

### Never upload real private keys or seed phrases.

Use testnet accounts and test documents during development.

---

# 🗺️ Roadmap

## Current / Prototype

* [x] React Web3 interface
* [x] MetaMask connection
* [x] Ethereum Sepolia integration
* [x] Document vault UI
* [x] Document metadata
* [x] AES-based encryption workflow
* [x] Lighthouse IPFS/Filecoin integration
* [x] Gemini-assisted document analysis
* [x] Chainlink CRE integration concepts
* [x] Lit Protocol access-control integration
* [x] Firestore persistence
* [x] Document archive and recovery
* [x] Document activity tracking

## Future

* [ ] Production-grade key management
* [ ] Full smart-contract audit
* [ ] Stronger document authentication
* [ ] Fine-grained document sharing
* [ ] Multi-user organization vaults
* [ ] Decentralized identity integration
* [ ] Advanced AI document classification
* [ ] Verifiable CRE workflows
* [ ] Mobile application
* [ ] Mainnet deployment
* [ ] Enterprise document management

---

# 🎯 Why Blockchain?

BlockNDrive does not attempt to put entire documents directly on-chain.

Instead:

```text
Large Document
     │
     ▼
Encrypted Off-Chain Storage
     │
     ▼
IPFS / Filecoin
     │
     ▼
CID + Hash + Metadata
     │
     ▼
Blockchain Registry
```

This approach separates:

**Storage**
from
**Verification**

The blockchain can provide an immutable reference and verification layer without paying the cost of storing large files directly on Ethereum.

---

# 🛡️ Security Model

The core security model can be summarized as:

```text
             USER
              │
              ▼
          MetaMask
              │
              ▼
       Wallet Ownership
              │
              ▼
        AES Encryption
              │
              ▼
      Lighthouse / IPFS
              │
              ▼
       CID + File Hash
              │
              ▼
      Sepolia Smart Contract
              │
              ▼
       Lit Access Control
              │
              ▼
       Authorized Access
```

The system therefore combines:

**Cryptography + Decentralized Storage + Blockchain + AI + Wallet Identity**

---

# 🏆 Project Vision

BlockNDrive aims to explore a new model for personal document storage where users have stronger control over their data and where document integrity can be independently verified.

The long-term vision is a privacy-focused document infrastructure combining:

> **Web3 + AI + Decentralized Storage + Cryptography**

into a single user-controlled document vault.

---

# 📜 License

Add an appropriate open-source license before distributing the project publicly.

For example:

```text
MIT License
```

if that matches your intended project licensing.

---

# 👨‍💻 Project

**BlockNDrive**

A decentralized, AI-assisted document vault built with Web3 technologies.

GitHub:

https://github.com/CryptoMYN/BlockNDrive
