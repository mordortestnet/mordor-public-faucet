# Security Policy

## Supported Versions

This project is focused on the Ethereum Classic Mordor testnet. As this is a testnet faucet system, security updates are provided for the latest version only.

| Version | Supported          |
| ------- | ------------------ |
| Latest  | :white_check_mark: |
| Older   | :x:                |

## 🔐 Security Considerations

### This is a Testnet Project

**Important:** This project is designed for the **Ethereum Classic Mordor testnet only**. It handles testnet tokens with no real-world value. However, we still take security seriously to protect user privacy and maintain best practices.

### What We Protect

- ✅ **Private Key Security** - Keys stored in GitHub Secrets
- ✅ **Workflow Security** - Validated inputs and safe execution
- ✅ **Code Security** - Regular dependency updates
- ✅ **Access Control** - Proper GitHub permissions

### What You Should Know

- 🔑 **Never use mainnet private keys** with this project
- 🔑 **GitHub Secrets are encrypted** but only as secure as your GitHub account
- 🔑 **Workflow logs are public** - never log sensitive data
- 🔑 **Fork carefully** - your fork's secrets are separate from upstream

## 🚨 Reporting a Vulnerability

We take security seriously. If you discover a security vulnerability, please follow these steps:

### For Critical Issues

**DO NOT** create a public GitHub issue for security vulnerabilities.

Instead:

1. **Use GitHub's Private Vulnerability Reporting**:
   - Go to the Security tab
   - Click "Report a vulnerability"
   - Fill out the advisory form

2. **Or Email the Maintainers**:
   - Email: [Insert maintainer email here]
   - Subject: "Security Vulnerability in Mordor Faucet"
   - Include detailed description and reproduction steps

### What to Include

When reporting a security issue, please include:

- **Description** - What is the vulnerability?
- **Impact** - What could an attacker do?
- **Steps to Reproduce** - How can we verify it?
- **Suggested Fix** - If you have ideas (optional)
- **Your Contact Info** - How can we reach you?

### Response Timeline

- **Initial Response**: Within 48 hours
- **Status Update**: Within 1 week
- **Fix Timeline**: Depends on severity
  - Critical: As soon as possible
  - High: Within 1 week
  - Medium: Within 2 weeks
  - Low: Next scheduled update

## 🛡️ Security Best Practices

### For Users

1. **Use Testnet Keys Only**
   - Never use mainnet private keys
   - Create dedicated testnet wallets

2. **Secure Your GitHub Account**
   - Enable 2FA (two-factor authentication)
   - Use strong, unique passwords
   - Review authorized apps regularly

3. **Protect Your Secrets**
   - Never share GitHub Secret values
   - Don't commit secrets to repositories
   - Rotate keys if compromised

4. **Fork Safely**
   - Your fork is separate from upstream
   - Configure your own secrets
   - Don't expose secrets in public forks

### For Contributors

1. **Code Security**
   - Never hardcode private keys
   - Always use environment variables
   - Validate all inputs
   - Handle errors safely

2. **Workflow Security**
   - Use minimal permissions
   - Don't expose secrets in logs
   - Validate PR inputs
   - Review third-party actions

3. **Dependencies**
   - Keep dependencies updated
   - Review dependency changes
   - Check for known vulnerabilities
   - Use specific versions, not `latest`

4. **Testing**
   - Test with testnet only
   - Never test with real funds
   - Verify workflow behavior
   - Check logs for leaks

## 🔍 Security Features

### Current Security Measures

1. **GitHub Secrets**
   - Private keys stored encrypted
   - Never exposed in logs
   - Access controlled by GitHub

2. **Workflow Validation**
   - Input validation in workflows
   - Safe error handling
   - Minimal permissions

3. **Dependency Management**
   - Dependabot for updates
   - Regular security audits
   - Pinned action versions

4. **Access Control**
   - PR approval requirements
   - Protected branches
   - Required reviews

### Planned Improvements

- [ ] Add automated security scanning (CodeQL)
- [ ] Implement workflow signing
- [ ] Add rate limiting for faucet requests
- [ ] Enhanced audit logging
- [ ] Additional input validation

## 📋 Security Checklist

Before deploying or forking:

- [ ] GitHub account has 2FA enabled
- [ ] Using testnet-only private keys
- [ ] Secrets configured in GitHub Settings
- [ ] Workflows are reviewed and understood
- [ ] Repository visibility is appropriate
- [ ] Branch protection rules configured
- [ ] Collaborator access is minimal

## 🔗 Security Resources

### External Resources

- [GitHub Security Best Practices](https://docs.github.com/en/code-security)
- [GitHub Actions Security](https://docs.github.com/en/actions/security-guides)
- [Ethereum Security](https://ethereum.org/en/security/)
- [ETC Security Best Practices](https://ethereumclassic.org/security)

### Tools We Use

- **Dependabot** - Automated dependency updates
- **Gitleaks** - Secret scanning
- **GitHub Secret Scanning** - Built-in secret detection
- **npm audit** - Dependency vulnerability checking

## 📞 Contact

For security-related questions or concerns:

- **Security Issues**: Use private vulnerability reporting
- **General Security Questions**: Open a GitHub Discussion
- **Urgent Matters**: Contact maintainers directly

## 🏆 Recognition

We appreciate security researchers who responsibly disclose vulnerabilities. Contributors who report valid security issues will be:

- Credited in the security advisory (if desired)
- Mentioned in release notes
- Added to our security acknowledgments

## 📜 Disclosure Policy

We follow responsible disclosure:

1. **Private Report** - You report the issue privately
2. **Acknowledgment** - We confirm receipt within 48 hours
3. **Fix Development** - We work on a fix
4. **Fix Release** - We release the fix
5. **Public Disclosure** - We publish advisory (with your permission)

Typical timeline: 30-90 days from report to public disclosure.

## ⚖️ Legal

This project is provided "as is" without warranty. Users accept all risks. This is educational/testnet software only.

---

Last Updated: 2026-02-12

Thank you for helping keep Mordor Public Faucet secure! 🔒
