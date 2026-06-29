# Funding And Sustainability

PayRails is intended to have a free, open-source core. The project can still
accept funding and offer paid services or premium products so development,
maintenance, security work, documentation, and bank adapter research are
sustainable.

## Goals

- Keep the essential payroll coordination toolkit available as open source.
- Fund ongoing development of the free core.
- Make it possible to pay for convenience, support, hosting, and custom work.
- Be transparent about what is free, what is paid, and why.
- Avoid creating pressure to make unsafe banking, payroll, tax, or compliance
  claims.

## Free Core Commitment

The free core should include the primitives needed for self-hosted use:

- Worker payment profile collection.
- Direct deposit authorization records.
- Pay run setup, approval, and audit history.
- Pay stub generation.
- Generic ACH/NACHA export.
- Generic CSV or bank export support where practical.
- Bank adapter interfaces and documented adapter examples.
- File hash, confirmation, failed payment, and return tracking.
- Security and privacy documentation.

## Donation And Sponsorship Path

The project may add donation or sponsorship links once an official destination is
set up. Good options to evaluate include GitHub Sponsors, Open Collective,
Stripe payment links, or another transparent donation channel.

Before adding a donation link:

- Decide who receives and manages the funds.
- Document how funds support development and maintenance.
- Add the official link to the README and, where appropriate, `.github/FUNDING.yml`.
- Avoid collecting payroll, bank, tax, or worker data through donation forms.

## Paid Or Premium Options

Potential paid offerings:

- Hosted PayRails for organizations that do not want to self-host.
- Setup and migration support.
- Custom bank adapter development.
- Advanced bank automation where officially supported by the bank.
- Team management, advanced reporting, or organization-level workflow features.
- Accountant, payroll, or compliance review services through qualified partners.

Paid offerings should help fund both the paid product and the free open-source
core.

## Guardrails

- Do not make the basic self-hosted payroll/direct-deposit workflow unusable
  without paying.
- Do not hide required security fixes behind a paid plan.
- Do not imply that paying for PayRails makes it a bank, payment processor, tax
  filing service, legal advisor, or accountant.
- Do not use customer payroll or bank data in public demos, fixtures, issues, or
  marketing without a separate reviewed process and explicit permission.
- Keep pricing, donation, and sponsorship messaging separate from compliance
  claims.

## Open Questions

- Which donation or sponsorship platform should be used first?
- Should premium features live in the same repository, separate repositories, or
  a hosted service?
- What minimum free-core feature set should be protected before paid features
  are introduced?
- What governance model should decide funding priorities?
