# External References — Traumtänzer

Dieser repo-lokale Index enthält externe technische Referenzen, die für den **aktuellen** Traumtänzer-Repozustand relevant sind. Er folgt dem Agent-Workforce-Contract: <https://github.com/jannekbuengener/agent-workforce/blob/main/contracts/EXTERNAL_REFERENCE_CONTRACT.md>.

Diese Datei erweitert **nicht** den Produkt-, Provider-, Pilot-, Safety-, Privacy- oder Claims-Scope. GitHub-/Repo-Live-State sowie die lokale Governance und der Canon bleiben autoritativ.

## Priorität und Authority

- `P0` — aktive Kernreferenz mit aktuellem Repo-Signal.
- `P1` — aktive sekundäre Referenz mit aktuellem Repo-Signal.
- `P2` — geparkt/referenz-only; kein Beleg für aktive Implementierung oder Freigabe.

External Source Authority ist davon unabhängig: `OFFICIAL_SPEC` > `OFFICIAL_DOCS` > `UPSTREAM_PROJECT_DOCS` > `UPSTREAM_ISSUES_RELEASES` > `ESTABLISHED_TECHNICAL_KNOWLEDGE` > `COMMUNITY` > `EXAMPLE_DISCOVERY`.

## Aktive Referenzen

| Kategorie | Name | Priorität | Source type | Authority | Zweck | Repo-Signal | Wann nutzen | Canonical URL / identity |
|---|---|---|---|---|---|---|---|---|
| Repo/CI | GitHub Docs | `P0` | `official_docs` | `OFFICIAL_DOCS` | PRs, Checks, Security und Repository-Governance. | `CONTRIBUTING.md` verlangt PR-only Canon-Änderungen und grüne CI-/Security-Gates; `.github/workflows/` ist aktiv. | PR-/Check-/Governance-/Security-Workflow-Fragen. | https://docs.github.com/ |
| Repo/CI | GitHub Actions | `P0` | `official_docs` | `OFFICIAL_DOCS` | Workflow- und Check-Semantik. | `.github/workflows/ci.yml`, `codeql.yml`, `dependency-review.yml`, `gitleaks.yml`, `release.yml`, `trivy.yml`. | Änderungen oder Diagnose an CI/Security-Workflows. | https://docs.github.com/en/actions |
| Harness | Python | `P1` | `official_docs` | `OFFICIAL_DOCS` | Sprache/Stdlib für das lokale Evidence-Harness. | `harness/*.py` enthält den aktuellen deterministischen Harness-Code. Das ist kein Beleg für einen freigegebenen Live-Produkt-Runtimepfad. | Harness-, Guard-, Kernel- oder Evidence-Code. | https://docs.python.org/3/ |
| Harness | SQLite | `P1` | `official_docs` | `OFFICIAL_DOCS` | Persistenz des lokalen, content-free Evidence Event Stores. | `harness/event_store.py` nutzt `sqlite3` und kennzeichnet die DB ausdrücklich als HARNESS-ONLY. | Nur bei Harness-Event-Store-/SQLite-Arbeit. | https://sqlite.org/docs.html |
| Security | CodeQL | `P1` | `official_docs` | `OFFICIAL_DOCS` | Code-Scanning-Workflow. | `.github/workflows/codeql.yml`; `CONTRIBUTING.md` nennt CodeQL im DoD. | CodeQL-/Code-Scanning-Konfiguration und Befunde. | https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning-with-codeql |
| Security | Gitleaks | `P1` | `upstream_project_docs` | `UPSTREAM_PROJECT_DOCS` | Secret-Scanning-Gate. | `.github/workflows/gitleaks.yml`; `CONTRIBUTING.md` nennt Gitleaks im DoD. | Secret-Scanning-Workflow und Konfiguration. | https://github.com/gitleaks/gitleaks |
| Supply chain | Dependency Review | `P1` | `official_docs` | `OFFICIAL_DOCS` | Dependency-Änderungsprüfung in PRs. | `.github/workflows/dependency-review.yml`; `CONTRIBUTING.md` nennt Dependency Review im DoD. | Dependency-Review-Workflow oder Supply-Chain-Fragen. | https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/about-dependency-review |
| Security | Trivy | `P1` | `official_docs` | `OFFICIAL_DOCS` | Repository-/Supply-Chain-Scanning gemäß vorhandenem Workflow. | `.github/workflows/trivy.yml`. | Nur bei bestehendem Trivy-Workflow/Scan-Scope. | https://trivy.dev/docs/ |

## Geparkte Referenzen

Es werden bewusst **keine LLM-Provider-Dokumentationen** als `P0`/`P1` geführt. README und Canon sagen ausdrücklich, dass ein externer LLM-Pfad für Live-Nutzer nicht freigegeben ist und der lokale Harness keinen Provider-/Pilot-Scope etabliert.

Ein Provider, Deployment-System oder weiterer Runtime-Dienst darf erst als `P2` aufgenommen und später hochgestuft werden, wenn ein konkreter lokaler Issue-/Canon-Pfad seinen Zweck und seine Grenzen dokumentiert.

## Pflege-Regeln

- Jeder `P0`/`P1`-Eintrag braucht dauerhaft ein aktuelles Repo-Signal.
- Referenzen dürfen Safety-, Privacy-, Claims- oder Canon-Hierarchie nicht erweitern oder abschwächen.
- Eine Doku zu einem Provider ist niemals Beweis für Provider-Freigabe, Pilotstatus oder Live-Nutzung.
- Community-/Example-Quellen dürfen Discovery unterstützen, überschreiben aber keine offizielle/upstream oder lokale Evidence.
- Keine workstation-spezifischen absoluten Pfade, Credentials, private Endpoints oder sensible Nutzerdaten committen.