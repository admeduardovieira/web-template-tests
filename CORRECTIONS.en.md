# CORRECTIONS.md — web-template-tests

Project: better-care/web-template-tests
Base branch analyzed: master
Destination fork: https://github.com/admeduardovieira/web-template-tests

## Corrections implemented

| ID | Title | Severity | Status | Risk | Files involved |
|----|-------|----------|--------|------|----------------|
| REA-webtemplate-001 | README.md: malformed XML tags in Maven dependency examples | P2 | IMPLEMENTED | Low | `README.md` |
| REA-webtemplate-002 | No maven-surefire-plugin in pom.xml | P3 | NOT IMPLEMENTED | Low | `pom.xml` |
| REA-webtemplate-003 | No CI workflow configured | P3 | NOT IMPLEMENTED | Low | `.github/workflows/` (new) |

## Details of implemented corrections

### REA-webtemplate-001 — Malformed XML tags in README
**Problem:** README.md contained Maven dependency examples with `></version>` instead of `</version>`, making copy-paste examples invalid XML.
**Fix:** Corrected all 4 occurrences in JUnit and TestNG dependency blocks.
**Validation:** Visual inspection confirms all `></version>` patterns replaced with `</version>`.

## Corrections not implemented

### REA-webtemplate-002 — No maven-surefire-plugin
Not implemented: requires understanding of intended test execution configuration. Suggested: add maven-surefire-plugin with junit-platform provider.

### REA-webtemplate-003 — No CI workflow
Not implemented: requires understanding of desired CI scope. Suggested: add build.yml for Maven test execution.

## Publication plan
- Fork: `admeduardovieira/web-template-tests` (created).
- Branch `fix/rea-webtemplate-001-003` for corrections.
- Commit identity: `admeduardovieira <admeduardovieira@users.noreply.github.com>`.
- PR #1: https://github.com/better-care/web-template-tests/pull/1 (open, base master).
