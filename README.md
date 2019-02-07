# SolidityInterviewQuestions

## Transactions:

   - https://ethereum.stackexchange.com/questions/1891/whats-the-difference-between-msg-sender-and-tx-origin
   
## Publish and verify contract code on testnet:

   - https://michalzalecki.com/how-to-verify-smart-contract-on-etherscan/

   ```
   How does a contract find out if another address is a contract?
   
   Is it possible, from within a contract written in Solidity, to check if a contract is placed on a specific address or if this address does not contain any code?
   ```
 ```js
   function isContract(address _addr) private returns (bool isContract){
  uint32 size;
  assembly {
    size := extcodesize(_addr)
  }
  return (size > 0);
}
```
```
The assembly language that all Ethereum contracts compile down to contains an opcode for this precise operation: EXTCODESIZE. This opcode returns the size of the code on an address. If the size is larger than zero, the address is a contract. But you need to write assembly code within the contract to access this opcode since the Solidity compiler does not support it directly at the moment. The above code creates a private method that you can call from within your contract to check if another address contains code. If you don't want a private method, remove the private keyword from the function header.

Edit: It turns out that EXTCODESIZE returns 0 if it is called from the constructor of a contract. So if you are using this in a security sensitive setting, you would have to consider if this is a problem.
```
   
