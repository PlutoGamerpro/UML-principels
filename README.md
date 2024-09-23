# Bibliotekssystem Design

```mermaid
%% Combined Mermaid Diagram for Bibliotekssystem Design

flowchart TD
    subgraph Flowchart
        A1[Start] --> B1{Bruger tilmelder sig / Logger ind}
        B1 --> C1[Søg efter bøger]
        C1 --> D1[Vælg bog]
        D1 --> E1[Lån bog / Returner bog]
        E1 --> F1[Opdater database]
        F1 --> G1[Slut]
    end

    subgraph UseCaseDiagram
        A2[Bruger] -->|tilmelder sig| B2[System]
        A2 -->|logger ind| B2
        A2 -->|søger efter bøger| B2
        A2 -->|låner bøger| B2
        A2 -->|returnerer bøger| B2
        A2 -->|ser lån| B2
        C2[Bibliotekar] -->|logger ind| B2
        C2 -->|tilføjer bøger| B2
        C2 -->|fjerner bøger| B2
        C2 -->|administrerer lån| B2
    end

    subgraph ClassDiagram
        class Bruger {
            brugerID: int
            navn: string
            email: string
            lånerHistorik: List
            tilmeld()
            logInd()
            søgBøger()
            lånBøger()
            returnerBøger()
        }

        class Bibliotekar {
            bibliotekarID: int
            navn: string
            email: string
            logInd()
            tilføjBøger()
            fjernBøger()
            administrerLån()
        }

        class Bog {
            bogID: int
            titel: string
            forfatter: string
            tilgængelig: boolean
            opdaterTilgængelig()
        }

        class Lån {
            lånID: int
            brugerID: int
            bogID: int
            lånedato: date
            afleveringsdato: date
            opretLån()
            afslutLån()
        }
    end

    subgraph SequenceDiagram
        participant Bruger
        participant System
        participant Database
        Bruger->>System: Log ind
        System->>Database: Valider bruger
        Database-->>System: Returner brugeroplysninger
        System-->>Bruger: Vis brugerinterface
    end

    subgraph ActivityDiagram
        A3[Tilmeld dig] --> B3[Log ind]
        B3 --> C3[Søg efter bøger]
        C3 --> D3[Vælg bog]
        D3 --> E3[Lån eller returnér]
        E3 --> F3[Opdater systemstatus]
    end
