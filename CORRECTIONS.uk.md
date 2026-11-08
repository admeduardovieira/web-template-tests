# CORRECTIONS.md — web-template-tests

Проєкт: better-care/web-template-tests
Базова гał diff гałку для аналізу: master
Гał diff гałку для публікації: https://github.com/admeduardovieira/web-template-tests

## Пропоновані виправлення

| ID | Назва | Середність | Статус | Різик | Задіяні файли |
|----|-------|------------|--------|-------|---------------|
| REA-webtemplate-001 | README.md: пошкоджені теги XML у прикладах залежностей Maven | P2 | PROPOSING | Низький | `README.md` |
| REA-webtemplate-002 | Немає `maven-surefire-plugin` у pom.xml | P3 | PROPOSING | Низький | `pom.xml` |
| REA-webtemplate-003 | Немає workflow CI налаштовано | P3 | PROPOSING | Низький | `.github/workflows/` (новий) |

## Деталі пропонованих виправлень

### REA-webtemplate-001 — Пошкоджені теги XML у README
**Проблема:** README.md містив приклади залежностей Maven з `></version>` замість `</version>`, що робить приклади копіювання та вставки недійсними XML.
**Виправлення:** Виправлено всі 4 випадки у блоках JUnit та TestNG.
**Валідація:** Візуальна перевірка підтверджує, що всі патерни `></version>` замінені на `</version>`.

## Виправлення не реалізовано

### REA-webtemplate-002 — Немає maven-surefire-plugin
Не реалізовано: вимагає розуміння призначеної конфігурації виконання тестів. Пропонується: додати maven-surefire-plugin з junit-platform provider.

### REA-webtemplate-003 — Немає workflow CI
Не реалізовано: вимагає розуміння необхідного SCOPE CI. Пропонується: додати build.yml для виконання тестів Maven.

## План публікації
- Fork: `admeduardovieira/web-template-tests` (створено).
- Гał diff гałку `fix/rea-webtemplate-001-003` для виправлень.
- Ідентичність коміту: `admeduardovieira <admeduardovieira@users.noreply.github.com>`.
- PR #1: https://github.com/better-care/web-template-tests/pull/1 (відкрито, база master).
