### Calling Contracts in Solidity
Solidity compiles contracts to bytecode and doesn't inherently understand the chain it's deployed on. When calling a contract, you can use:

## High-Level Syntax
Automatically handles calldata encoding.

Improves readability and developer experience.

Best when you have the ABI of the contract.

# solidity
OtherContract(address).someFunction(arg1, arg2);

## Low-Level Syntax
Requires manual encoding of calldata.

Offers fine-grained control, useful without the ABI.

Ideal for advanced interactions or generic contract calls.

# solidity
(bool success, bytes memory data) = address(contract).call(abi.encodeWithSignature("functionName(uint256)", 123));

### Escrow Contracts: Real-World Use
An escrow contract is a trustless financial mechanism involving:

# Participants
Buyer: Sends funds to the contract.

Seller: Provides the goods/services.

Arbitrator: A third party resolving disputes and authorizing payments.

# Functionality
deposit(): Buyer sends payment.

confirmDelivery(): Buyer acknowledges goods received.

releaseFunds(): Arbitrator sends funds to seller.

resolveDispute(): Arbitrator resolves any disagreements.

#### Reverting Transactions
When a contract call reverts, all state changes during that call are undone.

🧠 Key Concepts
require(), assert(), or revert() cause reversion.

Useful for error handling and state consistency.

Call Stack Behavior:

If Contract A → B → C, and C reverts, it can propagate back to A unless caught.

solidity
try contractB.someCall() {
    // proceed
} catch {
    // handle error
}
# Sending Ether Between Contracts
Ether and calldata are transferred using message calls:

# Message Calls
Each contract-to-contract call is part of the same transaction.

Execution completes only when the initial call finishes.

# Call Mechanics
EOAs and Contracts call others using their address (20 bytes).

msg.sender refers to the immediate caller of the function.

Ether Transfer Example:

# solidity
(bool sent, ) = payable(recipient).call{value: amount}("");
require(sent, "Transfer failed");
