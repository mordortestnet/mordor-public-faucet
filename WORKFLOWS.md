# Workflow Status Dashboard

This document provides an overview of all GitHub Actions workflows in this repository.

## 🔄 Core Workflows (User-Facing)

### Manual Workflows

| Workflow | File | Status | Purpose |
|----------|------|--------|---------|
| Wrap ETC to WETC | `wrap-etc.yml` | ![Workflow](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/wrap-etc.yml/badge.svg) | Manually wrap ETC to WETC tokens |
| Unwrap WETC to ETC | `unwrap-wetc.yml` | ![Workflow](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/unwrap-wetc.yml/badge.svg) | Manually unwrap WETC to ETC tokens |

### PR-Based Workflows (Automated)

| Workflow | File | Status | Purpose |
|----------|------|--------|---------|
| Token Distribution (WETC) | `token-distribution-pr.yml` | ![Workflow](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/token-distribution-pr.yml/badge.svg) | Distribute WETC via PR requests |
| ETC Distribution | `etc-distribution-pr.yml` | ![Workflow](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/etc-distribution-pr.yml/badge.svg) | Distribute ETC via PR requests |

### Multisig Workflows

| Workflow | File | Status | Purpose |
|----------|------|--------|---------|
| Catacomb Safe Distribution | `catacomb-safe-distribution.yml` | ![Workflow](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/catacomb-safe-distribution.yml/badge.svg) | Multisig token distribution with Safe |

## 🔧 CI/CD Workflows (Automated Quality Checks)

| Workflow | File | Status | Trigger | Purpose |
|----------|------|--------|---------|---------|
| Workflow Validation | `ci-workflow-validation.yml` | ![CI](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/ci-workflow-validation.yml/badge.svg) | PR, Push, Manual | Validate YAML syntax in workflows |
| Documentation Validation | `ci-docs-validation.yml` | ![CI](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/ci-docs-validation.yml/badge.svg) | PR, Push, Manual | Check markdown files and links |
| Security Scanning | `ci-security.yml` | ![CI](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/ci-security.yml/badge.svg) | PR, Push, Weekly, Manual | Scan for secrets and vulnerabilities |
| PR Checks | `ci-pr-checks.yml` | ![CI](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/ci-pr-checks.yml/badge.svg) | PR | Validate PRs and auto-label |

## 🛠️ Setup Workflows

| Workflow | File | Status | Purpose |
|----------|------|--------|---------|
| Setup Labels | `setup-labels.yml` | ![Setup](https://github.com/mordortestnet/mordor-public-faucet/actions/workflows/setup-labels.yml/badge.svg) | Create repository labels (run once) |

## 📊 Workflow Details

### Core Workflows

#### Wrap ETC to WETC
- **Trigger**: Manual (`workflow_dispatch`)
- **Input**: Percentage of balance to wrap (default: 10%)
- **Runtime**: ~30-60 seconds
- **Requirements**: `PRIVATE_KEY` secret, testnet ETC balance
- **Output**: Transaction hash, updated balances

#### Unwrap WETC to ETC
- **Trigger**: Manual (`workflow_dispatch`)
- **Input**: Amount to unwrap (empty = unwrap all)
- **Runtime**: ~30-60 seconds
- **Requirements**: `PRIVATE_KEY` secret, WETC balance
- **Output**: Transaction hash, updated balances

#### Token Distribution (WETC)
- **Trigger**: Pull Request (with approval)
- **Input**: Wallet address from PR description
- **Runtime**: ~1-2 minutes
- **Requirements**: `PRIVATE_KEY` secret, WETC balance
- **Output**: Distribution transaction

#### ETC Distribution
- **Trigger**: Pull Request (with approval)
- **Input**: Wallet address from PR description
- **Runtime**: ~1-2 minutes
- **Requirements**: `PRIVATE_KEY` secret, ETC balance
- **Output**: Distribution transaction

### CI/CD Workflows

#### Workflow Validation
**What it does**:
- Lints all YAML workflow files
- Validates workflow structure (name, on, jobs)
- Checks for syntax errors

**When it runs**:
- On PRs that modify workflows
- On pushes to main/master
- Manually via workflow_dispatch

**Expected runtime**: ~1 minute

#### Documentation Validation
**What it does**:
- Lints markdown files
- Checks for broken links
- Spell checks documentation

**When it runs**:
- On PRs that modify .md files
- On pushes to main/master
- Manually via workflow_dispatch

**Expected runtime**: ~1-2 minutes

#### Security Scanning
**What it does**:
- Scans for hardcoded secrets
- Checks workflow permissions
- Audits npm dependencies (ethers.js)
- Runs Gitleaks for secret detection

**When it runs**:
- On all PRs
- On pushes to main/master
- Weekly (Mondays at 9am UTC)
- Manually via workflow_dispatch

**Expected runtime**: ~2-3 minutes

#### PR Checks
**What it does**:
- Validates PR title and description
- Checks for linked issues
- Analyzes file changes
- Auto-applies labels based on changes

**When it runs**:
- On PR open, synchronize, reopen

**Expected runtime**: ~30 seconds

## 🔄 Dependabot

Dependabot automatically checks for GitHub Actions updates weekly.

**Configuration**: `.github/dependabot.yml`

**Schedule**: Weekly on Mondays at 9am UTC

**What it updates**:
- GitHub Actions in `.github/workflows/`
- GitHub Actions in `catacomb/.github/workflows/`

**Auto-created PRs**: Up to 5 concurrent PRs

## 📈 Monitoring Workflows

### View All Workflow Runs
Visit: https://github.com/mordortestnet/mordor-public-faucet/actions

### View Specific Workflow
Click the workflow name in the Actions tab sidebar

### Check Workflow Status
- ✅ **Green checkmark**: Workflow passed
- ❌ **Red X**: Workflow failed
- 🟡 **Yellow dot**: Workflow in progress
- ⏸️ **Gray circle**: Workflow skipped

### Debugging Failed Workflows

1. **Go to the workflow run**
   - Click Actions tab
   - Click the failed workflow
   - Click the failed job

2. **Read the logs**
   - Expand each step
   - Look for error messages
   - Note the failing step

3. **Common fixes**:
   - Re-run the workflow (network issues)
   - Fix YAML syntax errors
   - Update secrets if needed
   - Check permissions

## 🎯 Best Practices

### For Repository Maintainers

1. **Monitor CI Workflows**
   - Check PR checks before merging
   - Review security scan results weekly
   - Keep workflows updated via Dependabot

2. **Review PRs Carefully**
   - Ensure CI checks pass
   - Review auto-applied labels
   - Check for security implications

3. **Keep Secrets Secure**
   - Rotate PRIVATE_KEY periodically
   - Don't expose secrets in logs
   - Use minimal permissions

### For Contributors

1. **Before Submitting PRs**
   - Run workflows in your fork
   - Ensure CI checks will pass
   - Include descriptive titles

2. **Respond to CI Failures**
   - Read error messages
   - Fix issues promptly
   - Ask for help if needed

## 🔗 Quick Links

- [All Workflows](../../actions)
- [Workflow Documentation](../workflows/)
- [Setup Guide](../INITIALIZATION.md)
- [Contributing Guide](../CONTRIBUTING.md)
- [Security Policy](../SECURITY.md)

## 📞 Support

If workflows are failing or behaving unexpectedly:

1. Check this dashboard for status
2. Review workflow logs in Actions tab
3. Check [INITIALIZATION.md](INITIALIZATION.md) for setup help
4. Open an issue if problems persist

---

Last Updated: 2026-02-12

This dashboard is automatically updated with each workflow change.
