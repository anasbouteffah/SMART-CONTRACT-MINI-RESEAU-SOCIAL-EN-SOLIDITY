
# MiniSocial Smart Contract

This repository contains the source code and documentation for the **MiniSocial** smart contract, a basic social media simulation on the Ethereum blockchain. Built in Solidity, this smart contract allows users to publish and view messages. The contract is designed to be deployed using MetaMask on the SepoliaETH test network and was developed with Remix IDE.

## Project Overview

The **MiniSocial** contract enables:
- Posting messages by users.
- Retrieving posted messages along with author information.
- Checking the total count of messages posted on the platform.

### Key Features
- **Post Storage**: Each message is stored on-chain, with an associated author address.
- **Message Retrieval**: Users can view any posted message by specifying its index.
- **Message Count**: Retrieves the total number of messages published.

## Smart Contract Structure

The contract consists of:
1. **Post Struct**: A structure to define each post with:
   - `message`: The text content of the post.
   - `author`: The Ethereum address of the post’s creator.

2. **Functions**:
   - `publishPost(string memory _message)`: Publishes a message.
   - `getPost(uint index)`: Retrieves a specific post’s message and author by its index.
   - `getTotalPosts()`: Returns the total number of posts.

## Code

The Solidity code for the contract is as follows:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MiniSocial {
    struct Post {
        string message;   
        address author;   
    }
    
    Post[] public posts;

    function publishPost(string memory _message) public {
        Post memory newPost = Post({
            message: _message,
            author: msg.sender
        });

        posts.push(newPost);
    }

    function getPost(uint index) public view returns (string memory, address) {
        require(index < posts.length, "The message doesn't exist");
        Post memory post = posts[index];
        return (post.message, post.author);
    }

    function getTotalPosts() public view returns (uint) {
        return posts.length;
    }
}
```

## Deployment and Testing

### Prerequisites
- **Remix IDE**: Used for development and initial testing.
- **MetaMask**: Connect to the SepoliaETH test network for deployment.

### Steps
1. **Remix Testing**:
   - Deploy the contract in Remix’s virtual environment.
   - Use `publishPost` to add messages.
   - Verify `getPost` and `getTotalPosts` functions to ensure data consistency.
   
2. **Deployment on SepoliaETH**:
   - Use MetaMask to deploy the contract on SepoliaETH.
   - Ensure you have test ETH for gas fees.
   - Test the contract functions with different accounts to verify address-based functionality.

## Contributing

Feel free to open issues or submit pull requests to enhance the contract or documentation.

## License

This project is licensed under the MIT License.
