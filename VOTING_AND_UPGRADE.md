# Voting and Binary Upgrade Guide

This guide provides step-by-step instructions for voting on proposals and upgrading binaries after a proposal succeeds.

## Network Information
- Chain ID: `selfchain-testnet`
- RPC Endpoint: `https://rpc-testnet.selfchain.xyz:26657`

## Table of Contents
- [Voting on Proposals](#voting-on-proposals)
- [Upgrading Binaries](#upgrading-binaries)
- [Verification Steps](#verification-steps)

## Voting on Proposals

### 1. Check Active Proposals
```bash
selfchaind query gov proposals --status voting_period --node https://rpc-testnet.selfchain.xyz:26657
```

### 2. Get Proposal Details
```bash
selfchaind query gov proposal <proposal_id> --node https://rpc-testnet.selfchain.xyz:26657
```

### 3. Cast Your Vote
You can vote with the following options:
- `yes`: Vote in favor of the proposal
- `no`: Vote against the proposal
- `no_with_veto`: Vote to veto the proposal
- `abstain`: Abstain from voting

```bash
selfchaind tx gov vote <proposal_id> <vote_option> --from <your_key_name> --chain-id selfchain-testnet --node https://rpc-testnet.selfchain.xyz:26657
```

Example:
```bash
selfchaind tx gov vote 1 yes --from validator --chain-id selfchain-testnet --node https://rpc-testnet.selfchain.xyz:26657
```

## Upgrading Binaries

After a proposal succeeds, follow these steps to upgrade your binary:

### 1. Stop the Current Node
```bash
# Find the node process
ps aux | grep selfchaind

# Kill the process
kill -9 <process_id>
```

### 2. Backup Current Binary
```bash
cp $(which selfchaind) ~/selfchaind_backup
```

### 3. Download and Install New Binary
```bash
# Download the new binary
wget https://github.com/selfchainxyz/testnet-setup/releases/download/testnet-v2.0.0/selfchaind-linux-amd64

# Make it executable
chmod +x selfchaind-linux-amd64

# Move to the correct location
sudo mv selfchaind-linux-amd64 /usr/local/bin/selfchaind
```

### 4. Verify Binary Version
```bash
selfchaind version
```

### 5. Start the Node
You must start the node and ensure it is fully synced before proceeding.

Start the node process in the background:
```bash
nohup selfchaind start > selfchain-testnet.logs &
```

Check the live logs to confirm the node is syncing:
```bash
tail -f selfchain-testnet.logs
```

Check the node's current status:
```bash
selfchaind status
```

### 6. Verify Node Status
To verify your node's status against the testnet:
```bash
selfchaind status --node https://rpc-testnet.selfchain.xyz:26657
```

## Verification Steps

After upgrading, verify the following:

1. Check node synchronization:
```bash
selfchaind status | jq .SyncInfo
```

2. Verify the new version is running:
```bash
selfchaind version
```

3. Check for any errors in the logs:
```bash
journalctl -u selfchaind -f
```

## Important Notes

- Always backup your current binary before upgrading
- Ensure you have enough disk space for the new binary
- Keep your validator key secure during the upgrade process
- Monitor the node after upgrade for any issues
- If problems occur, you can rollback using the backup binary

## Troubleshooting

If you encounter issues during the upgrade:

1. Check the logs for specific error messages
2. Verify network connectivity
3. Ensure all required dependencies are installed
4. If necessary, rollback to the previous version using the backup binary

For any questions or issues, reach out to the SelfChain testnet support team via Discord.