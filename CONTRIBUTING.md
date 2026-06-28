# Contributing To PayRails

PayRails is early-stage. Contributions should keep the project safe,
well-scoped, and honest about what it can and cannot do.

## Good First Contributions

- Improve the public scope and terminology.
- Add research notes for bank file formats and setup requirements.
- Draft data models for worker payment profiles, pay runs, pay stubs, and bank
  adapters.
- Add validation rules and test fixtures that do not contain real payroll or
  bank data.
- Improve security, privacy, audit, and compliance documentation.

## Contribution Rules

- Do not commit real worker data, bank account numbers, routing numbers,
  payroll files, tax forms, bank credentials, API keys, or secrets.
- Use synthetic examples only.
- Keep banking and payroll claims precise. If something needs legal,
  accountant, bank, or compliance review, say so.
- Prefer small pull requests with a clear scope.
- Include tests or validation notes when changing executable code.
- Keep bank-specific logic isolated behind adapter boundaries.

## Local Setup

There is no application code yet. For now, clone the repository and review the
docs:

```sh
git clone https://github.com/bt1142msstate/PayRails.git
cd PayRails
```

Implementation setup instructions will be added after the initial stack is
selected.

## Pull Requests

Before opening a pull request:

1. Confirm no sensitive data is included.
2. Explain the user or contributor impact.
3. Document any validation performed.
4. Call out any unresolved compliance, payroll, tax, or banking assumptions.
