# window.ethereum.methods

The `window.ethereum` object is injected into the browser by Ethereum-enabled browser extensions like MetaMask. It exposes various methods to interact with the Ethereum network.

Here are some commonly used methods available on `window.ethereum`:

### 1. **`eth_requestAccounts`**
   - Requests access to the user's Ethereum accounts (MetaMask will ask the user to allow the request).
   - **Usage**:
     ```javascript
     await window.ethereum.request({ method: 'eth_requestAccounts' });
     ```
   
### 2. **`eth_chainId`**
   - Returns the current chain ID of the connected network.
   - **Usage**:
     ```javascript
     const chainId = await window.ethereum.request({ method: 'eth_chainId' });
     console.log(chainId); // Example: '0x1' for Ethereum mainnet
     ```

### 3. **`eth_accounts`**
   - Returns a list of Ethereum accounts available in the user's wallet (MetaMask).
   - **Usage**:
     ```javascript
     const accounts = await window.ethereum.request({ method: 'eth_accounts' });
     console.log(accounts); // List of accounts
     ```

### 4. **`eth_gasPrice`**
   - Returns the current gas price in wei.
   - **Usage**:
     ```javascript
     const gasPrice = await window.ethereum.request({ method: 'eth_gasPrice' });
     console.log(gasPrice); // Gas price in wei
     ```

### 5. **`eth_getBalance`**
   - Returns the balance of a given address in wei.
   - **Usage**:
     ```javascript
     const balance = await window.ethereum.request({
       method: 'eth_getBalance',
       params: ['0xAddressHere', 'latest']
     });
     console.log(balance); // Balance in wei
     ```

### 6. **`eth_sendTransaction`**
   - Sends a transaction to the Ethereum network (you need to pass a transaction object).
   - **Usage**:
     ```javascript
     const tx = await window.ethereum.request({
       method: 'eth_sendTransaction',
       params: [{
         from: '0xYourAddressHere',
         to: '0xRecipientAddressHere',
         value: '0xAmountInWei', // For example: '0x29a2241af62c0000' for 0.1 ETH
       }],
     });
     console.log(tx); // Transaction hash
     ```

### 7. **`eth_sign`**
   - Signs a message using the selected account.
   - **Usage**:
     ```javascript
     const message = 'Hello, Ethereum!';
     const signature = await window.ethereum.request({
       method: 'eth_sign',
       params: ['0xYourAddressHere', message],
     });
     console.log(signature); // The signature of the message
     ```

### 8. **`eth_signTypedData`** (v4+)
   - Used for signing typed data (e.g., for EIP-712 compatible signatures).
   - **Usage**:
     ```javascript
     const typedData = {
       types: {
         EIP712Domain: [
           { name: 'name', type: 'string' },
           { name: 'version', type: 'string' },
         ],
       },
       domain: { name: 'MyApp', version: '1' },
       message: { from: '0xYourAddressHere' },
     };
     const signature = await window.ethereum.request({
       method: 'eth_signTypedData',
       params: ['0xYourAddressHere', typedData],
     });
     console.log(signature); // The signature
     ```

### 9. **`eth_subscribe`**
   - Used to subscribe to certain Ethereum events (e.g., new blocks, pending transactions, etc.).
   - **Usage**:
     ```javascript
     const subscription = await window.ethereum.request({
       method: 'eth_subscribe',
       params: ['newHeads']
     });
     console.log(subscription);
     ```

### 10. **`enable`** (deprecated in favor of `eth_requestAccounts`)
   - This method was used in older versions of MetaMask to request account access. It is now deprecated in favor of `eth_requestAccounts`.

### 11. **`isConnected`**
   - Checks if the current provider (e.g., MetaMask) is connected.
   - **Usage**:
     ```javascript
     const isConnected = window.ethereum.isConnected();
     console.log(isConnected); // true if connected, false if not
     ```

### 12. **`request`** (general method to interact with Ethereum)
   - In newer versions of MetaMask (and other providers), `request` is a generic method that combines the functionality of previous methods like `send` and `sendAsync`.
   - **Usage**:
     ```javascript
     const accounts = await window.ethereum.request({ method: 'eth_accounts' });
     console.log(accounts); // List of accounts
     ```

### 13. **`on` (Event Listeners)**
   - You can listen for various events like account changes and network changes.
   - **Usage**:
     ```javascript
     window.ethereum.on('accountsChanged', (accounts) => {
       console.log('Accounts changed:', accounts);
     });

     window.ethereum.on('chainChanged', (chainId) => {
       console.log('Chain changed:', chainId);
     });
     ```

These are some of the most commonly used methods in `window.ethereum`. They allow you to interact with the Ethereum blockchain and perform actions like account management, sending transactions, and subscribing to events.

_let me know if there is any changes_
