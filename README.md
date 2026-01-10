```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#e3f2fd', 'edgeLabelBackground':'#ffffff', 'tertiaryColor': '#fdfefe'}}}%%
graph TD
    %% --- STYLING & PALETTE ---
    %% Increased font-size to 20px for all nodes to make shapes bigger and text readable
    %% Increased stroke-width to 4px/5px for bold outlines
    classDef sensing fill:#f3e5f5,stroke:#7b1fa2,stroke-width:4px,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef analysis fill:#e1f5fe,stroke:#0277bd,stroke-width:4px,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef core fill:#e8f0fe,stroke:#1565c0,stroke-width:5px,color:#000,font-weight:bold,font-size:20px,rx:5,ry:5
    classDef memory fill:#fff8e1,stroke:#fbc02d,stroke-width:4px,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef action fill:#e6f4ea,stroke:#2e7d32,stroke-width:4px,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef critical fill:#ffebee,stroke:#c62828,stroke-width:4px,stroke-dasharray: 5 5,color:#000,font-weight:bold,rx:5,ry:5,font-size:20px
    classDef user fill:#e0f7fa,stroke:#006064,stroke-width:4px,color:#000,shape:circle,font-weight:bold,font-size:20px

    %% --- LAYER 1: SENSING (INPUTS) ---
    subgraph Layer1 [Layer 1: Multimodal Sensing]
        direction TB
        Student((Student)):::user
        
        %% Grouping Inputs and Context side-by-side to reduce vertical whitespace
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
            Core[Gemini Reasoning Core<br/>Long-Context + Tools]:::core
            Simulator{Deep Think<br/>Simulator}:::core
            Matrix{Decision Matrix<br/>Pressure vs Stakes}:::core
            Explain[Explainability<br/>Why This Plan?]:::core
            Confidence{Confidence Estimator<br/>Certainty Guard}:::core
        end

        %% --- LAYER 4: EXECUTION MODES ---
        subgraph Layer4 [Layer 4: Execution Modes]
            direction TB
            
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
        AuditLog[(Audit Log<br/>Transparency)]:::memory
        ImpactMetrics[(Impact Metrics<br/>Success)]:::memory
        MotivationIndex[(Motivation Health<br/>Burnout/Reward)]:::memory
    end

    %% ==========================================================
    %% === CONNECTION DEFINITIONS & STYLING ===
    %% ==========================================================
    
    %% -- 1. Standard Flow (Layer 1 -> 2) --
    Student --> Inputs
    Inputs --> Fusion
    Meaning --> Fusion
    Health --> Fusion
    OverrideFlag --> Fusion
    Fusion --> AnalysisNodes
    
    %% -- 2. Critical Fallbacks (Layer 2) --
    Fusion -.->|Network Loss| Offline
    
    %% -- 3. Analysis -> Core (Layer 2 -> 3) --
    AnalysisNodes --> Core
    
    %% -- 4. Memory I/O (Blue Logic) --
    Cache <--> Core
    History <--> Core
    Vault <--> Core
    MotivationIndex <--> Core
    ImpactMetrics -->|Optimization| Core
    
    %% -- 5. Core Logic Loops --
    Core --> Simulator
    Simulator -->|High Risk| Core
    Simulator -->|Viable| Confidence
    Confidence -->|Low Confidence| Explain
    Confidence -->|High Confidence| Matrix
    Explain --> Live
    Core -.-> AuditLog
    Core -.->|Model Degraded| Offline
    AuditLog --> ImpactMetrics
    
    %% -- 6. Execution Decisions (Layer 3 -> 4) --
    Matrix -->|Low Pressure| Routine
    Matrix -->|High Pressure| Crisis
    Matrix -->|Panic| Safety
    
    %% -- 7. Mode Actions --
    Routine --> Prep
    Prep --> Personalize
    Personalize --> Curric
    
    Crisis --> Triage
    Triage --> Personalize
    
    Safety --> Alert
    
    %% -- 8. Interaction Setup (Layer 4 -> 5) --
    Curric --> Live
    Personalize --> Live
    
    %% -- 9. User Interaction Loop --
    Live --> UserDecision
    UserDecision -->|NO| Trust
    Trust --> Vault
    UserDecision -->|YES| Enforce
    Enforce --> Action
    Action --> Check
    
    %% -- 10. Outcomes --
    Check -->|Pass| Reward
    Reward --> Mastery
    Mastery --> Update
    Update --> History
    Update --> MotivationIndex
    Check -->|Fail| Recovery
    Recovery --> Prep

    %% -- 11. Thick Context Links --
    Fusion ==>|Context| Stakes
    Fusion ==>|Context| Pressure
    Fusion ==>|Context| Tracker
    Fusion ==>|Context| GoalHorizon
    Offline -.->|Sync| History

    %% ==========================
    %% === LINK STYLING RULES ===
    %% ==========================

    %% DEFAULT: GREEN (Standard Flow) - Increased to 4px
    linkStyle default stroke-width:4px,fill:none,stroke:#2e7d32,color:#2e7d32

    %% RED PATHS (Critical / Fail / Alert) - Increased to 4px or 5px
    linkStyle 6 stroke:#c62828,stroke-width:4px,stroke-dasharray: 5 5
    linkStyle 16 stroke:#c62828,stroke-width:4px,stroke-dasharray: 5 5
    linkStyle 17 stroke:#c62828,stroke-width:4px,stroke-dasharray: 5 5
    linkStyle 20,21 stroke:#c62828,stroke-width:5px
    linkStyle 25 stroke:#c62828,stroke-width:4px
    linkStyle 28 stroke:#c62828,stroke-width:4px
    linkStyle 33 stroke:#c62828,stroke-width:4px
    linkStyle 43 stroke:#c62828,stroke-width:4px,stroke-dasharray: 5 5

    %% BLUE PATHS (Memory / Data / Logging) - Increased to 3px/4px
    linkStyle 8,9,10,11 stroke:#1565c0,stroke-width:3px,stroke-dasharray: 3 3
    linkStyle 12,18,19 stroke:#1565c0,stroke-width:3px,stroke-dasharray: 3 3
    linkStyle 34,41 stroke:#1565c0,stroke-width:3px,stroke-dasharray: 3 3
    linkStyle 42 stroke:#1565c0,stroke-width:3px,stroke-dasharray: 3 3
    linkStyle 48 stroke:#1565c0,stroke-width:3px,stroke-dasharray: 3 3

    %% BOLD CONTEXT LINES (Purple/Teal) - Increased to 6px
    linkStyle 44,45,46,47 stroke:#7b1fa2,stroke-width:6px

    %% ZONE STYLING
    style Layer1 fill:#fcf8fd,stroke:#f3e5f5,stroke-width:2px
    style Layer2 fill:#eef9fe,stroke:#e1f5fe,stroke-width:2px
    style Layer3 fill:#f4f8fe,stroke:#e8f0fe,stroke-width:2px
    style Layer4 fill:#f1f8e9,stroke:#e6f4ea,stroke-width:2px
    style Layer5 fill:#e0f2f1,stroke:#b2dfdb,stroke-width:2px
    style LayerMemory fill:#fffde7,stroke:#fff9c4,stroke-width:2px,stroke-dasharray: 5 5

    %% Specific Subgraph Styling for Layer 1 Inputs
    style Inputs fill:#ede7f6,stroke:#b39ddb,stroke-width:2px,stroke-dasharray: 3 3
    style Context fill:#ffebee,stroke:#ef9a9a,stroke-width:2px,stroke-dasharray: 3 3
    style InputZone fill:none,stroke:none
    style Layer4 fill:#f1f8e9,stroke:#e6f4ea,stroke-width:2px
    style Layer5 fill:#e0f2f1,stroke:#b2dfdb,stroke-width:2px
    style LayerMemory fill:#fffde7,stroke:#fff9c4,stroke-width:2px,stroke-dasharray: 5 5
    linkStyle 41 stroke:#7b1fa2,stroke-width:2px,stroke-dasharray: 2 2
