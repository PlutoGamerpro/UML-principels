# UML-principels

## Flowchart
```mermaid
flowchart TD
    A[Start] --> B{Bruger tilmelder sig / Logger ind}
    B --> C[Søg efter bøger]
    C --> D[Vælg bog]
    D --> E[Lån bog / Returner bog]
    E --> F[Opdater database]
    F --> G[Slut]

graph TD
    A[Bruger] -->|tilmelder sig| B[System]
    A -->|logger ind| B
    A -->|søger efter bøger| B
    A -->|låner bøger| B
    A -->|returnerer bøger| B
    A -->|ser lån| B
    C[Bibliotekar] -->|logger ind| B
    C -->|tilføjer bøger| B
    C -->|fjerner bøger| B
    C -->|administrerer lån| B

classDiagram
    class Bruger {
        +brugerID
        +navn
        +email
        +lånerHistorik
        +tilmeld()
        +logInd()
        +søgBøger()
        +lånBøger()
        +returnerBøger()
    }

    class Bibliotekar {
        +bibliotekarID
        +navn
        +email
        +logInd()
        +tilføjBøger()
        +fjernBøger()
        +administrerLån()
    }

    class Bog {
        +bogID
        +titel
        +forfatter
        +tilgængelig
        +opdaterTilgængelig()
    }

    class Lån {
        +lånID
        +brugerID
        +bogID
        +lånedato
        +afleveringsdato
        +opretLån()
        +afslutLån()
    }

sequenceDiagram
    participant Bruger
    participant System
    participant Database
    Bruger->>System: Log ind
    System->>Database: Valider bruger
    Database-->>System: Returner brugeroplysninger
    System-->>Bruger: Vis brugerinterface



graph TD
    A[Tilmeld dig] --> B[Log ind]
    B --> C[Søg efter bøger]
    C --> D[Vælg bog]
    D --> E[Lån eller returnér]
    E --> F[Opdater systemstatus]
