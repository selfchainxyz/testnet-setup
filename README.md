# SelfChain Testnet Migration Guide

We are creating a new SelfChain testnet since the existing testnet has diverged from the current production state. This new testnet retains all addresses from the previous testnet with a fixed balance of 10,000 SLF tokens for each address. Validators are required to resynchronize and create their validators again to join the updated network.

If you are not part of the current address list or new to SelfChain, please explicitly request testnet tokens in our Discord channel.

Follow these step-by-step instructions carefully to migrate your validator to the new SelfChain testnet.

---

## 1. Prerequisites

Download the new binary and configuration files:

```bash
wget https://github.com/selfchainxyz/testnet-setup/releases/download/testnet-v1.0.1/testnet-backup.tar.gz
```

Extract the downloaded archive:

```bash
tar -xzvf testnet-backup.tar.gz
```

After extraction, you should have these three files:

* `config.toml`
* `genesis.json`
* `selfchaind-linux-amd64`

---

## 2. Clear Existing Setup

Before initializing the new validator, clear your current chain data:

```bash
rm -rf ~/.selfchain/
```

---

## 3. Initialize Validator

Run the initialization command with your validator name:

```bash
./selfchaind-linux-amd64 init <validator_name> --chain-id selfchain-testnet
```

---

## 4. Configure Files

Replace the default configuration with the provided files:

```bash
cp genesis.json ~/.selfchain/config/genesis.json
cp config.toml ~/.selfchain/config/config.toml
```

---

## 5. Wallet Setup

Use your existing wallet and private key. Ensure you have access to your original wallet.

If you require additional testnet tokens, please request an airdrop from the SelfChain team via Discord.

---

## 6. Create Validator

Execute the following command to register your validator with the network:

```bash
./selfchaind-linux-amd64 tx staking create-validator \
  --from=<wallet_name> \
  --amount=9000000000uslf \
  --pubkey=$(./selfchaind-linux-amd64 tendermint show-validator) \
  --moniker=<validator_name> \
  --chain-id=selfchain-testnet \
  --commission-rate="0.10" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1" \
  --broadcast-mode=sync \
  --fees=500uslf \
  --yes
```

Replace `<wallet_name>` and `<validator_name>` with your actual wallet and validator names.

---

## 7. Verify Setup

Check your validator status using:

```bash
./selfchaind-linux-amd64 query staking validator $(./selfchaind-linux-amd64 keys show <wallet_name> --bech val -a)
```

Ensure your validator is active and correctly funded.

---

## 8. Additional Support

For any questions or issues, reach out to the SelfChain testnet support team via Discord.
