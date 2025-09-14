# Security Policy

## Supported Versions

We only support the main branch of this repository. Older branches or forks may not receive security updates.

## Reporting a Vulnerability

If you discover a security issue in this repository (such as a vulnerability in a playbook, execution environment definition, or inventory script):

**Do not** open a public GitHub issue. **This could put other users at unecessary risk.**

Instead, please report it privately by emailing: matthias.prel-everex@outlook.com

### Include:

- A description of the issue

- Steps to reproduce (if possible)

- The potential impact

We will acknowledge receipt within 72 hours and provide a timeline for remediation after assessing the issue.

If you are unsure whether something qualifies as a vulnerability, please err on the side of reporting it.

## Preventative Guidance for Contributors

To reduce security risks in contributions:

- Secrets: Never commit passwords, API keys, SSH keys, or tokens. Use Ansible Vault
 or an external secrets manager.

- Logging: Use no_log: true for tasks handling sensitive values.

- Modules: Prefer Ansible modules over shell or command to reduce injection risks.

- Privilege Escalation: Only use become: true when absolutely required, and document why.

- Dependencies: Pin versions in requirements.yml and container definitions; avoid unverified or unmaintained roles/collections.

- Linting: Run ansible-lint and yamllint before submitting pull requests.

- Reviews: All pull requests must be peer-reviewed and must pass automated checks (linting, secret scanning, vulnerability scanning).

## Responsible Disclosure

We request that you give us a reasonable opportunity to remediate before publicly disclosing any security issue. Coordinated disclosure helps keep users safe. 

### Publicly disclosing any security issue significantly harms users.
