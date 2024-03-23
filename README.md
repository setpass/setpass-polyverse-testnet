# PIT Phase 2 repo project: Cross-chain Proof of NFT

This repository is created to enter the PIT phase 2.

## Team Members

- @dongqn

## Description

This application enables a user to submit a vote a ballot on a contract on OP Sepolia. The information about this vote subsequently gets sent to an ERC721 NFT contract on Base Sepolia to mint an NFT related to the vote.

Features:

- Uses Polymer x IBC as the cross-chain format
- Commits to the spirit of application specific chains/rollups where voting functionality could be specialized on one chain, NFT marketplace on another and both can form composable applications through interoperability.

## Resources used

The repo uses the [ibc-app-solidity-template](https://github.com/open-ibc/ibc-app-solidity-template) as starting point and adds custom contracts XBallot and XProofOfVoteNFT that implement the custom logic.

It changes the send-packet.js script slightly to adjust to the custom logic.

The expected behaviour from the template should still work but nevertheless we quickly review the steps for the user to test the application...
Run `just --list` for a full overview of the just commands.

Additional resources used:
- Hardhat
- Blockscout
- Tenderly

## Steps to reproduce

After cloning the repo, install dependencies:

```sh
just install
```

And add your private key to the .env file (rename it from .env.example).

### Sending a packet

Now with an existing channel in the config (your own or the default), run:

```sh
just do-it
```
You'll see an active waiting poll in the terminal and will be informed if the packet was sent successfully.

## Proof of testnet interaction

After following the steps above you should have interacted with the testnet. You can check this at the [IBC Explorer](https://sepolia.polymer.zone/packets).

Here's the data of our application:

- XBallot (OP Sepolia) : 0xdeB99059bbe8C4Fabc76Da956Ac9e8B482dC7535
- XProofOfVoteNFT (Base Sepolia): 0x5cd12fc20679c623966a7ca49eaa0ecf6bc2c258
- Channel (OP Sepolia): channel-39230
- Channel (Base Sepolia): channel-39231

- Proof of Testnet interaction:
    - [SendTx](https://optimism-sepolia.blockscout.com/tx/0x8f1e26688aafb3e09342cead7d901863f5ec4234a50c6aedac7cf1de4b6ffaff)
    - [RecvTx](https://base-sepolia.blockscout.com/tx/0x18a8dbae03c92f2957e66f94d7b5b74d563978cac1df7c4b20fae8a025ee789c)
    - [Ack](https://optimism-sepolia.blockscout.com/tx/0x651541d76a97f904226f124e452ee38ba6878436537e770de38b57cc8d1fc45d)

## Challenges Faced

- Debugging used to be tricky when the sendPacket on the contract was successfully submitted but there was an error further down the packet lifecycle.
What helped was to verify the contracts and use Tenderly for step-by-step debugging to see what the relayers submitted to the dispatcher etc.

## What we learned

How to make the first dApp using Polymer.

## Future improvements

Basic functionality was implemented, but the following things can be improved:

- More tests
- More input validation
- Add event listeners related to important IBC lifecycle steps

## Licence

[Apache 2.0](LICENSE)
