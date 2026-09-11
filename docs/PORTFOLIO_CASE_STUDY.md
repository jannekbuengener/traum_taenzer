# Traumtänzer — Portfolio Case Study

## 1. Ausgangsidee

Traumtänzer ist als privater digitaler Erfahrungsraum zur Selbstreflexion konzipiert.

Gerade weil das Produkt mit subjektiven, persönlichen und potenziell sensiblen Inhalten arbeitet, entsteht früh ein Responsible-AI-Problem:

> **Wie kann ein KI-gestütztes System Raum für Reflexion schaffen, ohne Diagnose, Therapie, autoritäre Deutung, emotionale Abhängigkeit oder unkontrollierte Datennutzung zu erzeugen?**

Die Antwort des Projekts ist nicht „ein besonders guter Prompt“, sondern ein System aus **Governance, deterministischen Guards, Claim-Grenzen, Privacy-Regeln und Evidence**.

## 2. Das Risiko falscher Claims

Bei einem Produkt rund um Reflexion und innere Erfahrung können harmlose Formulierungen schnell zu unzulässigen Behauptungen werden.

Das Claims Framework verbietet deshalb unter anderem:

- Therapie- oder Heilbehauptungen,
- Diagnosen oder Aussagen über psychische Zustände,
- Kriseninterventions-Claims,
- autoritäre Traum-/Symboldeutung,
- Persönlichkeitsprofile als Wahrheit,
- Companion-Rhetorik, die emotionale Bindung wie zu einer Person fördert,
- Wirkungsbehauptungen, die der aktuelle Produktstand nicht belegt.

Symbolische Inhalte dürfen als mögliche Perspektive angeboten werden, nicht als Wahrheit über einen Nutzer.

Siehe: [CLAIMS_FRAMEWORK](../knowledge/project/CLAIMS_FRAMEWORK.md).

## 3. Grenzen werden vor Features definiert

Die Constitution setzt vier P0-Prinzipien:

1. **Safety vor Experience**
2. **Privacy vor Bequemlichkeit**
3. **Fail-closed statt fail-open**
4. **Evidence vor Behauptung**

Diese Reihenfolge ist eine Produktentscheidung.

Ein Feature darf deshalb nicht dadurch „besser“ werden, dass es:

- Exit erschwert,
- mehr persönliche Daten speichert,
- Safety-Entscheidungen an ein LLM delegiert,
- einen stärkeren Claim macht als die Evidence erlaubt.

Siehe: [CONSTITUTION](../knowledge/governance/CONSTITUTION.md).

## 4. Safety

Das Safety Playbook behandelt Exit nicht als spätes UX-Detail.

Wichtige Regeln sind:

- Exit jederzeit und ohne Begründung,
- Safeword stoppt die Session unmittelbar,
- keine Nachfragen oder Überredungsversuche nach Safeword,
- bei Unsicherheit oder Safety-Signal wird stabilisiert / beendet statt vertieft,
- keine Diagnose,
- keine Illusion eines 24/7-Companions oder Krisendienstes.

Das System soll nicht „intelligent weiterreden“, wenn seine sichere Grenze erreicht ist.

Siehe: [SAFETY_PLAYBOOK](../knowledge/project/SAFETY_PLAYBOOK.md).

## 5. Privacy

Privacy ist als Systeminvariante gedacht, nicht nur als Datenschutzerklärung.

Der Canon fordert insbesondere:

- Session-Content standardmäßig ephemer,
- keine Persistenz ohne dokumentierten Zweck und Löschpfad,
- Redaction-first,
- keine unnötigen Nutzerinhalte in Logs,
- Provider-Nutzung nur innerhalb des freigegebenen Daten-/DPA-Rahmens.

Damit wird die Frage „dürfen wir diese Daten überhaupt an diesen Pfad geben?“ vor die Frage gestellt, ob ein Modell technisch gute Antworten liefern könnte.

Siehe: [PRIVACY_BY_DESIGN](../knowledge/project/PRIVACY_BY_DESIGN.md).

## 6. Architektur: LLM als Adapter, nicht als Orchestrator

Eine zentrale Architekturentscheidung lautet:

> **Das Sprachmodell ist austauschbarer Inferenz-Adapter — nicht die Kontrollinstanz.**

Die vereinfachte Architektur:

```text
User Input
   ↓
Deterministic Guards
   ↓
Safe? ── no/uncertain ─→ Safe State / Exit / Referral
   │
  yes
   ↓
Session Kernel
   ↕
LLM Adapter
   ↓
Bounded Response
```

Der Kernel und deterministische Guards kontrollieren Session-Logik, Safety und Persistenz. Ein LLM darf Text erzeugen, aber nicht seine eigene Autorität definieren.

Siehe: [ARCHITECTURE_OVERVIEW](../knowledge/architecture/ARCHITECTURE_OVERVIEW.md).

## 7. Governance von KI-Agenten

Auch die Entwicklung selbst nutzt mehrere KI-Agenten.

Die Agent Policy behandelt diese Systeme bewusst als **Zuarbeiter, nicht Entscheider**.

Agenten dürfen beispielsweise:

- analysieren,
- Diffs vorbereiten,
- Evidence sammeln,
- Konflikte benennen.

Sie dürfen insbesondere nicht:

- Safety-/Privacy-Grenzen abschwächen,
- neue Produktclaims erfinden,
- ungeprüfte Tests behaupten,
- finale Freigaben aus sich selbst ableiten,
- Scope oder Canon eigenmächtig erweitern.

Damit gilt dieselbe Grundidee sowohl im Produkt als auch im Entwicklungsprozess: **KI-Fähigkeit erzeugt nicht automatisch Autorität.**

Siehe: [AGENT_POLICY](../knowledge/governance/AGENT_POLICY.md).

## 8. Evidence / technische Umsetzung

Traumtänzer ist heute nicht mehr ausschließlich eine Sammlung von Konzeptdokumenten.

Der aktuelle Status dokumentiert unter anderem:

- lokales deterministisches Evidence-Harness,
- Kernel / Guards,
- Stub-Adapter,
- content-freien SQLite-Event-Store,
- Fault Injection,
- Smoke- und Szenario-Evidence,
- Runtime-Evidence-Pfade,
- eine Hetzner-deploybare Runtime-Foundation mit einem dokumentierten nicht-providergekoppelten Evidence-Lauf.

Diese technische Foundation ist jedoch ausdrücklich **kein Beweis für Pilot- oder Live-Freigabe**.

Das Projekt trennt:

```text
technical evidence
       !=
provider approval
       !=
pilot approval
       !=
live product
```

Der jeweils aktuelle Stand liegt in [CURRENT_STATUS](../knowledge/CURRENT_STATUS.md).

## 9. Aktueller Stand und Blocker

Zum dokumentierten Status gehören positive technische Evidence **und** offene P0-Gates.

Insbesondere ist aktuell kein geprüfter externer LLM-Pfad für Live-Nutzer freigegeben. Provider-gekoppelte Tests bleiben dadurch blockiert, und weitere Pilot-Evidence-Artefakte sind offen.

Daraus folgt konservativ:

- lokale / kontrollierte System-Evidence: vorhanden,
- technische Runtime-Foundation: vorhanden,
- externer Provider-Go für Live-Nutzer: nein,
- freigegebener Pilot: nein,
- Live-Produkt: nein.

Das ist ein Beispiel dafür, wie das Projekt technischen Fortschritt dokumentiert, ohne daraus automatisch einen stärkeren Produktclaim zu machen.

## 10. Meine Rolle

Meine Kernrolle ist **Concept-to-System und AI-assisted Governance/Product Design**.

Ich arbeite an:

- der ursprünglichen Produktidee,
- der Zerlegung in Systemgrenzen,
- Requirements und Nicht-Zielen,
- Safety-/Privacy-/Claim-Regeln,
- Architektur- und Autoritätsentscheidungen,
- Orchestrierung von KI-Systemen als Zuarbeiter,
- Review und Konsistenzprüfung,
- Evidence-orientierter Statusbewertung.

Die Implementierung ist stark AI-assisted. Das Portfolio soll deshalb nicht suggerieren, ich hätte jede Runtime-Komponente manuell geschrieben oder sei klassischer Senior Software Engineer.

Der relevante Kompetenzclaim lautet:

> **Ich kann eine sensible Produktidee so strukturieren, dass technische Möglichkeiten, Nutzererlebnis, Safety, Privacy, Claims und KI-Autorität explizite und überprüfbare Grenzen bekommen.**

## 11. Was dieser Case demonstriert

- Responsible AI
- Product / System Thinking
- Requirements & Boundaries
- Safety-by-Design
- Privacy-by-Design
- Claim Governance
- Fail-closed System Design
- AI-Agent Governance
- Evidence / Validation
- AI-assisted Delivery
- Umgang mit Unsicherheit und nicht freigegebenen Zuständen

## 12. Was dieser Case nicht behauptet

Traumtänzer ist aktuell:

- **kein Therapieangebot**,
- **kein diagnostisches System**,
- **kein Krisendienst**,
- **kein freigegebenes Live-Produkt**,
- **kein freigegebener Pilot**,
- **kein Beweis einer psychologischen oder medizinischen Wirksamkeit**.

Die Idee, Symbolik oder subjektive Erfahrung zu untersuchen, ist Produkt-/Forschungsrahmen. Sie ist keine wissenschaftlich belegte Wirkungsbehauptung.

## 13. Lessons Learned

### Governance muss früher kommen als bei klassischen Demo-Projekten

Bei sensiblen AI-Produkten können spätere Disclaimer keine Architektur reparieren, die vorher falsche Autorität oder Datennutzung eingebaut hat.

### Ein LLM sollte seine eigenen Grenzen nicht kontrollieren

Deterministische Guards und Kernel-Verträge machen Safety-Boundaries überprüfbarer als reine Prompt-Regeln.

### „Technisch funktioniert“ ist nur ein Status

Ein funktionierender Runtime-Pfad, eine grüne Evidence-Suite oder ein Provider-Test ist nicht automatisch ein Pilot- oder Produkt-Go.

### Gute AI-Produkte brauchen auch die Fähigkeit, nicht zu handeln

Fail-closed, Exit und ein ehrliches „nicht freigegeben“ sind Produktfähigkeiten — keine Niederlagen.
