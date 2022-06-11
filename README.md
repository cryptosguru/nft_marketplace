# 🖼️ NFT Marketplace

[![https://img.shields.io/badge/made%20with-hardhat-yellow](https://img.shields.io/badge/made%20with-hardhat-yellow)](https://hardhat.org/)
[![https://img.shields.io/badge/made%20with-nextjs-blue](https://img.shields.io/badge/made%20with-nextjs-blue)](https://nextjs.org/)

This is a fullstack DApp NFT Marketplace.  
Made with NodeJS, Hardhat, Solidity, ReactJS, NextJS and Vercel.

# Market basic actions

You can **create** (mint) new tokens, uploading their image and metadata on [IPFS](https://ipfs.io/) using [Pinata](https://www.pinata.cloud/).  
If you've created or bought an NFT, you may also **sell** it by setting a price and paying a listing fee.  
When **buying** an NFT, the price will be transferred to the seller and the listing fee to the NFT Marketplace owner.  
It's also possible to **cancel** a market item, transferring it back to the owner.

---

# Lean NFTs Visualization

There are only two pages to view market's NFTs:

- **Market Page**

Shows all NFTs that are available to be bought.  
This page will show NFTs even if the user doesn't have the [Metamask](https://metamask.io/) extension or isn't connected to the dapp.

- **My NFTs Page**

Show all account's created, owned and on sale NFTs.  
Here you keep track of NFT's you've created and check for how much they've been last sold and their current owner.  
You can also list your current owned NFTs or cancel existing ones.  
To view this page, you must have Metamask installed and have it connected to Polygon's Testnet network.

# User Experience
When **changing account or network**, the page will refresh updating only the affected components.

When performing an action, a loading feedback is shown and the card updates to its new state automatically.

# Easy Deployment

Frontend is automatically deployed using Vercel's Github integration, but contracts have to be manually deployed to keep a better control on them.  
However, new deployed contract addresses can be updated on the frontend simply by running a script that modifies Vercel's project environment variables and triggers a new frontend deployment.

# How to run

- Copy `.env.local.example` to `.env.local` and fill it with environment variables
- Run `npm run node` to start a local EVM blockchain testnet
- Run `npm run setup` to deploy NFT and Marketplace contracts and perform some initial actions to the local blockchain
- Run `npm run dev` to start frontend application
- Make sure to use `Localhost 8545` as the Metamask's network
- Make sure to import local Account #0 and #1 into Metamask accounts.

# How to deploy

- Frontend is deployed automatically on `main` branch using Vercel's github integration
- Set ACCOUNT_PRIVATE_KEY in `.env.local` and send it some Polygon's Testnet [Matic](https://faucet.polygon.technology/) tokens
- Run `npm run deploy:mumbai` to deploy contracts to Polygon`s Testnet (Mumbai)
- Optional: do the same for ACCOUNT2_PRIVATE_KEY env and run `npm run setup-marketplace:mumbai` to setup the marketplace with existing tokens and sales.
- Run `npm run env` to update Vercel's environment variables with the new deployed contract addresses.\*
- Make sure to use `Polygon Testnet Mumbai` as Metamask's network

_\* You'll need to create the envs on Vercel first_

# Development Challenges

- Updating NFT UI Cards after an action was performed
- Dealing with [Metamask's accountsChanged event being fired twice on mobile](https://github.com/MetaMask/metamask-mobile/issues/2162)
- Building a Web3 context provider
- Debugging different problems that ended up causing "Estimate gas failed" errors\*

_\* They're usually caused by incorrect contract addresses and wrong default gas values_

## Mumbai marketplace setup command is breaking with a 'estimate gas failed' error

Try changing `hardhat.config.js` mumbai gas values.  
I'm using the ones I've found here:  
https://forum.moralis.io/t/deploy-to-polygon-matic-mumbai-fails/700

## Nouce is too high

Reset your Metamask account transaction history.  
Find out more on:  
https://medium.com/@thelasthash/solved-nonce-too-high-error-with-metamask-and-hardhat-adc66f092cd

