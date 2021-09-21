# **Learn about Casper ecosystem and smart contracts on Casper**


## 1. **Create and deploy a simple, smart contract with cargo casper and cargo test**

Creating a project *casper-contract* with `cargo casper casper-contract` and then installing the necessary toolchain. Then build the project with `make prepare` and `make build-contract`.

![](https://i.imgur.com/EDa4RUm.png)

Finally test the project with `make test`

![](https://i.imgur.com/kD5Vl7T.png)

The final result shows the succesful build and test of a simple smart contract built upon Casper. 

![](https://i.imgur.com/wE8pYcR.png)


## 2. **Complete one of the existing tutorials for writing smart contracts**

I followed the implementation of ERC-20 implementation tutorial because .

### Preparation
Clone the project.

### Implementation
Went through the tutorial and understood the implementation of an ERC-20 token implementation.

![](https://i.imgur.com/yr6If0C.png)

### Testing
Test the project with `make test`

![](https://i.imgur.com/cE1c2wY.png)


## 3. **Demonstrate key management concepts by modifying the client in the Multi-Sig tutorial to address one of the additional scenarios**

I followed the second scenario (Deploying with special keys)


### client-side code

```javascript=
const keyManager = require('./key-manager');
const TRANSFER_AMOUNT = process.env.TRANSFER_AMOUNT || 2500000000;

(async function () {
    let deploy;
    let masterKey = keyManager.randomMasterKey();
    let fullAccessAccount = masterKey.deriveIndex(1);
    let limitedAccessAccount = masterKey.deriveIndex(2);

    console.log("\n0.1 Fund main account.\n");
    await keyManager.fundAccount(fullAccessAccount);
    await keyManager.printAccount(fullAccessAccount);
    
    console.log("\n[x]0.2 Install Keys Manager contract");
    deploy = keyManager.keys.buildContractInstallDeploy(fullAccessAccount);
    await keyManager.sendDeploy(deploy, [fullAccessAccount]);
    await keyManager.printAccount(fullAccessAccount);

    // 1. Set fullAccessAccount's weight to 2
    console.log("\n1. Setting fullAccessAccount's weight to 2\n");
    deploy = keyManager.keys.setKeyWeightDeploy(fullAccessAccount, fullAccessAccount, 2);
    await keyManager.sendDeploy(deploy, [fullAccessAccount]);
    await keyManager.printAccount(fullAccessAccount);
    
    // 2. Set Keys Management Threshold to 2.
    console.log("\n2. Setting Keys Management Threshold to 2\n");
    deploy = keyManager.keys.setKeyManagementThresholdDeploy(fullAccessAccount, 2);
    await keyManager.sendDeploy(deploy, [fullAccessAccount]);
    await keyManager.printAccount(fullAccessAccount);
    
    // 3. Set Deploy Threshold to 1.
    console.log("\n3. Setting Deploy Threshold to 1.\n");
    deploy = keyManager.keys.setDeploymentThresholdDeploy(fullAccessAccount, 1);
    await keyManager.sendDeploy(deploy, [fullAccessAccount]);
    await keyManager.printAccount(fullAccessAccount);
    
    // 4. Add our first new key (limited Access Account) with weight 1.
    console.log("\n4. Addding first new key with weight 1.\n");
    deploy = keyManager.keys.setKeyWeightDeploy(fullAccessAccount, limitedAccessAccount, 1);
    await keyManager.sendDeploy(deploy, [fullAccessAccount]);
    await keyManager.printAccount(fullAccessAccount);
    
})();
```

### Output:

![](https://i.imgur.com/txZCKUq.png)


## 4. **Learn to transfer tokens to an account on the Casper Testnet.**

### Transfer using CLI:

![](https://i.imgur.com/KbRAmpS.png)


### Transfer using Casper Portal:

![](https://i.imgur.com/HBI8fHy.png)




## 5. **Learn to Delegate and Undelegate on the Casper Testnet.**

### Delegation using CLI:

![](https://i.imgur.com/5HTBD6e.png)


### Delegation using Casper Portal: 

![](https://i.imgur.com/L1GHaHg.png)

### Undelegation using CLI:

![](https://i.imgur.com/IrJS9LN.png)


### Undelegation using Casper Portal: 

![](https://i.imgur.com/9ZxEhpd.png)


















