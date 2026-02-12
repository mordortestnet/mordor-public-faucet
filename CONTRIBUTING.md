# Contributing to Mordor Public Faucet

Thank you for your interest in contributing to the Mordor Public Faucet project! This document provides guidelines and instructions for contributing.

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have:
- A GitHub account
- Basic understanding of GitHub Actions
- Familiarity with Ethereum Classic and the Mordor testnet
- Node.js 20+ (for local testing)

### Setting Up Your Fork

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/mordor-public-faucet.git
   cd mordor-public-faucet
   ```
3. **Add the upstream remote**:
   ```bash
   git remote add upstream https://github.com/mordortestnet/mordor-public-faucet.git
   ```
4. **Enable GitHub Actions** in your fork (Actions tab → Enable workflows)

## 📋 Types of Contributions

We welcome various types of contributions:

### 🐛 Bug Fixes
- Fix issues in existing workflows
- Correct documentation errors
- Improve error handling

### ✨ New Features
- Add new workflow capabilities
- Enhance existing functionality
- Improve user experience

### 📚 Documentation
- Improve existing documentation
- Add examples and tutorials
- Translate documentation

### 🧪 Testing
- Add workflow tests
- Improve validation
- Test edge cases

## 🔧 Development Workflow

### 1. Create a Branch

Create a descriptive branch for your work:
```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/bug-description
```

### 2. Make Your Changes

- **Keep changes focused** - One feature or fix per PR
- **Follow existing patterns** - Match the style of existing workflows
- **Test your changes** - Ensure workflows work as expected
- **Update documentation** - Keep docs in sync with code changes

### 3. Test Your Changes

For workflow changes:
1. Enable the workflow in your fork
2. Test it manually using `workflow_dispatch`
3. Verify the output in the Actions tab
4. Check for any errors or warnings

For documentation:
1. Preview markdown files locally
2. Check for broken links
3. Verify formatting

### 4. Commit Your Changes

Write clear, descriptive commit messages:
```bash
git add .
git commit -m "feat: add new distribution workflow"
# or
git commit -m "fix: correct gas estimation in wrap workflow"
# or
git commit -m "docs: update README with new examples"
```

**Commit message format:**
- `feat:` - New features
- `fix:` - Bug fixes
- `docs:` - Documentation changes
- `chore:` - Maintenance tasks
- `refactor:` - Code refactoring
- `test:` - Testing improvements

### 5. Push and Create Pull Request

```bash
git push origin your-branch-name
```

Then create a Pull Request on GitHub with:
- **Clear title** describing the change
- **Detailed description** of what and why
- **Link to related issues** (if applicable)
- **Screenshots** (for UI/output changes)

## 📝 Pull Request Guidelines

### PR Checklist

Before submitting your PR, ensure:
- [ ] Code follows existing patterns and style
- [ ] All workflows are tested and working
- [ ] Documentation is updated (if needed)
- [ ] Commit messages are clear and descriptive
- [ ] PR description explains the changes
- [ ] No secrets or private keys are committed
- [ ] CI checks pass

### PR Review Process

1. **Automated checks** run on your PR (CI/CD workflows)
2. **Maintainer review** - We'll review your changes
3. **Feedback** - Address any requested changes
4. **Approval** - Once approved, we'll merge your PR
5. **Thanks!** - Your contribution is appreciated 🎉

## 🔐 Security Considerations

### DO:
- ✅ Use GitHub Secrets for sensitive data
- ✅ Validate all user inputs
- ✅ Follow least-privilege principle
- ✅ Document security implications
- ✅ Report security issues privately

### DON'T:
- ❌ Commit private keys or secrets
- ❌ Expose sensitive data in logs
- ❌ Skip input validation
- ❌ Use overly permissive workflow permissions
- ❌ Ignore security warnings

### Reporting Security Issues

**DO NOT** open public issues for security vulnerabilities.

Instead, please email security concerns to the maintainers or use GitHub's private vulnerability reporting feature.

## 🧪 Testing Workflows

### Manual Testing

1. **Fork the repository** (if you haven't already)
2. **Add required secrets** to your fork:
   - `PRIVATE_KEY` - Your test wallet private key
3. **Enable workflows** in your fork
4. **Trigger workflows** manually:
   - Go to Actions tab
   - Select the workflow
   - Click "Run workflow"
   - Provide required inputs
5. **Verify results** in the workflow logs

### Testing PR-based Workflows

1. Create a test PR in your fork
2. Add a wallet address in the PR description
3. Monitor the workflow execution
4. Verify the validation and approval process

## 📚 Resources

### Documentation
- [README.md](README.md) - Main documentation
- [QUICKSTART.md](QUICKSTART.md) - Quick start guide
- [PR_DISTRIBUTION_GUIDE.md](PR_DISTRIBUTION_GUIDE.md) - PR distribution guide
- [SYSTEM_OVERVIEW.md](SYSTEM_OVERVIEW.md) - System architecture

### External Resources
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Ethers.js Documentation](https://docs.ethers.org/)
- [Mordor Testnet Info](https://github.com/etclabscore/mordor)
- [ETC Block Explorer](https://etc-mordor.blockscout.com/)

## 💬 Communication

### Asking Questions
- Open a GitHub Discussion for general questions
- Open an Issue for bug reports or feature requests
- Comment on existing Issues/PRs for clarification

### Getting Help
If you need help with your contribution:
1. Check existing documentation
2. Search existing Issues/Discussions
3. Ask in GitHub Discussions
4. Reach out to maintainers

## 🏷️ Issue Labels

We use labels to organize issues:
- `bug` - Something isn't working
- `enhancement` - New feature or request
- `documentation` - Documentation improvements
- `good first issue` - Good for newcomers
- `help wanted` - Extra attention needed
- `security` - Security-related issues
- `workflows` - GitHub Actions workflow changes
- `catacomb` - Related to Catacomb multisig

## 📜 Code of Conduct

Be respectful and inclusive:
- Use welcoming and inclusive language
- Be respectful of differing viewpoints
- Accept constructive criticism gracefully
- Focus on what's best for the community
- Show empathy towards other contributors

## 🎯 Project Goals

Keep in mind our project goals:
- **Simplicity** - Easy to use and understand
- **Security** - Safe handling of private keys and transactions
- **Reliability** - Workflows should work consistently
- **Documentation** - Clear and comprehensive docs
- **Community** - Support ETC Mordor testnet users

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

Thank you for contributing to Mordor Public Faucet! 🚀
