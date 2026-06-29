# PayRails Roadmap

This roadmap tracks the work that is clearly in scope for the open-source core.
It does not imply that PayRails is ready for real payroll, tax filing, or bank
submission.

## Phase 0: Research And Specs

- Define the core data model for organizations, workers, payment profiles, pay
  periods, pay runs, pay stubs, bank adapters, exports, and audit records.
- Document security requirements for bank account data, encryption, masking,
  access control, deletion, and retention.
- Gather generic ACH/NACHA requirements from public documentation.
- Gather Regions-specific setup and export requirements from public or
  customer-provided non-secret documentation.
- Define synthetic test fixture rules for ACH/NACHA validation.
- Define the static ES module architecture, package boundaries, and dependency
  rules before scaffolding application code.
- Define the donation, sponsorship, and premium offering boundaries that can
  fund development without weakening the open-source core.

## Phase 1: Core Pay Run And Pay Stub Engine

- Draft worker payment destination records.
- Draft pay period and pay run approval flows.
- Generate pay stub data and PDFs from synthetic data.
- Produce owner/accountant export summaries.
- Track pay run status, approvals, file hashes, and audit events.

## Phase 2: ACH/NACHA Export

- Implement generic NACHA file generation.
- Add deterministic validation and snapshot tests with synthetic data.
- Add a Regions-compatible adapter only after the rules are documented.
- Track generated file hashes and export metadata.
- Document manual bank upload boundaries.

## Phase 3: Bank Setup Guides

- Add a bank adapter registry.
- Add generic NACHA setup guidance.
- Add Regions setup guidance where accurate and supportable.
- Track cutoff, limit, return, prenote, and notification notes by adapter.

## Phase 4: Browser Extension Assistant

- Define the approved pay run payload shape.
- Require owner review before any assisted submission step.
- Stop on MFA, CAPTCHA, unexpected bank portal screens, or portal changes.
- Capture confirmation evidence without storing bank credentials.

## Phase 5: Machine-To-Machine Adapters

- Add SFTP, host-to-host, or API adapters only for banks that officially support
  those methods for the organization.
- Keep credentials, certificates, and secrets out of the repository.
- Add retries, status polling, failure alerts, and audit records.

## Phase 6: Tax And Annual Document Support

- Research payroll tax worksheet exports.
- Draft W-2 and 1099 data models separately from payment export logic.
- Require accountant, payroll, and compliance review before production claims.
