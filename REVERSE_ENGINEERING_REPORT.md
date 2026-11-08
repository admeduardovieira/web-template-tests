# REVERSE_ENGINEERING_REPORT — web-template-tests

## A. Diagnóstico geral

### Arquitetura identificada
Biblioteca Java/Maven de testes para WebTemplate (EHR compositions) da Better Platform. Fornece interfaces e utilitários para converter composições entre formatos RAW, FLAT e STRUCTURED, e validá-las contra templates. Estrutura:

- `src/main/java/care/better/platform/web/template/`: interfaces principais (CompositionConverter, WebTemplateProvider, CompositionValidator) e classes base (AbstractWebTemplateTest, CompositionBuilderContextKey, ValidationErrorDto, WebTemplateTestExtension)
- `src/test/java/`: ~60 classes de teste JUnit 5 para cenários de conversão e validação
- `pom.xml`: Maven project (Java 1.8, Jackson 2.11.3, JUnit 5.6.3, AssertJ 3.17.2)
- `README.md`: documentação de configuração para projetos consumidores

### Tecnologias e dependências
- Java 1.8
- Maven
- Jackson 2.11.3, JUnit 5.6.3, AssertJ 3.17.2, Google Collections 1.0, Commons IO 2.8.0
- Empacota como test-jar (maven-jar-plugin test-jar goal)

### Estado de manutenção
Último commit ativo. Branch default: master. Repositório: https://github.com/better-care/web-template-tests.

### Mecanismos de testes existentes
~60 testes JUnit 5 em `src/test/java/`. Não há CI workflow (GitHub Actions) configurado.

### Limitações da investigação
- Maven não instalado; testes não executados.
- REA 6.7.0 não operacional; análise estática apenas.

## B. Problemas encontrados

| ID | Título | Severidade | Status | Localização |
|----|--------|------------|--------|-------------|
| REA-webtemplate-001 | README.md: XML malformado (tag `></version>`) nos exemplos de dependências Maven | P2 | CONFIRMADO | `README.md:29,35,105,115` |
| REA-webtemplate-002 | Nenhuma dependência `maven-surefire-plugin` no pom.xml | P3 | CONFIRMADO | `pom.xml` |
| REA-webtemplate-003 | Nenhum workflow CI (GitHub Actions) configurado | P3 | CONFIRMADO | ausência de `.github/workflows` |

### Detalhes dos problemas confirmados

**REA-webtemplate-001 (P2, CONFIRMADO)**: O README.md contém exemplos de dependências Maven com tags de fechamento malformadas: `${jupiter.version></version>` em vez de `${jupiter.version}</version>`. Isso torna os exemplos de copiar-e-colar inválidos (XML não bem-formado).

Evidência: `README.md:29,35` (blocos de JUnit), `README.md:105,115` (blocos de TestNG).

**REA-webtemplate-002 (P3, CONFIRMADO)**: O `pom.xml` configura `maven-compiler-plugin` e `maven-jar-plugin`, mas não declara `maven-surefire-plugin`, necessário para executar testes JUnit 5 via `mvn test`.

**REA-webtemplate-003 (P3, CONFIRMADO)**: Não há pasta `.github/workflows` — nenhum CI para build, teste ou verificação de PR.

## C. Problemas recorrentes
Nenhum problema recorrente público encontrado.

## D. Erros não documentados
Todos os itens da seção B são problemas não documentados anteriormente.

## E. Performance
Biblioteca de testes Java; sem operações de performance críticas.

## F. Melhorias técnicas
- Corrigir tags XML malformadas no README (REA-webtemplate-001, implementado)
- Adicionar maven-surefire-plugin ao pom.xml (REA-webtemplate-002)
- Adicionar workflow CI (REA-webtemplate-003)

## G. Plano de execução
Todas independentes e baixo risco.

## H. Resultado esperado
Documentação Maven corrigida, builds reproduzíveis, CI configurado.

**Ferramentas usadas:** git, gh, PowerShell, inspeção estática.  
**Limitação:** Maven não instalado.  
**Ambiente:** Windows, PowerShell 5.1, `C:\Users\User\audit-repos\web-template-tests` (clone do upstream, branch master).
