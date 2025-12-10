# Current State: Onboarding & Entry Flow
This diagram illustrates the current manual onboarding process for *new* entrepreneurs.
Key characteristics:
- **Parallel Entry**: Entrepreneurs enter via the public portal (e3connector) or directly through an Agency.
- **Pain Point**: High risk of drop-off because the email invitation requires user re-entry of data.
- **Opt-Out**: Entrepreneurs who decline the network are simply logged in the Agency CRM.
```mermaid
graph TD
    Start((Entrepreneur Needs Support))
    
    %% Enforce side-by-side layout for entry points
    subgraph Entry
        direction LR
        E3Site["Visit e3connector.com"]
        AgencyContact["Make Contact / <br/> Start with Agency"]
    end
    
    Start --> E3Site
    Start --> AgencyContact
    sidebar_db[("Shared Database <br/> SourceLink")]
    subgraph Direct_Entry [Direct to Network Path]
        E3Site --> E3Signup[Sign Up on Portal]
        E3Signup --> sidebar_db
        E3Signup --> AI_Rec[AI Suggests Agencies]
        
        %% Referral loop
        AI_Rec -.->|Referral| AgencyContact
    end
    subgraph Agency_Entry [Agency Path]
        AgencyContact --> SignupForm[Agency Signup Form]
        SignupForm --> Q_OptIn{Opt into <br/> Entrepreneur Network?}
        
        %% No Branch
        Q_OptIn -- No --> AgencyCRM["Log in Agency CRM <br/> (Internal Only)"]
        
        %% Yes Branch with Pain Point
        Q_OptIn -- Yes --> TriggerEmail["Trigger System Email <br/> 'Join the Network'"]
        
        subgraph Pain_Point [PAIN POINT: Friction]
            direction TB
            TriggerEmail
            RiskDrop["RISK: Drop-off <br/> User must re-enter info"]
        end
        
        TriggerEmail --> UserAction["User clicks Link & <br/> Signs up Independently"]
        UserAction -.-> E3Site
    end
    %% Styling
    classDef plain fill:none,stroke:none;
    class Entry plain;
    
    classDef pain fill:#ffeeee,stroke:#f96,stroke-width:2px,stroke-dasharray: 5 5;
    class Pain_Point pain;
    class RiskDrop pain;