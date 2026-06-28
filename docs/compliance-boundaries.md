# Compliance Boundaries

PayRails should make payroll and direct-deposit workflows clearer and more
affordable, but it must not overstate what an open-source tool can safely do.

## PayRails Is Not

- A bank.
- A money transmitter.
- A payment processor.
- A payroll tax filing service.
- Legal, tax, accounting, or banking advice.
- A replacement for employer obligations, bank agreements, or professional
  review.

## Initial Operating Model

The organization using PayRails owns the bank relationship and payment channel.
PayRails prepares payment instructions, pay stubs, records, validation outputs,
and audit history. The owner or approved admin submits payment files through
their own bank or enabled transmission method.

## Data Handling Rules

- Store full bank account details only when the implementation has reviewed
  encryption, access control, audit, deletion, and retention requirements.
- Show masked payment details in routine UI, logs, exports, and support flows.
- Keep generated bank files and payroll exports out of git.
- Use synthetic data for fixtures, demos, screenshots, tests, and docs.
- Treat audit logs as sensitive because they may reveal payroll behavior.

## Payroll And Tax Boundaries

Pay stubs, payroll tax worksheets, W-2s, 1099s, and filing exports require
separate validation. The project should not claim full tax filing accuracy until
that layer has dedicated tests, documentation, accountant or payroll review, and
clear jurisdiction-specific boundaries.

## Bank Adapter Boundaries

Bank adapters must document their source of truth and uncertainty. A bank
adapter should not claim support for submission methods, cutoff times, limits,
fees, or return behavior unless that information is verified from reliable bank
documentation or a user-provided non-secret source.
