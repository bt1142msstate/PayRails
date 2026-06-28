# Security Policy

PayRails deals with payroll and bank-payment workflows, so security issues are
high impact even while the project is early-stage.

## Do Not Share Sensitive Data Publicly

Do not open public issues, pull requests, comments, screenshots, logs, or
attachments containing:

- Real bank account or routing numbers.
- Worker names paired with payroll, pay stub, tax, or bank details.
- Bank portal credentials, API keys, tokens, certificates, or private keys.
- Generated ACH/NACHA files or bank upload files from real organizations.
- Tax forms, payroll registers, or personally identifiable payroll records.

Use synthetic fixtures for examples and tests.

## Reporting A Vulnerability

If GitHub private vulnerability reporting is enabled for this repository, use
that path first. Otherwise, open a minimal public issue that describes the
affected area without including exploit details or sensitive data, and ask for a
private contact path.

Expected response goals:

- Acknowledge the report.
- Confirm whether the issue is reproducible.
- Patch or document mitigation steps.
- Credit the reporter when appropriate and requested.

## Supported Versions

There are no production releases yet. Security fixes apply to the main branch
until versioned releases begin.
