```mermaid
graph LR
    %% --- STYLING & PALETTE (High Contrast for Judges) ---
    classDef sensing fill:#f3e5f5,stroke:#7b1fa2,stroke-width:3px,color:#000,font-weight:bold
    classDef analysis fill:#e1f5fe,stroke:#0277bd,stroke-width:3px,color:#000,font-weight:bold
    classDef core fill:#e8f0fe,stroke:#1565c0,stroke-width:4px,color:#000,font-weight:bold,font-size:14px
    classDef memory fill:#fff8e1,stroke:#fbc02d,stroke-width:3px,color:#000,font-weight:bold
    classDef action fill:#e6f4ea,stroke:#2e7d32,stroke-width:3px,color:#000,font-weight:bold
    classDef critical fill:#ffebee,stroke:#c62828,stroke-width:3px,stroke-dasharray: 5 5,color:#000,font-weight:bold
    classDef user fill:#e0f7fa,stroke:#006064,stroke-width:3px,color:#000,shape:circle,font-weight:bold

    %% --- LAYER 1: SENSING (INPUTS) ---
    subgraph Layer1 [Layer 1: Multimodal Sensing]
        direction TB
        Student((Student)):::user --> Inputs
        
        subgraph Inputs [Input Channels]
            direction TB
            Drive[Drive Ingestion<br/>Syllabi]:::sensing
            Device[Device Stats<br/>Focus/Drift]:::sensing
            Vision[Visual Context<br/>Camera]:::sensing
            Voice[Voice/Chat<br/>Wake Word]:::sensing
        end
        
        Meaning[Meaning Anchor<br/>Visa/Scholarship]:::critical
        Health[Health State<br/>Sick/Recovering]:::critical
        
        Inputs --> Fusion[Sensing Engine<br/>Multimodal Fusion]:::sensing
        Meaning --> Fusion
        Health --> Fusion
    end

    %% --- LAYER 2: ANALYSIS ---
    subgraph Layer2 [Layer 2: State Analysis]
        direction TB
        Fusion --> AnalysisNodes
        
        subgraph AnalysisNodes [Classifiers & Policy]
            direction TB
            Stakes[Stakes Classifier<br/>Loss Impact]:::analysis
            Pressure[Pressure Map<br/>Load vs Capacity]:::analysis
            Tracker[Engagement Tracker<br/>Behavior Trends]:::analysis
            PrivacyPolicy[Consent & Policy Engine]:::analysis
        end
        
        Offline[Offline Fallback<br/>Edge Mode]:::critical
        Fusion -.->|Network Loss| Offline
    end

    %% --- DATABASE MEMORY (Explicit) ---
    subgraph LayerMemory [Database Memory]
        direction TB
        Cache[(Context Cache<br/>1M Token)]:::memory
        History[(Adaptive Memory<br/>User Model)]:::memory
        Vault[(AntiPattern Vault<br/>Bad Patterns)]:::memory
        AuditLog[(Audit Log<br/>Transparency)]:::memory
        ImpactMetrics[(Impact Metrics<br/>Success)]:::memory
    end

    %% --- LAYER 3: REASONING CORE ---
    subgraph Layer3 [Layer 3: Gemini Reasoning]
        direction TB
        AnalysisNodes --> Core
        
        Cache <--> Core
        History <--> Core
        Vault <--> Core
        ImpactMetrics -->|Optimization Loop| Core
        
        Core[Gemini Reasoning Core<br/>Long-Context + Tools]:::core
        
        Core --> Simulator{Deep Think<br/>Simulator}:::core
        Simulator -->|High Risk| Core
        Simulator -->|Viable| Matrix{Decision Matrix<br/>Pressure vs Stakes}:::core
        
        Core --> Explain[Explainability<br/>Why This Plan?]:::core
        Core -.-> AuditLog
        Core -.->|Model Degraded| Offline
        AuditLog --> ImpactMetrics
    end

    %% --- LAYER 4: EXECUTION MODES ---
    subgraph Layer4 [Layer 4: Execution Modes]
        direction TB
        
        Matrix -->|Low Pressure| Routine[Routine Mode<br/>Proactive]:::action
        Routine --> Prep[Resource Orchestrator<br/>Fetch Readings]:::action
        Prep --> Curric[Auto-Curriculum<br/>Builder]:::action
        
        Matrix -->|High Pressure| Crisis[Crisis Mode<br/>Reactive]:::critical
        Crisis --> Triage[Compression Engine<br/>Audio Summaries]:::critical
        
        Matrix -->|Panic| Safety[Safety Net]:::critical
        Safety --> Alert[Peer Alert]:::critical
    end

    %% --- LAYER 5: INTERACTION LOOP ---
    subgraph Layer5 [Layer 5: Interaction]
        direction TB
        Curric --> Live
        Triage --> Live
        Explain --> Live
        
        Live[Gemini Live Negotiator<br/>Real-time Persona]:::core
        Live --> UserDecision{Accepts?}:::user
        
        UserDecision -->|NO| Trust[Trust Calibration]:::memory
        Trust --> Vault
        
        UserDecision -->|YES| Enforce[App Lock Service]:::action
        Enforce --> Action((Execute<br/>Study)):::action
        
        Action --> Check{Knowledge<br/>Check}:::analysis
        Check -->|Pass| Reward[Unlock Rewards]:::action
        Reward --> Mastery[Mastery Evaluator]:::action
        Mastery --> Update[Success Update]:::memory
        Update --> History
        
        Check -->|Fail| Recovery[Spaced Recovery]:::action
        Recovery --> Prep
    end

    %% --- BOLD CONNECTIONS ---
    Fusion ==>|Context| Stakes
    Fusion ==>|Context| Pressure
    Fusion ==>|Context| Tracker
    
    Offline -.->|Sync| History
    
    linkStyle default stroke-width:4px,fill:none,stroke:#333
    Fusion -->|Context| Tracker
    
    Offline -.->|Sync| History
    
    linkStyle default stroke-width:3px,fill:none,stroke:#555
