```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#e3f2fd', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#fdfefe'}}}%%
graph TD
    %% --- STYLING & PALETTE ---
    classDef sensing fill:#f3e5f5,stroke:#7b1fa2,stroke-width:4px,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef analysis fill:#e1f5fe,stroke:#0277bd,stroke-width:4px,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef core fill:#e8f0fe,stroke:#1565c0,stroke-width:5px,color:#000,font-weight:bold,font-size:20px,rx:5,ry:5
    classDef memory fill:#fff8e1,stroke:#fbc02d,stroke-width:4px,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef action fill:#e6f4ea,stroke:#2e7d32,stroke-width:4px,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef critical fill:#ffebee,stroke:#c62828,stroke-width:4px,stroke-dasharray: 5 5,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef user fill:#e0f7fa,stroke:#006064,stroke-width:4px,color:#000,shape:circle,font-weight:bold,font-size:20px

    %% --- LAYER 0: IDENTITY ---
    subgraph Layer0 [Layer 0: Identity & Access]
        direction TB
        Student((Student)):::user
        Auth[Auth & Identity<br/>OAuth / Passkey]:::analysis
        Session[Session Manager<br/>Trust + TTL]:::analysis
    end

    %% --- LAYER 1: SENSING (INPUTS) ---
    subgraph Layer1 [Layer 1: Multimodal Sensing]
        direction TB
        
        %% Grouping Inputs and Context side-by-side
        subgraph InputZone [ ]
            direction LR
            style InputZone fill:none,stroke:none

            subgraph Inputs [Digital Channels]
                direction TB
                Drive[Drive Ingestion<br/>Syllabi]:::sensing
                Device[Device Stats<br/>Focus/Drift]:::sensing
                Vision[Visual Context<br/>Camera]:::sensing
                Voice[Voice/Chat<br/>Wake Word]:::sensing
            end
            
            subgraph Context [Human Context]
                direction TB
                Meaning[Meaning Anchor<br/>Visa/Scholarship]:::critical
                Health[Health State<br/>Sick/Recovering]:::critical
                OverrideFlag[Human Override<br/>Mentor/Self]:::critical
            end
        end
        
        Fusion[Sensing Engine<br/>Multimodal Fusion]:::sensing
    end

    %% --- MAIN PROCESSING COLUMN (LEFT) ---
    subgraph MainSystem [Main Processing Pipeline]
        style MainSystem fill:#fcfcfc,stroke:#eee,stroke-width:2px
        direction TB

        %% --- LAYER 2: ANALYSIS ---
        subgraph Layer2 [Layer 2: State Analysis]
            direction TB
            subgraph AnalysisNodes [Classifiers & Policy]
                direction LR
                Stakes[Stakes Classifier<br/>Loss Impact]:::analysis
                Pressure[Pressure Map<br/>Load vs Capacity]:::analysis
                Tracker[Engagement Tracker<br/>Behavior Trends]:::analysis
                PrivacyPolicy[Consent & Policy Engine]:::analysis
                GoalHorizon[Goal Horizon Analyzer<br/>Deadline Proximity]:::analysis
            end
            Offline[Offline Fallback<br/>Edge Mode]:::critical
        end

        %% --- LAYER 3: REASONING CORE ---
        subgraph Layer3 [Layer 3: Gemini Reasoning]
            direction TB
            PolicyLearner[Policy Learner<br/>Outcome Optimization]:::analysis
            Core[Gemini 3 Pro Reasoning Core<br/>Long-Context + Tools]:::core
            BudgetGuard[Cost & Rate Guard<br/>Token / Latency]:::analysis
            Simulator{Deep Think<br/>Simulator}:::core
            Matrix{Decision Matrix<br/>Pressure vs Stakes}:::core
            Explain[Explainability<br/>Why This Plan?]:::core
            Confidence{Confidence Estimator<br/>Certainty Guard}:::core
        end

        %% --- LAYER 4: EXECUTION MODES ---
        subgraph Layer4 [Layer 4: Execution Modes]
            direction TB
            
            CapabilityGate[Capability Gate<br/>Tool Allowlist]:::critical
            
            subgraph Tools [External Tools]
                direction LR
                CalendarAPI[Calendar API]:::action
                FileSystem[File System]:::action
                NotificationSvc[Notification Service]:::action
            end

            Personalize[Personalization Engine<br/>Modality & Tone Pref]:::core

            subgraph ModeBranch [Decision Branches]
                direction LR
                Routine[Routine Mode<br/>Proactive]:::action
                Crisis[Crisis Mode<br/>Reactive]:::critical
                Safety[Safety Net]:::critical
            end
            Prep[Resource Orchestrator<br/>Fetch Readings]:::action
            Curric[Auto-Curriculum<br/>Builder]:::action
            Triage[Compression Engine<br/>Audio Summaries]:::critical
            Alert[Peer Alert]:::critical
        end

        %% --- LAYER 5: INTERACTION LOOP ---
        subgraph Layer5 [Layer 5: Interaction]
            direction TB
            Live[Gemini Live Negotiator<br/>Real-time Persona]:::core
            UserDecision{Accepts?}:::user
            Trust[Trust Calibration]:::memory
            Enforce[App Lock Service]:::action
            Action((Execute<br/>Study)):::action
            Check{Knowledge<br/>Check}:::analysis
            Reward[Unlock Rewards]:::action
            Mastery[Mastery Evaluator]:::action
            Update[Success Update]:::memory
            Recovery[Spaced Recovery]:::action
        end
    end

    %% --- DATABASE MEMORY COLUMN (RIGHT) ---
    subgraph LayerMemory [Database Memory]
        direction TB
        Cache[(Context Cache<br/>1M Token)]:::memory
        History[(Adaptive Memory<br/>User Model)]:::memory
        Vault[(AntiPattern Vault<br/>Bad Patterns)]:::memory
        HorizonMemory[(Long-Horizon State<br/>Days/Weeks)]:::memory
        AuditLog[(Audit Log<br/>Transparency)]:::memory
        NoActionLog[Non-Action Reason Log]:::memory
        ImpactMetrics[(Impact Metrics<br/>Success)]:::memory
        MotivationIndex[(Motivation Health<br/>Burnout/Reward)]:::memory
    end

    %% ==========================================================
    %% === CONNECTION DEFINITIONS ===
    %% ==========================================================
    
    %% -- 0. Identity Flow (0-6) --
    Student --> Auth
    Auth --> Session
    Session --> Inputs
    Session --> Meaning
    Session --> Health
    Session --> OverrideFlag
    Session --> PrivacyPolicy

    %% -- 1. Standard Flow (7-11) --
    Inputs --> Fusion
    Meaning --> Fusion
    Health --> Fusion
    OverrideFlag --> Fusion
    Fusion --> AnalysisNodes
    
    %% -- 2. Critical Fallbacks (12-13) --
    Fusion -.->|Network Loss| Offline
    BudgetGuard -.->|Throttle/Cost| Offline
    
    %% -- 3. Analysis -> Core (14) --
    AnalysisNodes --> Core
    
    %% -- 4. Memory I/O & Learning Loop (15-22) --
    Cache <--> Core
    History <--> Core
    Vault <--> Core
    MotivationIndex <--> Core
    HorizonMemory <--> Core
    ImpactMetrics --> PolicyLearner
    MotivationIndex --> PolicyLearner
    PolicyLearner -->|Optimization| Core
    
    %% -- 5. Core Logic Loops (23-34) --
    Core --> BudgetGuard
    BudgetGuard --> Simulator
    Simulator -->|High Risk| Core
    Simulator -->|Viable| Confidence
    Confidence -->|Low Confidence| Explain
    Confidence -->|Abort| NoActionLog
    NoActionLog --> AuditLog
    Confidence -->|High Confidence| Matrix
    Explain --> Live
    Core -.-> AuditLog
    Core -.->|Model Degraded| Offline
    AuditLog --> ImpactMetrics
    
    %% -- 6. Execution Decisions & Capability Gate (35-44) --
    Matrix -->|Low Pressure| Routine
    Matrix -->|High Pressure| Crisis
    Matrix -->|Panic| Safety
    
    Routine --> CapabilityGate
    Crisis --> CapabilityGate
    OverrideFlag --> CapabilityGate
    
    CapabilityGate --> Tools
    Tools -.->|Data Return| Core
    CapabilityGate --> Prep
    CapabilityGate --> Enforce
    
    %% -- 7. Mode Actions (45-48) --
    Prep --> Personalize
    Personalize --> Curric
    Triage --> Personalize
    Safety --> Alert
    
    %% -- 8. Interaction Setup (49-50) --
    Curric --> Live
    Personalize --> Live
    
    %% -- 9. User Interaction Loop (51-56) --
    Live --> UserDecision
    UserDecision -->|NO| Trust
    Trust --> Vault
    UserDecision -->|YES| Enforce
    Enforce --> Action
    Action --> Check
    
    %% -- 10. Outcomes (57-63) --
    Check -->|Pass| Reward
    Reward --> Mastery
    Mastery --> Update
    Update --> History
    Update --> MotivationIndex
    Check -->|Fail| Recovery
    Recovery --> Prep

    %% -- 11. Thick Context Links (64-68) --
    Fusion ==Context==> Stakes
    Fusion ==Context==> Pressure
    Fusion ==Context==> Tracker
    Fusion ==Context==> GoalHorizon
    Offline -.->|Sync| History

    %% ==========================
    %% === STYLING ===
    %% ==========================

    %% Generic link style (NEON GREEN for Standard/Pass/Routine)
    linkStyle default stroke-width:3px,fill:none,stroke:#00E676,color:#00E676

    %% --- NEON RED (Critical / Fail / Risk / Crisis) ---
    %% Indices: 12, 13, 25, 27, 28, 33, 36, 37, 39, 40, 48, 52, 62
    linkStyle 12,13,25,27,28,33,36,37,39,40,48,52,62 stroke:#FF1744,stroke-width:3px,color:#FF1744

    %% --- NEON BLUE (Memory / Data / Logs / Feedback) ---
    %% Indices: 15-22, 29, 32, 34, 42, 53, 60, 61, 68
    linkStyle 15,16,17,18,19,20,21,22,29,32,34,42,53,60,61,68 stroke:#2979FF,stroke-width:3px,color:#2979FF

    %% --- NEON PURPLE (Thick Context Lines) ---
    %% Indices: 64, 65, 66, 67
    linkStyle 64,65,66,67 stroke:#D500F9,stroke-width:5px,color:#D500F9

    %% Subgraph styling
    style Layer0 fill:#ffffff,stroke:#333,stroke-width:2px
    style Layer1 fill:#fcf8fd,stroke:#f3e5f5,stroke-width:2px
    style Layer2 fill:#eef9fe,stroke:#e1f5fe,stroke-width:2px
    style Layer3 fill:#f4f8fe,stroke:#e8f0fe,stroke-width:2px
    style Layer4 fill:#f1f8e9,stroke:#e6f4ea,stroke-width:2px
    style Layer5 fill:#e0f2f1,stroke:#b2dfdb,stroke-width:2px
    style LayerMemory fill:#fffde7,stroke:#fff9c4,stroke-width:2px,stroke-dasharray: 5 5

    style Inputs fill:#ede7f6,stroke:#b39ddb,stroke-width:2px,stroke-dasharray: 3 3
    style Context fill:#ffebee,stroke:#ef9a9a,stroke-width:2px,stroke-dasharray: 3 3
    style InputZone fill:none,stroke:none
    style Tools fill:#ffffff,stroke:#7b1fa2,stroke-width:2px
