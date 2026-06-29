# Adapter Model

PayRails should isolate bank and payment rail differences behind adapters so the
core payroll workflow can stay consistent.

Adapters should be implemented as static ES modules in JavaScript or TypeScript
packages. The core package should depend only on adapter interfaces and shared
types; concrete bank, file, browser-extension, SFTP, host-to-host, or API
adapters should depend on the core contracts rather than the other way around.

## Core Adapter Responsibilities

Each adapter should define:

- Payment rail or bank family.
- Supported export or submission methods.
- Required organization setup.
- Required fields.
- File format rules.
- Validation rules.
- Cutoff and limit notes.
- Return and notification handling.
- Test or prenote expectations.
- Manual upload guidance, if supported.
- Source and confidence level for bank-specific claims.

## Initial Adapters

- `generic-nacha-export`: United States ACH/NACHA file generation using generic
  rules and synthetic fixtures.
- `csv-export`: generic tabular export for banks or accounting tools that accept
  CSV uploads.
- `regions-nacha-export`: Regions-compatible NACHA output after requirements
  are documented.
- `regions-manual-upload-guide`: setup and manual upload documentation for
  approved Regions business or treasury banking workflows.

## Future Adapters

- Bank-specific SFTP adapters.
- Host-to-host file transfer adapters.
- Bank API adapters.
- Browser extension assisted-upload adapters.
- Non-US payment rail adapters where legally and technically appropriate.

## Adapter Safety Rules

- Keep bank credentials and secrets outside adapter source code.
- Do not store bank portal usernames or passwords in PayRails.
- Keep adapter side effects at the edge so validation and file generation can be
  tested without live bank systems.
- Require explicit owner approval before export or submission.
- Record export hashes, totals, confirmation references, and audit events.
- Stop automated or assisted flows when screens, MFA, CAPTCHA, limits, or
  validation results differ from expectations.
