<!--
  Approval rubric for the docs-auto-approver agent (SecondCloset/agent-hub).

  Every non-heading, non-comment line below is a rule the agent evaluates against the
  PR diff before it approves. Empty this file and the agent approves any in-scope PR on
  its mechanical checks alone.

  Keep rules judgeable from the diff alone. A rule that needs knowledge the diff does
  not carry will fail unpredictably.
-->

# Approval rubric — Parcel API docs

## R-A — No endpoint or field disappears unexplained

`swagger.yml` documents a published API. A PR may add paths, add fields, or reword
descriptions freely. Removing a path, an operation, a parameter, or a response field is
a breaking change for whoever integrates against it: fail unless the PR title or body
says why it is going (endpoint retired, never shipped, corrected because it never
existed).

## R-B — The spec stays well-formed

The diff must leave `swagger.yml` parseable and structurally intact: indentation
consistent with its surroundings, `paths` entries keeping their method / `responses`
shape, `$ref` targets that exist in the file. A truncated block or a dangling `$ref` is
a fail — this repo publishes the spec straight to the docs site.

## R-C — Changed behaviour is described, not just renamed

When a PR changes what an existing field or response means — a type, an enum value, a
required flag — the `description` around it changes with it. A field whose type changes
while its prose still describes the old one is a fail.
