# Thesis

Repository della mia tesi sulla sicurezza del codice generato da AI code assistants, con focus su **OCaml**, **GitHub Copilot/Codex** e confronto tra paradigma funzionale e linguaggi più esposti a pattern imperativi/OOP.

## Obiettivo

L'obiettivo della tesi è studiare le vulnerabilità presenti in snippet OCaml generati da AI assistants in scenari realistici. Il lavoro è ispirato allo studio *Security Weaknesses of Copilot-Generated Code in GitHub Projects*, che ha analizzato snippet Python e JavaScript generati da tool come Copilot e classificato le debolezze secondo CWE.[web:18]

## Idea del progetto

Dato che non esiste un corpus ampio e affidabile di snippet OCaml attribuibili con certezza a Copilot in repository pubblici, questo repository usa un **dataset controllato**, generato sperimentalmente. L'idea è mantenere la pipeline dello studio originale — generazione/raccolta snippet, analisi statica, revisione manuale, classificazione CWE — ma applicarla a task OCaml selezionati per dominio.[web:18]

## Struttura

```text
dataset/
├── web-backend/
├── web-frontend-js_of_ocaml/
├── networking-protocol-parsing/
├── systems-filesystem/
├── process-execution-automation/
├── randomness-crypto/
├── serialization-deserialization/
├── concurrency-async/
├── finance-business-logic/
├── formal-methods-dsl/
├── compiler-language-tooling/
├── static-analysis-program-analysis/
├── embedded-safety-critical/
└── mirageos-unikernel/
```

Ogni dominio contiene sottocartelle separate per modello:

```text
<dominio>/
├── codex/
└── copilot/
```

## Workflow

Per ogni dominio:

1. definizione del task;
2. scrittura del prompt;
3. generazione dello snippet OCaml;
4. analisi statica;
5. revisione manuale;
6. classificazione delle issue secondo CWE;
7. confronto tra modelli e tra domini.[web:18]

## CWE di interesse

Le CWE osservate dipendono dal dominio, ma tra le principali da cercare ci sono:

- CWE-20: Improper Input Validation
- CWE-22: Path Traversal
- CWE-78: OS Command Injection
- CWE-79: Cross-Site Scripting
- CWE-94: Improper Control of Generation of Code
- CWE-295: Improper Certificate Validation
- CWE-330: Insufficient Randomness
- CWE-434: Unrestricted File Upload
- CWE-502: Deserialization of Untrusted Data[web:18]

## Focus teorico

La tesi sostiene che OCaml, grazie a tipizzazione statica forte, memory safety e minore dipendenza da stato mutabile, possa ridurre alcune classi di vulnerabilità rispetto a linguaggi dinamici come Python e JavaScript. Questo non significa che il codice OCaml generato da AI sia automaticamente sicuro, ma che il paradigma può influenzare il tipo e la frequenza delle weakness osservabili.[web:18][web:105][web:239]

## MirageOS

Una parte del lavoro è dedicata anche a **MirageOS**, perché rappresenta un caso molto interessante di OCaml usato in sistemi e servizi security-critical. MirageOS punta a ridurre attack surface e complessità attraverso unikernel specializzati e librerie type-safe, quindi è utile per discutere il legame tra paradigma funzionale e sicurezza del software.[web:239][web:105]

## Nota metodologica

Questo repository non misura direttamente la prevalenza del codice vulnerabile “in the wild” su GitHub per OCaml. Raccoglie invece un benchmark controllato di snippet generati da assistant diversi, con l'obiettivo di produrre un confronto metodologicamente chiaro
