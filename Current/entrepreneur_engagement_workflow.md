# Current State: Engagement & Activity Tracking

This diagram illustrates the workflow for processing activities (mentoring, events) for *existing* entrepreneurs in the network.
Key characteristics:
- **Trigger**: Occurs when an entrepreneur has an interaction (session, event, etc.).
- **Pain Point**: Staff must manually enter data into both the Agency CRM and the Shared Portal.

```mermaid
graph TD
    Start((Entrepreneur has Activity <br/> Session/Event))

    subgraph Agency_Workflow [Agency Process]
        Start --> StaffLog[1. Staff logs in Agency CRM]
        StaffLog --> AgencyDB[(Agency Database)]
        
        subgraph Pain_Point [PAIN POINT: Double Data Entry]
            direction TB
            StaffLog
            StaffManual[2. Staff MANUALLY enters in <br/> SourceLink Portal]
        end
    end

    %% Shared Database
    SourceLinkDB[(Shared Database <br/> SourceLink)]
    
    StaffManual --> SourceLinkDB

    %% Styling
    classDef pain fill:#ffeeee,stroke:#f96,stroke-width:2px,stroke-dasharray: 5 5;
    class Pain_Point pain;
```
