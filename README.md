# Fake Product Detection via Blockchain 🛡️🔗

A decentralized, anti-counterfeiting supply chain solution. This platform bridges a traditional Django web architecture with an immutable Ethereum ledger (Ganache), allowing manufacturers to securely lock product authenticity and empowering consumers to verify items instantly via dynamic QR codes.

## 🌟 Key Features

* **True Web3 Hybrid Architecture:** Utilizes an off-chain database (SQLite) for heavy media storage and an on-chain Ethereum smart contract for immutable cryptographic hashes.
* **Instant Dual-Verification:** Consumers scan a dynamic QR code to query the system in real-time. The custom **Dual-Ledger Verification Algorithm (DLVA)** cross-references the local database against the blockchain to verify if the product is Genuine, Tampered, or Fake.
* **Tamper-Proof Design:** Even if the central metadata database is compromised by a cyber attack, the system detects tampered data by pulling the unhackable "True Hash" directly from the blockchain.
* **Interactive Threat Simulation:** Includes a built-in "Scammer Dashboard" to actively demonstrate the system's resilience against local database breaches during live demonstrations.
* **One-Click Restoration:** Administrators can instantly repair compromised local database entries by downloading the original, immutable state directly from the Ethereum ledger.

## 🧠 Core Technologies & Algorithms

* **SHA-256 (Secure Hash Algorithm):** Converts product metadata (ID, Brand, Timestamp) into a fixed 256-bit digital fingerprint, ensuring collision resistance and preventing reverse-engineering.
* **Smart Contracts (Solidity):** Acts as the decentralized "Truth Source." The contract securely manages the cryptographic signatures and strictly controls write-access via authorized Admin wallet addresses.
* **Web3.py Middleware:** Serves as the crucial RPC bridge, allowing the Python backend to securely sign transactions and read/write data to the Ganache network.

## 🛠️ Technology Stack

* **Language:** Python 3.11.x, Solidity (^0.8.0)
* **Framework:** Django
* **Blockchain Environment:** Ganache (Local RPC)
* **Middleware:** `web3.py`, `py-solc-x`
* **Databases:** SQLite (Off-Chain Storage)
* **Frontend:** HTML5, CSS3, Bootstrap, Javascript

## 🚀 Installation & Setup

Follow these steps to run the Web3 application locally.

### 1. Prerequisites
* [Python 3.x](https://www.python.org/downloads/)
* [Ganache Desktop Application](https://trufflesuite.com/ganache/)

### 2. Environment Setup
Clone the repository and install the required dependencies:
```bash
git clone [https://github.com/puneethrajg/fake-product-detection-via-blockchain.git]
cd fake-product-detection-via-blockchain

# Create and activate a virtual environment
python -m venv myenv
source myenv/bin/activate  # On Windows: myenv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Blockchain Deployment
1. Open **Ganache** and start a new workspace (ensure it's running on `http://127.0.0.1:7545`).
2. Run the deployment script to compile the Solidity contract and deploy it to the local network:
```bash
python deploy.py
```
*(Note: This will generate a `blockchain_config.json` file containing your Contract Address and ABI).*

### 4. Database Initialization
Apply the Django migrations to set up the off-chain application database:
```bash
python manage.py makemigrations
python manage.py migrate
```

### 5. Run the Application
Start the Django development server:
```bash
python manage.py runserver
```
Navigate to `http://127.0.0.1:8000` in your web browser.

## 🧪 Demonstration Flow

1. **The Registration:** Log in as Admin and register a new product. Watch the Ganache UI to see the transaction instantly mined into a block. A unique QR code is generated.
2. **The Happy Path:** Scan the generated QR code to trigger the DLVA and see the "Product is Authentic" screen.
3. **The Cyber Attack:** Navigate to the Scammer Dashboard and execute the tamper script to maliciously alter the off-chain SQLite database.
4. **The Catch:** Scan the exact same QR code again. The DLVA will catch the mismatch between the hacked local database and the immutable Ganache ledger, displaying the "WARNING: Security Compromise Detected" screen.
5. **The Restoration:** As an Admin, trigger the reset function to pull the true hash back down from the Ethereum network and repair the local database.

## 📜 License

Copyright (c) 2026 Puneeth Raj Gorigam

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

