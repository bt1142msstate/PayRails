# PayRails

PayRails is a free, open-source payroll and direct-deposit coordination toolkit
for organizations that need bank-ready files, pay stubs, approval workflows, and
clear setup guidance without being locked into expensive payroll software.

The first users are expected to be small organizations with practical payroll
coordination needs, but the long-term goal is broader: PayRails should be
architected so organizations of any size can adopt, extend, self-host, or build
on it.

## Project Status

PayRails is currently in the planning and specification phase. This repository
contains the public scope, roadmap, contribution guidance, and security
boundaries for the initial implementation.

No production payroll, tax filing, or bank-submission code exists yet. Do not use
this repository to process real payroll, store real worker bank details, or file
tax documents.

## Repository Contents

- [README.md](README.md): product vision, scope, and phased plan.
- [docs/roadmap.md](docs/roadmap.md): near-term open-source roadmap.
- [docs/compliance-boundaries.md](docs/compliance-boundaries.md): banking,
  payroll, privacy, and tax boundaries for contributors.
- [docs/adapter-model.md](docs/adapter-model.md): first draft of the bank and
  payment rail adapter model.
- [docs/architecture.md](docs/architecture.md): static ES module and modularity
  principles for the first implementation.
- [docs/sustainability.md](docs/sustainability.md): donation, sponsorship, and
  paid offering principles.
- [CONTRIBUTING.md](CONTRIBUTING.md): how to contribute safely.
- [SECURITY.md](SECURITY.md): how to report security concerns and handle
  sensitive payroll/bank data.
- [LICENSE](LICENSE): MIT license.

## Important Boundaries

PayRails is not a bank, money transmitter, payment processor, payroll tax filing
service, or legal/accounting advisor. The project should help organizations
prepare, validate, document, and export payroll payment instructions that they
submit through their own approved banking channels.

Never commit secrets, bank credentials, worker bank details, payroll files, tax
forms, or other private payroll data to this repository.

## Mission

Build a free, open-source payroll and direct-deposit coordination toolkit that
helps organizations pay people without being locked into expensive payroll
software when they need bank-ready files, pay stubs, approval workflows, and
clear setup guidance.

This is a general-purpose project, not an afterschool-specific module. It should
be usable by small businesses, nonprofits, churches, education programs,
creators, local service businesses, community groups, and other organizations
that need a practical payroll/direct-deposit workflow.

The initial product should stay especially approachable for small organizations,
because they are often the most underserved by payroll tooling. That should not
mean hard-coding small-organization assumptions into the data model,
architecture, permissions, audit model, or adapter system.

The goal is to make the software layer around payroll and direct deposit as open
and affordable as possible while still respecting that banks, payment rails,
taxes, and compliance rules exist.

## Core Idea

The project should not try to become a bank or hold money. It should help an
organization generate accurate payment instructions and records that flow
through the organization's own bank or approved payment channel.

The first practical target is:

1. A worker enters direct deposit information and signs an authorization.
2. Owner/admin reviews approved hours or pay.
3. The system generates pay stubs and a bank-ready payment file.
4. The owner uploads or sends the file through their bank.
5. The system records confirmation, totals, status, and audit history.

Later, where a bank supports it, the system can automate the upload through
SFTP, host-to-host file transfer, a bank API, or a browser extension assistant.

## What The Free/Open Core Should Include

- Worker direct deposit profile collection.
- Direct deposit authorization records.
- Pay run setup and approval.
- Hourly, salary, reimbursement, bonus, and adjustment support.
- Gross pay, deductions, taxes/withholding fields, net pay, and year-to-date
  totals.
- Pay stub PDF generation.
- ACH/NACHA file generation for United States banks.
- Generic CSV/bank export formats where supported.
- Bank adapter system for bank-specific requirements.
- Audit logs for who approved, generated, changed, exported, or submitted a pay
  run.
- Confirmation number and file hash tracking.
- Failed/returned payment tracking.
- Owner/accountant review exports.
- Future W-2/payroll tax export helpers.

## Architecture Direction

The first implementation should use static ES modules for JavaScript and
TypeScript code. Core packages should expose explicit `import` and `export`
boundaries, avoid CommonJS, and keep dynamic loading out of the domain layer.

PayRails should optimize for low coupling and high modularity:

- Domain logic should not import app, database, bank portal, PDF renderer,
  hosted-service, or premium-product code.
- Bank and payment rail differences should live behind adapter interfaces.
- Infrastructure should depend on the core; the core should not depend on
  infrastructure.
- Public package exports should be intentional and narrow.
- Tests should be able to exercise core payroll, pay stub, validation, audit,
  and export behavior with synthetic fixtures and without live bank services.

See [docs/architecture.md](docs/architecture.md) for the implementation
principles.

## What This Should Not Do At First

- Do not hold organization funds.
- Do not act as a bank or payment processor.
- Do not store bank portal usernames or passwords.
- Do not commit secrets, bank data, worker bank details, or payroll files to
  GitHub.
- Do not promise full payroll tax filing accuracy until that layer has its own
  review, tests, documentation, and accountant/payroll validation.

## Bank Adapter Model

The project should be built around bank adapters.

Each bank profile should define:

- Supported submission methods:
  - manual upload
  - NACHA file export
  - CSV export
  - browser extension upload assistant
  - SFTP
  - host-to-host file transfer
  - bank API
- Required bank services to enable.
- File format rules.
- Cutoff times.
- Batch limits.
- Per-entry limits.
- Return and notification handling.
- Test or prenote requirements.
- Known bank fees when publicly available.
- Setup instructions and contact wording.

Potential initial adapters:

- `generic-nacha-export`
- `regions-nacha-export`
- `regions-manual-upload-guide`
- `csv-export`
- `browser-extension-upload-assist`

Future adapters:

- `regions-sftp`
- `regions-api`
- `chase-nacha-upload`
- `bank-of-america-cashpro`
- `wells-fargo-api`
- international bank/payment-rail adapters

## Regions First Path

The first real bank target can be Regions because it is the first known bank
needed by an early user.

The initial Regions path should likely be:

1. Generate a Regions-compatible NACHA file.
2. Give the owner a clear upload guide for Regions business/treasury banking.
3. Record the upload confirmation manually.
4. Later, investigate whether Regions can enable SFTP, host-to-host, API, or
   another machine-to-machine file transmission method for the account.

This lets the project work before any bank partnership exists.

## Automation Levels

The system should support multiple automation levels so organizations can choose
what is safe for them.

### Level 1: Manual Export

- Generate ACH/NACHA file.
- Owner downloads it.
- Owner uploads it to bank portal.
- Owner records confirmation.

### Level 2: Guided Upload

- Generate ACH/NACHA file.
- Show exact bank-specific upload steps.
- Validate totals before export.
- Prompt owner to enter confirmation after upload.

### Level 3: Browser Extension Assistant

- Extension runs in the owner's browser.
- Owner is already signed in to their bank.
- Extension helps upload/fill the bank portal where allowed.
- Owner reviews and clicks submit.
- Extension captures confirmation evidence.

### Level 4: Assisted Submit

- Extension or local agent uploads the file and submits after owner approval.
- It stops if MFA, CAPTCHA, unexpected screens, or portal changes appear.
- It records confirmation evidence back to the app.

### Level 5: Machine-To-Machine Submit

- Uses SFTP, host-to-host file transmission, or bank API.
- Requires bank enablement.
- Can be scheduled after owner approval.
- Should include strong validation, audit logs, retry rules, and failure alerts.

## Global Direction

ACH/NACHA is United States-specific. The project should be designed so other
countries can add their own payment rail adapters later.

Examples of future rails or adapter families:

- ACH/NACHA for the United States.
- Bank-specific file upload formats.
- SEPA-style exports where legally and technically appropriate.
- Country-specific payroll bank file formats.
- Local bank API adapters.

The core concepts should stay the same:

- employer/organization owns the bank relationship
- project generates validated payment instructions
- user approves before money movement
- secrets and bank data stay out of GitHub
- audit history is preserved

## Pay Stubs And Payroll Documents

Pay stubs should be part of the early product because they are a natural output
of approved pay runs.

Pay stub fields should include:

- employee name and masked account/payment destination
- pay period
- pay date
- hours and rates
- gross pay
- deductions
- taxes/withholding fields
- employer contributions where applicable
- net pay
- year-to-date totals
- pay run ID and confirmation references

W-2, 1099, payroll tax worksheets, and filing exports should be phased in later.
They are possible, but they need much heavier validation and review than basic
pay stubs.

## Security And Privacy Principles

- Encrypt worker bank details at rest.
- Use masked display values in UI and logs.
- Keep full bank account numbers out of routine reads.
- Use least-privilege access controls.
- Require owner/admin approval for pay runs.
- Require multi-step confirmation for exports/submission.
- Store hashes and metadata for exported payment files.
- Keep bank portal credentials out of the system when possible.
- Use customer-owned bank accounts and customer-owned bank access.
- Never store payroll files or secrets in a public GitHub repo.
- Make deletion, retention, and export rules explicit.

## Potential Product Shape

This can be both:

1. A standalone open-source GitHub project.
2. A reusable module inside larger organization-management platforms.

## Funding And Sustainability

PayRails should be free and open-source at its core, but it also needs a
realistic path to fund ongoing development, maintenance, security review,
documentation, and bank adapter work.

Possible sustainability paths:

- Donations or sponsorships from users, organizations, and supporters.
- Optional paid setup support for organizations that want help getting started.
- Optional custom bank adapter development.
- Optional hosted or managed version for organizations that do not want to
  self-host.
- Optional premium features that fund both the premium product and the free
  open-source core.
- Optional accountant, payroll, or compliance review services through partners
  later.

The free core should continue to include the essential payroll coordination,
pay stub, export, adapter, and audit primitives needed for self-hosted use. Paid
offerings should focus on convenience, hosting, support, advanced automation,
customization, and services rather than locking away the basic ability to run a
payroll/direct-deposit workflow.

See [docs/sustainability.md](docs/sustainability.md) for the current funding
principles.

## Early Build Phases

### Phase 0: Research And Specs

- Gather Regions NACHA requirements.
- Gather generic NACHA file requirements.
- Decide data model for worker payment profiles, pay runs, pay stubs, and bank
  adapters.
- Identify security requirements for storing bank account data.
- Define what the module will and will not do.

### Phase 1: Core Pay Run And Pay Stub Engine

- Worker profile payment destination.
- Pay period setup.
- Pay run draft and approval.
- Pay stub PDF generation.
- Export summary for owner/accountant review.

### Phase 2: ACH/NACHA Export

- Generic NACHA export.
- Regions-compatible NACHA export.
- File validation.
- File hash and audit record.
- Manual upload confirmation tracking.

### Phase 3: Bank Setup Guides

- Bank selector.
- Regions setup guide.
- Generic NACHA upload guide.
- Bank capability profiles.
- Cutoff/limits/return handling notes.

### Phase 4: Browser Extension Assistant

- Securely receive approved pay run payload.
- Open or assist with bank portal upload where allowed.
- Require review before submit.
- Capture confirmation evidence.
- Report success/failure back to the app.

### Phase 5: Machine-To-Machine Adapters

- Add SFTP/host-to-host/API adapters only where banks officially support them.
- Keep each bank adapter isolated.
- Add retry, status polling, alerting, and audit records.

### Phase 6: Tax And Annual Document Support

- Payroll tax worksheet exports.
- W-2 data generation.
- W-2 PDF generation.
- SSA/IRS/state filing export research.
- Accountant/payroll validation before production claims.

## First Questions For The New Codex Project

- Should the first implementation be plain TypeScript, Firebase-based, or a
  framework-neutral package plus optional Firebase adapter?
- What exact data model should represent worker payment profiles and pay runs?
- What encryption approach should be used for account and routing numbers?
- How should NACHA files be tested without real bank submission?
- What should the Regions adapter validate beyond generic NACHA?
- What parts should be reusable globally versus US-only?
- What disclaimers and documentation are needed so users understand the tool is
  not itself a bank or payroll tax filing service?
