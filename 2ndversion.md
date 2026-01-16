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

    %% --- LAYER 1: SENSING ---
    subgraph Layer1 [Layer 1: Multimodal Sensing]
        direction TB
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

    %% --- MAIN PROCESSING COLUMN ---
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

        %% --- LAYER 4: COGNITIVE SUPPLY CHAIN ---
        subgraph Layer4 ["Layer 4: Cognitive Supply Chain & Control"]
            direction TB
            
            StrategyComposer[Strategy Composer<br/>Execution Mode & Plan]:::analysis
            SupplyChain["Cognitive Supply Chain<br/>Manager"]:::action

            subgraph ContentFactory [Content Generation Engine]
                direction LR
                AudioGen["Audio Gen<br/>(Bus/Travel Mode)"]:::action
                VideoFetch["Video/Tutorial<br/>(Deep Dive Mode)"]:::action
                SummaryGen["Summary/Flashcards<br/>(Cram/Revision Mode)"]:::action
            end

            CapabilityGate[Capability Gate<br/>Safety & Consent Check]:::critical
            
            subgraph Enforcers [Actuators]
                direction LR
                AppLock["App Lock Service<br/>(Drift Prevention)"]:::critical
                TimeSched["Time Scheduler<br/>(Adaptive Blocks)"]:::action
                ContentDeliv["Content Delivery<br/>(Just-in-Time)"]:::action
            end
        end

        %% --- LAYER 5: ACCOUNTABILITY CONTRACT ---
        subgraph Layer5 ["Layer 5: Human-AI Contract & Accountability"]
            direction TB
            LiveNeg[Live Contract Negotiator<br/>Gemini Live]:::core
            UserCommit{Accepts?}:::user
            
            ConsequenceEng["Consequence &<br/>Enforcement Engine"]:::action
            RealAction((Real-World<br/>Study Session)):::action
            
            PoW{Proof-of-Work<br/>Verifier}:::analysis
            
            subgraph AdaptiveLogic [Adaptive Closure Engine]
                direction LR
                MasteryCheck[Mastery Evaluator<br/>Drill Down]:::analysis
                PacingEngine[Pacing Engine<br/>Extend/Reschedule]:::critical
                AdaptiveFeedback[Adaptive Feedback<br/>Slow/Fast Learner]:::memory
            end
        end
    end

    %% --- DATABASE MEMORY COLUMN (CLEANED & SIMPLIFIED) ---
    subgraph LayerMemory [Database Memory]
        direction TB
        %% 1. Student State (The "Now")
        StudentStateDB[(StudentStateDB<br/>Focus/Burnout/Stress)]:::memory
        
        %% 2. Thought Signature (The "History" & "Pattern")
        ThoughtSignature[(ThoughtSignatureStore<br/>Long-Horizon/Patterns)]:::memory
        
        %% 3. Outcome Learning (The "Optimization")
        OutcomeLearning[(OutcomeLearningDB<br/>Success/Strategies)]:::memory
        
        %% 4. Safety Audit (The "Trust")
        SafetyAudit[(SafetyAuditLog<br/>Panic/Intervention Log)]:::memory
    end

    %% ==========================================================
    %% === CONNECTION LOGIC ===
    %% ==========================================================

    %% -- 0. Identity Flow --
    Student --> Auth
    Auth --> Session
    Session --> Inputs
    Session --> Meaning
    Session --> Health
    Session --> OverrideFlag
    Session --> PrivacyPolicy

    %% -- 1. Standard Flow --
    Inputs --> Fusion
    Meaning --> Fusion
    Health --> Fusion
    OverrideFlag --> Fusion
    Fusion --> AnalysisNodes
    
    %% -- 2. Critical Fallbacks --
    Fusion -.->|Network Loss| Offline
    BudgetGuard -.->|Throttle/Cost| Offline
    
    %% -- 3. Analysis -> Core --
    AnalysisNodes --> Core
    
    %% -- 4. Memory I/O (UPDATED FOR NEW DBS) --
    StudentStateDB <--> Core
    ThoughtSignature <--> Core
    OutcomeLearning <--> Core
    SafetyAudit <--> Core

    AnalysisNodes -.->|Update| StudentStateDB
    OutcomeLearning --> PolicyLearner
    PolicyLearner -->|Optimization| Core
    
    %% -- 5. Core Logic Loops --
    Core --> BudgetGuard
    BudgetGuard --> Simulator
    Simulator -->|High Risk| Core
    Simulator -->|Viable| Confidence
    Confidence -->|Low Confidence| Explain
    Confidence -->|Abort| SafetyAudit
    
    %% Confidence -> Matrix
    Confidence -->|High Confidence| Matrix
    Explain --> LiveNeg
    Core -.-> SafetyAudit
    Core -.->|Model Degraded| Offline
    
    %% -- 6. LAYER 4: STRATEGY & SUPPLY CHAIN --
    Matrix --> StrategyComposer
    StrategyComposer --> SupplyChain
    
    %% Context-Aware Resource Fetching
    SupplyChain -->|Travel/Commute| AudioGen
    SupplyChain -->|Deep Dive| VideoFetch
    SupplyChain -->|Revision/Panic| SummaryGen
    
    %% Factory to Gate
    AudioGen --> CapabilityGate
    VideoFetch --> CapabilityGate
    SummaryGen --> CapabilityGate
    
    %% Gate Logic
    CapabilityGate --> LiveNeg
    
    %% -- 7. LAYER 5: INTERACTION & CONTRACT --
    LiveNeg --> UserCommit
    UserCommit -->|Yes| ConsequenceEng
    UserCommit -->|No/Negotiate| AdaptiveLogic
    
    %% Execution triggers Actuators
    ConsequenceEng --> AppLock
    ConsequenceEng --> TimeSched
    ConsequenceEng --> ContentDeliv
    
    %% Actuators drive Real Action
    AppLock --> RealAction
    TimeSched --> RealAction
    ContentDeliv --> RealAction
    
    %% -- 8. CLOSURE & ADAPTATION --
    RealAction --> PoW
    
    %% PoW Outcomes
    PoW -->|Pass| MasteryCheck
    PoW -->|Fail| PacingEngine
    
    %% Adaptation Loops (UPDATED FOR NEW DBS)
    MasteryCheck --> AdaptiveFeedback
    AdaptiveFeedback --> ThoughtSignature
    AdaptiveFeedback --> OutcomeLearning
    
    PacingEngine -->|Extend Block| TimeSched
    PacingEngine -->|Simplify Resource| SupplyChain
    
    %% -- 9. Thick Context Links --
    Fusion ==Context==> Stakes
    Fusion ==Context==> Pressure
    Fusion ==Context==> Tracker
    Fusion ==Context==> GoalHorizon
    Offline -.->|Sync| ThoughtSignature

    %% ==========================
    %% === STYLING APPLICATION ===
    %% ==========================

    linkStyle default stroke-width:3px,fill:none,stroke:#00E676,color:#00E676
    linkStyle 12,13,25,27,28,33 stroke:#FF1744,stroke-width:3px,color:#FF1744
    linkStyle 15,16,17,18,20,22 stroke:#2979FF,stroke-width:3px,color:#2979FF

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
