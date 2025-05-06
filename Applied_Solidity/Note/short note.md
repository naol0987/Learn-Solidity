# Solidity Voting & Inheritance Notes

## Voting Systems
Voting is essential for DAOs and governance contracts. Key implementations include:

### Core Components
1. Single Vote per User
   - Uses mapping(address => bool) to track votes
   - Prevents double voting with require checks

2. Multiple Votes
   - Stores votes in arrays: mapping(address => uint256[])
   - Allows voting on multiple proposals

3. Vote Tracking
   - Emits events like VoteCast(address voter)
   - Maintains vote counters with totalVotes

4. Access Control
   - Restricts voting to members via isMember mapping
   - Admin functions to manage voters

### Example Implementation
contract Voting {
    mapping(address => bool) public hasVoted;
    uint256 public totalVotes;
    
    event VoteCast(address voter);
    
    function vote() external {
        require(!hasVoted[msg.sender], "Already voted");
        hasVoted[msg.sender] = true;
        totalVotes++;
        emit VoteCast(msg.sender);
    }
}


## Inheritance in Solidity
Enables code reuse and modular contract design

### Types of Inheritance
1. Single Inheritance
   - Simple parent-child relationship
   - Inherits all public/internal functions

2. Multiple Inheritance
   - Combines multiple parent contracts
   - Order matters due to C3 linearization

### Key Features
- Function Overriding: Use override keyword
- Constructor Initialization: Parent constructors execute in order
- Visibility Rules: Maintains parent contract visibility

### Example Usage
contract Base {
    function foo() public virtual returns (string memory) {
        return "Base";
    }
}

contract Child is Base {
    function foo() public override returns (string memory) {
        return "Child";
    }
}


### Best Practices
- Keep inheritance chains simple
- Use abstract contracts for base functionality
- Document override functions clearly

This covers the essential aspects of voting systems and inheritance patterns in Solidity smart contracts.