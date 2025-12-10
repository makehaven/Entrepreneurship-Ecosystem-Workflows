# Entrepreneurship Ecosystem Data Workflows

These diagrams outline the data flow for entrepreneurs entering and interacting with the ecosystem.

## 1. Current Workflow (Manual Bridges & Double Entry)
This chart highlights the current friction points:
*   **Lack of API:** Data transfer relies on triggering emails and asking the user to manually sign up again.
*   **Double Entry:** Agencies with their own CRMs must enter interaction data twice (once locally, once in SourceLink).
*   **Disconnected Data:** No automated way to link the Agency's record with the Shared Database record.

```mermaid
flowchart TD
    %% Roles/Systems
    Ent((Entrepreneur))
    Agency[Agency CRM\n(e.g., MakeHaven)]
    SharedDB[(Shared Database\nSourceLink)]
    E3[e3connector.com\nPublic Portal]
    Agent(Agency Staff)

    %% Path 1: Direct Discovery
    subgraph Direct_Discovery [Path 1: Direct Signup]
        Ent -- Finds Network --> E3
        E3 -- "Sign Up & AI Suggestions" --> SharedDB
        SharedDB -- Creates Record --> SharedDB
    end

    %% Path 2: Agency Onboarding
    subgraph Agency_Entry [Path 2: via Agency]
        Ent -- "Joins/Signs Up" --> Agency
        Agency -- "Collects Interest & Key Data" --> Agency
        
        %% The Gap
        Agency -.->|NO API CONNECTION| SharedDB
        
        %% The Workaround
        Agency -- "Trigger Email with Link" --> Ent
        Ent -- "Manually Clicks Link\n(Friction Risk)" --> E3
        E3 --> SharedDB
    end

    %% Path 3: Ongoing Interactions (The Double Entry Problem)
    subgraph Operations [Ongoing Tracking]
        Agent -- "Performs Service/Mentoring" --> Ent
        Agent -- "Enters Data (1st Time)" --> Agency
        Agent -.->|NO SYNC| SharedDB
        Agent -- "Manually Re-enters Data\n(Double Entry)" --> SharedDB
    end

    %% Styles
    classDef gap fill:#ffcccc,stroke:#ff0000,stroke-dasharray: 5 5;
    classDef system fill:#e1f5fe,stroke:#01579b;
    classDef person fill:#fff9c4,stroke:#fbc02d;

    class Agency,SharedDB,E3 system;
    class Ent,Agent person;
    linkStyle 3,8,9 stroke:#ff0000,stroke-width:2px,color:red;
```

---

## 2. Future Ideal Workflow (API Integrated)
This chart illustrates the goals:
*   **Automated Sync:** Users opting in at the Agency level are automatically pushed to the Shared Database.
*   **External ID:** The Agency CRM stores the SourceLink ID to maintain a persistent link.
*   **Single Entry:** Staff enters data once in their CRM; the system pushes the event to the Shared Database automatically.

```mermaid
flowchart TD
    %% Roles/Systems
    Ent((Entrepreneur))
    Agency[Agency CRM\n(e.g., MakeHaven)]
    SharedDB[(Shared Database\nSourceLink)]
    E3[e3connector.com\nPublic Portal]
    Agent(Agency Staff)
    API{{API / Integration Layer}}

    %% Path 1: Direct Discovery
    subgraph Direct_Discovery [Path 1: Direct Signup]
        Ent -- Finds Network --> E3
        E3 --> SharedDB
    end

    %% Path 2: Agency Onboarding (Integrated)
    subgraph Agency_Entry [Path 2: via Agency]
        Ent -- "Joins & Opts-in" --> Agency
        Agency -- "Push Registration Data" --> API
        API -- "Create/Match User" --> SharedDB
        SharedDB -- "Return External ID" --> API
        API -- "Save External ID" --> Agency
    end

    %% Path 3: Ongoing Interactions (Automated)
    subgraph Operations [Ongoing Tracking]
        Agent -- "Performs Service/Mentoring" --> Ent
        Agent -- "Enters Data (Single Entry)" --> Agency
        Agency -- "Push Event/Interaction\n(using External ID)" --> API
        API -- "Log Activity" --> SharedDB
    end

    %% Search/Lookup
    subgraph Lookup [Identification]
        Agency -. "Search by Email/Name" .-> API
        API -. "Return Existing ID" .-> Agency
    end

    %% Styles
    classDef system fill:#e1f5fe,stroke:#01579b;
    classDef person fill:#fff9c4,stroke:#fbc02d;
    classDef api fill:#dcedc8,stroke:#33691e,stroke-width:2px;

    class Agency,SharedDB,E3 system;
    class Ent,Agent person;
    class API api;
```
