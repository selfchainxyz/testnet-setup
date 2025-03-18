# Upgrade Instructions for Self Chain Testnet

## Step 1: Download and Setup  
- Download the older version of the binary from [Self Chain Releases](https://docs.selfchain.xyz/nodes-and-validators/releases#self-chain-testnet-v2.0.0).  
- Set up the Cosmos project.

## Step 2: Replace Genesis File  
- Replace the provided **testnet `genesis.json`** with the correct version.

## Step 3: Update Configuration  
- Modify the following settings in **`config.toml`** as required.

## Step 4: Run Older Binary  
- Start the **older binary** and let it run until it **stops indexing** for **v2 version**. 

## Step 5: Upgrade to CosmWasm Binary  
- Replace the older binary with the **updated CosmWasm binary**.   - https://drive.google.com/file/d/1nuuqllKvI7AzXBXj6agCpEMYAHLtdvL3/view?usp=sharing
- Continue running the node until it reaches the **top block**.
