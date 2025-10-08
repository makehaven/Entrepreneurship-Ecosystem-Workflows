# Entrepreneurship Ecosystem Workflow

```mermaid

flowchart TD

%% --- Phase 1: Intake ---
subgraph "Phase 1 - Initial Intake"
    direction LR
    A[Entrepreneur accesses web portal] --> B[Completes common questions]
    B --> C{Primary business type?}
    C --> D1[Answers product specific questions]
    C --> E1[Answers service specific questions]
    C --> F1[Answers store specific questions]
end

%% --- Phase 2: Analysis ---
subgraph "Phase 2 - Analysis and Matching"
    UnifiedInput[Aggregate all responses]
    UnifiedInput --> R[Generate needs report]
    R --> R_System[System finds partner orgs]
    R --> R_Human[Counselor reviews report]
end

%% --- Phase 3: Engagement ---
subgraph "Phase 3 - Partner Organization Engagement"
    Notify[System sends notifications]
    Notify --> EPOs[Partner orgs review prospect]
    EPOs --> Invite{Invite entrepreneur?}
    Invite -- Yes --> SpecificIntake[Complete specific intake]
    Invite -- No --> NoAction[No further action]
end

%% --- Connections Between Phases ---
D1 --> UnifiedInput
E1 --> UnifiedInput
F1 --> UnifiedInput
R_System --> Notify
