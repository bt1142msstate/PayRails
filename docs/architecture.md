# Architecture Principles

PayRails should be built as a set of small, explicit modules with a stable core
and replaceable adapters. The architecture should make payroll rules, pay run
state, pay stub generation, audit behavior, and export validation testable
without live bank systems or hosted infrastructure.

## Static ES Modules

All JavaScript and TypeScript implementation code should use static ES modules:

- Use `import` and `export` syntax.
- Use `type: "module"` for package manifests.
- Prefer explicit named exports.
- Avoid CommonJS `require`, `module.exports`, and mixed module formats.
- Avoid dynamic `import()` in core domain packages.
- Allow dynamic loading only at documented extension boundaries, such as an
  optional plugin host, browser extension entrypoint, or deployment-specific
  integration layer.
- Keep package entrypoints explicit through `exports` maps once packages exist.

Static ESM keeps the dependency graph analyzable, improves compatibility with
modern TypeScript tooling, supports tree-shaking, and makes unwanted coupling
easier to detect.

## Dependency Direction

The dependency direction should stay one way:

1. Domain core defines entities, value objects, validation rules, pay run state,
   pay stub data, audit events, and abstract ports.
2. Feature packages depend on the core to implement export, document, or
   workflow behavior.
3. Adapters depend on core contracts and feature package contracts.
4. Apps, CLIs, hosted services, browser extensions, and premium products compose
   the core, features, and adapters.

The core must not import application frameworks, databases, bank SDKs, PDF
renderers, browser automation, hosted-service code, commercial licensing code,
or bank-specific adapters.

## Suggested Package Boundaries

The first implementation should start with a small number of packages and add
new packages only when there is a real dependency boundary:

- `core`: shared domain models, pay run state, money/date helpers, validation
  primitives, audit contracts, and port definitions.
- `pay-stubs`: pay stub data shaping and renderer contracts.
- `ach-nacha`: generic ACH/NACHA file generation and validation using synthetic
  fixtures.
- `adapters`: adapter contracts, registry helpers, and generic adapters.
- `bank-adapters/*`: concrete bank-specific adapters such as Regions when
  requirements are documented.
- `fixtures`: synthetic test data that is safe to commit.
- `apps/*`: UI, CLI, hosted, or browser extension compositions.

Package boundaries can change as the project learns, but coupling should not
flow from core logic into infrastructure.

## Low Coupling Rules

- Pass dependencies through explicit parameters, constructors, or factory
  functions instead of global singletons.
- Keep side effects at the edges: file IO, database IO, network calls, browser
  automation, and bank transmission code should not live inside core domain
  logic.
- Model payment rails and bank capabilities as data and interfaces before adding
  concrete integrations.
- Keep premium, hosted, and partner-service code outside the free core's domain
  logic.
- Prefer small modules with one reason to change.
- Prefer stable data contracts over importing implementation details across
  package boundaries.
- Avoid circular dependencies.

## High Modularity Rules

- Keep payroll calculation, pay run workflow, pay stub shaping, file export,
  adapter validation, audit logging, and confirmation tracking separable.
- Make each bank adapter independently testable with synthetic fixtures.
- Make country-specific payment rail logic replaceable.
- Keep UI and storage choices replaceable by depending on ports from the core.
- Export public APIs intentionally; do not expose internal folders as public
  contracts by accident.

## Testing Expectations

Core and adapter tests should run with synthetic data and no live bank access.
At minimum, early implementation should support:

- Unit tests for pay run state transitions and validations.
- Snapshot or golden-file tests for generated pay stub data and ACH/NACHA files.
- Contract tests for adapter capability metadata and validation output.
- Import graph checks that fail on circular dependencies or forbidden imports
  from core to infrastructure.
- Fixture checks that prevent real payroll, bank, tax, credential, or personal
  data from entering tests.

## Review Checklist

Before merging implementation code, reviewers should ask:

- Does this code use static ESM?
- Does the dependency direction still point inward toward the core?
- Can the domain behavior be tested without live infrastructure?
- Are bank-specific rules isolated behind adapters?
- Are public exports intentional?
- Is sensitive payroll or bank data excluded from examples, tests, logs, and
  fixtures?
