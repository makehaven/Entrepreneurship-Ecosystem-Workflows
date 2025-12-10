# Entrepreneurship Ecosystem Workflow

```mermaid

flowchart TD

%%{init:{
  "theme":"base",
  "themeVariables":{
    "primaryColor":"#F0F4F8",
    "primaryBorderColor":"#3B82F6",
    "primaryTextColor":"#111827",
    "lineColor":"#4B5563",
    "fontSize":"15px"
  }
}}%%

%% --- Class Definitions ---
classDef Start fill:#10B981,color:#fff,stroke:#059669,stroke-width:2px;
classDef Process fill:#F9FAFB,stroke:#D1D5DB,stroke-width:1px,color:#111827;
classDef Decision fill:#F59E0B,color:#fff,stroke:#D97706,stroke-width:2px;
classDef HumanAction fill:#3B82F6,color:#fff,stroke:#2563EB,stroke-width:2px;
classDef SystemAction fill:#8B5CF6,color:#fff,stroke:#7C3AED,stroke-width:2px;
classDef PartnerOrg fill:#EC4899,color:#fff,stroke:#DB2777,stroke-width:2px;

%% --- Phase 1: Intake ---
subgraph "Phase 1 - Initial Intake via Better Ecosystems Portal"
    direction LR
    A[Entrepreneur accesses web portal]:::Start --> B[Completes common questions]:::Process
    B --> C{What is the primary business type}:::Decision
    C --> D[Physical product track]:::Process
    D --> D1[Answers product specific questions]:::Process
    C --> E[Service or digital track]:::Process
    E --> E1[Answers service specific questions]:::Process
    C --> F[Mainstreet or retail track]:::Process
    F --> F1[Answers store specific questions]:::Process
end

%% --- Phase 2: Analysis ---
subgraph "Phase 2 - Analysis and Matching"
    UnifiedInput[Aggregate all responses]:::Process
    UnifiedInput --> R[Generate entrepreneur needs report]:::SystemAction
    R --> R_System[System analyzes report and finds partner organizations]:::SystemAction
    R --> R_Human[Human counselor reviews report]:::HumanAction
    R_Human --> Counsel[Counselor provides guidance & recommendations]:::HumanAction
end

%% --- Phase 3: Engagement ---
subgraph "Phase 3 - Partner Organization Engagement"
    Notify[System sends notifications to matched partner orgs]:::SystemAction
    Notify --> EPOs[Partner orgs review prospect]:::PartnerOrg
    EPOs --> Invite{Invite entrepreneur}:::PartnerOrg
    Invite -- Yes --> SpecificIntake[Entrepreneur completes org specific intake form]:::Process
    Invite -- No --> NoAction[No further action by this org]:::Process
    SpecificIntake --> Onboarding[Entrepreneur begins onboarding with partner]:::Start
end

%% --- Reverse Flow ---
subgraph "Reverse Flow"
    EPO_Start[Partner org identifies an existing client for additional support]:::PartnerOrg
end

%% --- Connections Between Phases ---
D1 --> UnifiedInput
E1 --> UnifiedInput
F1 --> UnifiedInput
R_System --> Notify
Counsel -.->|Referral| EPOs
EPO_Start --> UnifiedInput
