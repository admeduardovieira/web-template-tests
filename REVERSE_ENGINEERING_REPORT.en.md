# REVERSE_ENGINEERING_REPORT — web-template-tests

## A. General diagnosis

### Architecture identified
Java/Maven test library for WebTemplate (EHR compositions) from Better Platform. Provides interfaces and utilities to convert compositions between RAW, FLAT and STRUCTURED formats, and to validate them against templates. Structure:

- `src/main/java/care/better/platform/web/template/`: main interfaces (CompositionConverter, WebTemplateProvider, CompositionValidator) and base classes (AbstractWebTemplateTest, CompositionBuilderContextKey, ValidationErrorDto, WebTemplateTestExtension)
- `src/test/java/`: ~60 JUnit 5 test classes for conversion and validation scenarios
- `pom.xml`: Maven project (Java 1.8, Jackson 2.11.3, JUnit 5.6.3, AssertJ 3.17.2)
- `README.md`: configuration documentation for consumer projects

### Technologies and dependencies
- Java 1.8
- Maven
- Jackson 2.11.3, JUnit 5.6.3, AssertJ 3.17.2, Google Collections 1.0, Commons IO 2.8.0
- Packages as test-jar (maven-jar-plugin test-jar goal)

### Maintenance status
Last active commit. Default branch: master. Repository: https://github.com/better-care/web-template-tests.

### Existing test mechanisms
~60 JUnit 5 tests in `src/test/java/`. No CI workflow (GitHub Actions) configured.

### Investigation limitations
- Maven not installed; tests not executed.
- REA 6.7.0 not operational; static analysis only.

## B. Problems found

| ID | Title | Severity | Status | Location |
|----|-------|----------|--------|----------|
| REA-webtemplate-001 | README.md: malformed XML tags in Maven dependency examples | P2 | CONFIRMED | `README.md:29,35,105,115` |
| REA-webtemplate-002 | No `maven-surefire-plugin` in pom.xml | P3 | CONFIRMED | `pom.xml` |
| REA-webtemplate-003 | No CI workflow configured | P3 | CONFIRMED | absence of `.github/workflows` |

### Confirmed problems details

**REA-webtemplate-001 (P2, CONFIRMED):** The README.md contains Maven dependency examples with malformed closing tags: `${jupiter.version></version>` instead of `${jupiter.version}</version>`. This makes copy-paste examples invalid XML (not well-formed).

Evidence: `README.md:29,35` (JUnit blocks), `README.md:105,115` (TestNG blocks).

**REA-webtemplate-002 (P3, CONFIRMED):** The `pom.xml` configures `maven-compiler-plugin` and `maven-jar-plugin`, but does not declare `maven-surefire-plugin`, required to run JUnit 5 tests via `mvn test`.

**REA-webtemplate-003 (P3, CONFIRMED):** No `.github/workflows` folder — no CI for build, testing or PR verification.

## C. Recurring problems
No recurring public problems found.

## D. Undocumented errors
All items in section B are previously undocumented problems.

## E. Performance
Java test library; no performance-critical operations.

## F. Technical improvements
- Fix malformed XML tags in README (REA-webtemplate-001, implemented)
- Add maven-surefire-plugin to pom.xml (REA-webtemplate-002)
- Add CI workflow (REA-webtemplate-003)

## G. Execution plan
All independent and low risk.

## H. Expected result
Corrected Maven documentation, reproducible builds, CI configured.

**Tools used:** git, gh, PowerShell, static inspection.  
**Limitation:** Maven not installed.  
**Environment:** Windows, PowerShell 5.1, `C:\Users\User\audit-repos\web-template-tests` (clone of upstream, master branch).
