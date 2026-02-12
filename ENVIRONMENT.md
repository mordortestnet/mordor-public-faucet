# Environment Variables & Secrets Configuration

This document describes all environment variables and GitHub Secrets required to run the Mordor Public Faucet workflows.

## 🔐 Required Secrets

### PRIVATE_KEY (Required for all workflows)

**Description**: The private key of your Ethereum Classic wallet for the Mordor testnet.

**How to obtain**:
1. Create a new wallet specifically for testnet use (NEVER use mainnet keys)
2. You can create a wallet using:
   - MetaMask (create new account, export private key)
   - MyCrypto (create new wallet)
   - ethers.js CLI: `npx ethers-wallet --create`
   - Or any other Ethereum wallet tool

**How to add to GitHub**:
1. Go to your repository on GitHub
2. Navigate to **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Name: `PRIVATE_KEY`
5. Value: Your wallet's private key **without the `0x` prefix**
   - Example format: `1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef`
   - Do NOT include: `0x1234567890abcdef...`
6. Click **Add secret**

**Security Notes**:
- ⚠️ **TESTNET ONLY**: Never use a private key that holds mainnet funds
- 🔒 **Dedicated Wallet**: Create a new wallet specifically for this purpose
- 🔒 **Never Commit**: Never commit private keys to the repository
- 🔒 **Secure Storage**: GitHub Secrets are encrypted and only exposed during workflow runs
- 🔒 **Access Control**: Only users with write access to the repository can see/edit secrets

**Used by**:
- ✅ `wrap-etc.yml` - Wrapping ETC to WETC
- ✅ `unwrap-wetc.yml` - Unwrapping WETC to ETC
- ✅ `token-distribution-pr.yml` - PR-based WETC distribution
- ✅ `etc-distribution-pr.yml` - PR-based ETC distribution
- ✅ `catacomb-safe-distribution.yml` - Catacomb multisig distribution

---

## 🔑 Optional Secrets

### For Catacomb Safe (Multisig) Workflows

If using the Catacomb Safe multisig approach (`catacomb/` directory):

#### SAFE_ADDRESS
**Description**: The address of your Safe (Catacomb) multisig wallet on Mordor testnet.

**Example**: `0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb`

**How to obtain**:
1. Create a Safe on Catacomb (ETC's Safe deployment)
2. Copy the Safe address
3. Add as a GitHub Secret (same process as PRIVATE_KEY)

#### SIGNER_PRIVATE_KEY_1, SIGNER_PRIVATE_KEY_2, etc.
**Description**: Private keys for Safe signers (if you control multiple signers).

**Security**: Same security considerations as PRIVATE_KEY above.

---

## 📋 Workflow Input Variables

These are NOT secrets but inputs provided when running workflows:

### Wrap ETC Workflow

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `percentage` | string | `10` | Percentage of ETC balance to wrap (1-100) |

**Example**: `25` will wrap 25% of your ETC balance

### Unwrap WETC Workflow

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `amount` | string | (empty) | Amount of WETC to unwrap. Leave empty to unwrap all. |

**Example**: `5.5` will unwrap 5.5 WETC

### PR-Based Distribution Workflows

These workflows extract the wallet address from the PR body, no manual input required.

| Input | Source | Description |
|-------|--------|-------------|
| Wallet Address | PR Description | Extracted automatically from PR body |

**Example PR Description**:
```
Please send test tokens to: 0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb
```

---

## 🌐 Environment Configuration

### Network Configuration (Built-in)

These values are hardcoded in the workflows and do not need to be configured:

| Variable | Value | Description |
|----------|-------|-------------|
| `MORDOR_RPC` | `https://rpc.mordor.etccooperative.org` | RPC endpoint for Mordor testnet |
| `CHAIN_ID` | `63` | Ethereum Classic Mordor testnet chain ID |
| `WETC_ADDRESS` | `0x1953cab0E5bFa6D4a9BaD6E05fD46C1CC6527a5a` | WETC (Wrapped ETC) contract address |

### Block Explorer

| Variable | Value | Description |
|----------|-------|-------------|
| `BLOCK_EXPLORER` | `https://etc-mordor.blockscout.com/` | Blockscout explorer for Mordor |

---

## 🚀 Quick Setup Guide

### For Basic Usage (Wrap/Unwrap)

1. **Create a testnet wallet**
   ```bash
   # Using ethers.js
   npx ethers-wallet --create
   ```

2. **Get some Mordor ETC**
   - Use an existing Mordor testnet faucet
   - Or ask in ETC community channels

3. **Add PRIVATE_KEY secret**
   - Settings → Secrets → Actions → New secret
   - Name: `PRIVATE_KEY`
   - Value: Your private key (no 0x prefix)

4. **Enable workflows**
   - Go to Actions tab
   - Click "I understand my workflows, go ahead and enable them"

5. **Run a workflow**
   - Actions → Select workflow → Run workflow

### For PR-Based Distribution (Faucet)

1. **Complete Basic Setup above**

2. **Enable PR workflows**
   - Workflows are triggered automatically on PR events
   - No additional configuration needed

3. **Test the faucet**
   - Create a test PR in your fork
   - Add a wallet address in the PR description
   - Watch the workflow run

### For Catacomb Safe (Multisig)

1. **Complete Basic Setup above**

2. **Create Safe on Catacomb**
   - Visit Catacomb Safe interface
   - Create 2-of-3 (or desired configuration) Safe
   - Note the Safe address

3. **Add Safe secrets**
   - `SAFE_ADDRESS`: Your Safe's address
   - `SIGNER_PRIVATE_KEY_1`: First signer's key
   - `SIGNER_PRIVATE_KEY_2`: Second signer's key (if you control it)

4. **Configure Safe workflow**
   - Update `catacomb-safe-distribution.yml` with your Safe address
   - Set up signing threshold

---

## 🔒 Security Best Practices

### DO ✅

- ✅ Use dedicated testnet wallets
- ✅ Store keys in GitHub Secrets
- ✅ Enable 2FA on your GitHub account
- ✅ Review workflow logs after each run
- ✅ Use minimal permissions
- ✅ Rotate keys if compromised
- ✅ Test with small amounts first

### DON'T ❌

- ❌ Use mainnet private keys
- ❌ Commit secrets to the repository
- ❌ Share secret values publicly
- ❌ Use the same key across multiple projects
- ❌ Expose secrets in workflow logs
- ❌ Give repository access to untrusted users
- ❌ Skip testing before production use

---

## 🔍 Verifying Your Setup

### Check Secret Configuration

1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Verify `PRIVATE_KEY` is listed
3. You cannot view the value (this is correct)
4. Only admins can update secrets

### Test the Configuration

1. **Run a test workflow**:
   - Go to Actions → "Wrap ETC to WETC"
   - Click "Run workflow"
   - Use a small percentage (e.g., 1%)
   - Check the logs

2. **Verify in logs**:
   - Wallet address should be displayed
   - Balance should be shown
   - No errors about missing PRIVATE_KEY
   - Transaction should complete successfully

3. **Check on Block Explorer**:
   - Copy transaction hash from logs
   - Visit https://etc-mordor.blockscout.com/
   - Paste transaction hash
   - Verify transaction succeeded

---

## 📞 Troubleshooting

### "PRIVATE_KEY not found in environment"

**Problem**: The PRIVATE_KEY secret is not configured.

**Solution**:
1. Go to Settings → Secrets → Actions
2. Verify PRIVATE_KEY exists
3. Check it's named exactly `PRIVATE_KEY` (case-sensitive)
4. Re-add the secret if needed

### "Insufficient balance" or "Insufficient funds"

**Problem**: Wallet doesn't have enough ETC for the operation.

**Solution**:
1. Check your wallet balance on Blockscout
2. Get more testnet ETC from a faucet
3. Reduce the percentage when wrapping
4. Reserve enough ETC for gas fees

### Workflow fails with "Invalid private key"

**Problem**: The private key format is incorrect.

**Solution**:
1. Ensure no `0x` prefix
2. Should be 64 hexadecimal characters
3. Check for extra spaces or newlines
4. Re-export from your wallet if needed

### Cannot trigger workflows

**Problem**: Workflows are disabled in your fork.

**Solution**:
1. Go to the Actions tab
2. Click "I understand my workflows, go ahead and enable them"
3. Try running the workflow again

---

## 📚 Additional Resources

- [GitHub Secrets Documentation](https://docs.github.com/en/actions/security-guides/encrypted-secrets)
- [Mordor Testnet Information](https://github.com/etclabscore/mordor)
- [Ethers.js Documentation](https://docs.ethers.org/)
- [Security Policy](SECURITY.md)

---

## 💬 Need Help?

If you're having trouble with configuration:

1. Check this documentation first
2. Review the [QUICKSTART.md](QUICKSTART.md)
3. Search existing GitHub Issues
4. Open a new Issue with details
5. Ask in GitHub Discussions

---

Last Updated: 2026-02-12
