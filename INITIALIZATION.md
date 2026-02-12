# Project Initialization Guide

This guide will help you set up a new fork of the Mordor Public Faucet and get it running with CI/CD.

## 🎯 Quick Overview

The Mordor Public Faucet is a GitHub Actions-based system for:
- Wrapping/unwrapping ETC ↔ WETC on the Mordor testnet
- Distributing testnet tokens via Pull Request workflows
- Managing a multisig treasury with Catacomb Safe

## 📋 Prerequisites

Before you begin, ensure you have:
- ✅ A GitHub account with 2FA enabled
- ✅ Basic knowledge of GitHub and GitHub Actions
- ✅ A wallet with Mordor testnet ETC (for testing)
- ✅ Understanding of Ethereum and testnet concepts

## 🚀 Step-by-Step Setup

### 1. Fork the Repository

1. Visit https://github.com/mordortestnet/mordor-public-faucet
2. Click the **Fork** button in the top-right corner
3. Choose your account/organization
4. Wait for the fork to complete

### 2. Enable GitHub Actions

After forking:

1. Go to your forked repository
2. Click the **Actions** tab
3. Click **"I understand my workflows, go ahead and enable them"**
4. Workflows are now active in your fork

### 3. Configure Required Secrets

#### Create a Testnet Wallet

**IMPORTANT**: Create a NEW wallet specifically for testnet use. Never use mainnet keys!

```bash
# Using ethers.js (recommended)
npx ethers-wallet --create

# Or use MetaMask
# 1. Open MetaMask
# 2. Create a new account
# 3. Export private key (Settings → Security & Privacy → Reveal Private Key)
```

Save your private key securely (you'll need it in the next step).

#### Add PRIVATE_KEY Secret

1. Go to your fork: `https://github.com/YOUR_USERNAME/mordor-public-faucet`
2. Click **Settings** (top menu)
3. In the left sidebar: **Secrets and variables** → **Actions**
4. Click **New repository secret**
5. Configure the secret:
   - **Name**: `PRIVATE_KEY`
   - **Value**: Your wallet's private key **without** the `0x` prefix
   - Example: `abcd1234...` (64 hexadecimal characters)
6. Click **Add secret**

#### Verify Secret Configuration

1. Go to **Settings** → **Secrets and variables** → **Actions**
2. You should see `PRIVATE_KEY` listed
3. The value will be hidden (this is correct and secure)

### 4. Fund Your Wallet with Testnet ETC

Your wallet needs Mordor testnet ETC to perform transactions.

**Option A**: Use an existing Mordor faucet
- Search for "Mordor testnet faucet" in the ETC community
- Request testnet ETC to your wallet address

**Option B**: Ask in the community
- Join ETC Discord or Telegram
- Ask for Mordor testnet tokens
- Provide your wallet address

**Verify your balance**:
1. Visit https://etc-mordor.blockscout.com/
2. Search for your wallet address
3. Confirm you have ETC balance

### 5. Test the Setup

#### Test Wrap Workflow

1. Go to **Actions** tab in your fork
2. Click **"Wrap ETC to WETC"** workflow (left sidebar)
3. Click **Run workflow** (right side)
4. Configure inputs:
   - Branch: `main` or `master`
   - Percentage: `1` (test with 1% first)
5. Click **Run workflow** button
6. Wait for the workflow to complete (30-60 seconds)
7. Check the logs for success

**Expected output**:
```
✅ Wallet address: 0x...
✅ Current ETC balance: X.XX ETC
✅ Amount to wrap: Y.YY ETC (1%)
✅ Transaction confirmed in block XXXXX
✅ Transaction Summary
   ETC Balance: X.XX → Z.ZZ
   WETC Balance: 0.00 → Y.YY
```

#### Verify on Blockchain

1. Copy the transaction hash from the workflow logs
2. Visit https://etc-mordor.blockscout.com/
3. Paste the transaction hash in the search bar
4. Verify the transaction succeeded

### 6. Configure Branch Protection (Optional but Recommended)

Protect your main branch from accidental changes:

1. Go to **Settings** → **Branches**
2. Click **Add rule** (or **Add branch protection rule**)
3. Configure:
   - **Branch name pattern**: `main` (or `master`)
   - ✅ **Require pull request reviews before merging**
   - ✅ **Require status checks to pass before merging**
   - Select CI workflows: `CI - Workflow Validation`, `CI - Security`, etc.
   - ✅ **Require branches to be up to date before merging**
   - ✅ **Include administrators** (optional)
4. Click **Create** or **Save changes**

### 7. Set Up GitHub Labels (Optional)

Labels help organize issues and PRs. Create these labels:

| Label | Color | Description |
|-------|-------|-------------|
| `bug` | `#d73a4a` | Something isn't working |
| `documentation` | `#0075ca` | Documentation improvements |
| `enhancement` | `#a2eeef` | New feature or request |
| `good first issue` | `#7057ff` | Good for newcomers |
| `help wanted` | `#008672` | Extra attention needed |
| `security` | `#ee0701` | Security-related issues |
| `workflows` | `#fbca04` | GitHub Actions workflow changes |
| `catacomb` | `#bfdadc` | Related to Catacomb multisig |
| `dependencies` | `#0366d6` | Dependency updates |
| `github-actions` | `#000000` | GitHub Actions updates |

**How to add labels**:
1. Go to **Issues** → **Labels**
2. Click **New label** for each label above
3. Enter name, description, and color
4. Click **Create label**

### 8. Enable Discussions (Optional)

Enable GitHub Discussions for community questions:

1. Go to **Settings**
2. Scroll to **Features** section
3. Check ✅ **Discussions**
4. Click **Set up discussions**
5. Create initial categories:
   - 💬 General - General discussion
   - 💡 Ideas - Feature ideas and suggestions
   - 🙏 Q&A - Questions and answers
   - 📣 Announcements - Project announcements

### 9. Configure Dependabot (Already Configured)

Dependabot is pre-configured to update GitHub Actions weekly. To verify:

1. Check `.github/dependabot.yml` exists in your fork
2. Dependabot will automatically create PRs for updates
3. Review and merge these PRs to keep actions up-to-date

## 📊 Project Health Checklist

After setup, verify everything is working:

- [ ] ✅ Repository forked successfully
- [ ] ✅ GitHub Actions enabled
- [ ] ✅ `PRIVATE_KEY` secret configured
- [ ] ✅ Wallet funded with testnet ETC
- [ ] ✅ Wrap workflow tested successfully
- [ ] ✅ Transaction verified on Blockscout
- [ ] ✅ CI workflows passing (check Actions tab)
- [ ] ✅ Branch protection configured (optional)
- [ ] ✅ Labels created (optional)
- [ ] ✅ Discussions enabled (optional)

## 🎯 Next Steps

### For Basic Usage
1. ✅ Setup complete! You can now use wrap/unwrap workflows
2. See [QUICKSTART.md](QUICKSTART.md) for usage examples
3. See [ENVIRONMENT.md](ENVIRONMENT.md) for configuration details

### For PR-Based Distribution
1. ✅ Setup complete! Your fork can accept token requests via PRs
2. See [PR_DISTRIBUTION_GUIDE.md](PR_DISTRIBUTION_GUIDE.md) for setup
3. Configure PR approval requirements in branch protection

### For Catacomb Safe (Multisig)
1. Create a Safe on Catacomb (ETC's Safe deployment)
2. See `catacomb/CATACOMB_SETUP_GUIDE.md` for detailed setup
3. Configure additional secrets for Safe signers

## 🔧 Advanced Configuration

### Custom RPC Endpoint

To use a different RPC endpoint:
1. Edit workflow files (e.g., `wrap-etc.yml`)
2. Change `MORDOR_RPC` constant
3. Commit and push changes

### Custom WETC Contract

To use a different WETC contract:
1. Edit workflow files
2. Change `WETC_ADDRESS` constant
3. Update the ABI if needed
4. Commit and push changes

### Multiple Wallets

To use different wallets for different workflows:
1. Create additional secrets: `PRIVATE_KEY_WRAP`, `PRIVATE_KEY_FAUCET`, etc.
2. Edit workflow files to use the appropriate secret
3. Commit and push changes

## 🆘 Troubleshooting

### Workflows Not Appearing

**Problem**: Actions tab shows no workflows.

**Solution**:
1. Click "I understand my workflows, go ahead and enable them"
2. Refresh the page
3. Wait a few minutes and check again

### "PRIVATE_KEY not found" Error

**Problem**: Workflow fails with missing PRIVATE_KEY.

**Solution**:
1. Go to Settings → Secrets → Actions
2. Verify `PRIVATE_KEY` exists
3. Check spelling (must be exactly `PRIVATE_KEY`)
4. Re-add the secret if needed

### "Insufficient balance" Error

**Problem**: Not enough ETC for transaction.

**Solution**:
1. Check balance on Blockscout
2. Get more testnet ETC from a faucet
3. Reduce wrap percentage to 1%

### CI Workflows Failing

**Problem**: New CI workflows show failures.

**Solution**:
1. Go to Actions tab
2. Click the failed workflow
3. Read the error message
4. Common issues:
   - YAML syntax errors (check workflow files)
   - Missing dependencies (re-run workflow)
   - Network issues (temporary, re-run)

### Cannot Push to Repository

**Problem**: Git push fails with permission error.

**Solution**:
1. Verify you're pushing to YOUR fork, not the upstream repo
2. Check your GitHub authentication
3. Use HTTPS or SSH based on your setup

## 📚 Additional Resources

### Documentation
- [QUICKSTART.md](QUICKSTART.md) - Quick start guide
- [ENVIRONMENT.md](ENVIRONMENT.md) - Environment variables
- [CONTRIBUTING.md](CONTRIBUTING.md) - Contributing guide
- [SECURITY.md](SECURITY.md) - Security policy

### External Links
- [Mordor Testnet Info](https://github.com/etclabscore/mordor)
- [Blockscout Explorer](https://etc-mordor.blockscout.com/)
- [GitHub Actions Docs](https://docs.github.com/en/actions)
- [Ethers.js Documentation](https://docs.ethers.org/)

### Community
- [ETC Discord](https://ethereumclassic.org/discord)
- [ETC Reddit](https://www.reddit.com/r/EthereumClassic/)
- [GitHub Discussions](../../discussions) (if enabled)

## 💬 Getting Help

If you run into issues:

1. **Check this guide** - Review the troubleshooting section
2. **Check existing docs** - See the documentation links above
3. **Search issues** - Look for similar problems in Issues tab
4. **Ask for help** - Create a new issue with:
   - Clear description of the problem
   - Steps to reproduce
   - Workflow logs (if applicable)
   - What you've tried so far

## ✅ Success Checklist

You'll know setup is successful when:

- [x] You can run the Wrap ETC workflow manually
- [x] The workflow completes without errors
- [x] You can see the transaction on Blockscout
- [x] Your wallet balances update correctly
- [x] CI workflows pass (green checkmarks in Actions tab)

## 🎉 Congratulations!

You've successfully set up the Mordor Public Faucet! 

Your fork is now ready to:
- ✅ Wrap and unwrap ETC ↔ WETC
- ✅ Accept token distribution requests via PRs
- ✅ Automatically validate contributions with CI/CD
- ✅ Keep dependencies updated with Dependabot

**Happy testing on Mordor! 🚀**

---

Last Updated: 2026-02-12

For questions or issues, please open a GitHub Issue or Discussion.
