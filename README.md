# IAN

# Burnable BEP20 Token

### 🛡 Secure and Burnable BEP20 Token on Binance Smart Chain

This repository contains the **Burnable BEP20 token** smart contract, allowing token holders to burn tokens from their balance or through an approved spender. This is based on the Binance Smart Chain (BSC) **BEP20 standard** with additional security and transparency features.

## 📜 **Contract Details**
- **Contract Name:** BurnableBEP20
- **Token Standard:** BEP20
- **Blockchain:** Binance Smart Chain (BSC)
- **Compiler Version:** `0.8.x`
- **Verified Contract:** ✅

### 🔍 **View on BscScan**
**Contract Address:**  
`0x07d5bf841beb877c9bE550B79cb0d49e4e091Dec`  
🔗 [BscScan Explorer](https://bscscan.com/address/0x07d5bf841beb877c9bE550B79cb0d49e4e091Dec)

---

## 🔥 **Features**
✅ **Token Burning** - Users can permanently destroy tokens to reduce total supply.  
✅ **Ownership Control** - The contract owner can manage access and permissions.  
✅ **Security Audited** - Ensures protection against vulnerabilities.  
✅ **Service Fee System** - Integrated fee system with a `ServicePayer` contract.  
✅ **Minting Function** - The owner can create additional supply when needed.  

---

## 📖 **Contract Code**
The contract source code is located in `/contracts/BurnableBEP20.sol`.

### **🛠 Deployment Details**
```solidity
contract BurnableBEP20 is BEP20Burnable, ServicePayer {
    constructor(
        string memory name_,
        string memory symbol_,
        uint8 decimals_,
        uint256 initialBalance_,
        address payable feeReceiver_
    ) payable BEP20(name_, symbol_) ServicePayer(feeReceiver_, "BurnableBEP20") {
        require(initialBalance_ > 0, "BurnableBEP20: supply cannot be zero");

        _setupDecimals(decimals_);
        _mint(_msgSender(), initialBalance_);
    }
}

🔬 Testing

To run the tests, use Hardhat:

npm install
npx hardhat test

Example test case in /tests/test_burnable.js:

const { expect } = require("chai");

describe("BurnableBEP20 Token", function () {
    let owner, user, token;

    beforeEach(async function () {
        const BurnableBEP20 = await ethers.getContractFactory("BurnableBEP20");
        token = await BurnableBEP20.deploy("BurnableToken", "BTK", 18, 1000000, owner.address);
        [owner, user] = await ethers.getSigners();
    });

    it("Should allow token burning", async function () {
        await token.connect(owner).burn(500);
        expect(await token.totalSupply()).to.equal(999500);
    });
});

🛠 Deployment Instructions

To deploy the contract using Hardhat, run:

npx hardhat run scripts/deploy.js --network bsc

Modify /scripts/deploy.js to include:

async function main() {
    const BurnableBEP20 = await ethers.getContractFactory("BurnableBEP20");
    const token = await BurnableBEP20.deploy("BurnableToken", "BTK", 18, 1000000, "0xFEE_RECEIVER");

    console.log("BurnableBEP20 deployed to:", token.address);
}

📑 Audit Report

This contract has undergone a security audit. You can find the audit details in audits/security-audit.pdf.

🔒 Security Measures
	•	Prevents overflows/underflows with Solidity 0.8.x
	•	Blacklist protection can be implemented if needed.
	•	Ownership can be renounced to decentralize control.

Find more details in docs/security.md.

📜 License

This project is licensed under the MIT License.

---