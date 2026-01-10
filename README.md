```mermaid
graph TD
    %% --- STYLING ---
    classDef gemini fill:#e8f0fe,stroke:#4285f4,stroke-width:2px,color:#000;
    classDef memory fill:#fce8e6,stroke:#ea4335,stroke-width:2px,color:#000;
    classDef action fill:#e6f4ea,stroke:#34a853,stroke-width:2px,color:#000;
    classDef critical fill:#fef7e0,stroke:#fbbc04,stroke-width:2px,stroke-dasharray: 5 5,color:#000;

    %% --- LAYER 1: VIBE-AWARE SENSING (INPUTS) ---
    subgraph "Layer 1: Omni-Sensing & Context"
        Ingest["Omni-Ingest<br/>(Syllabi, Emails, Portal)"] -->|Raw Data| Cache[("Context Cache<br/>(1M Token Window)")]
        Live["Gemini Live Interface<br/>(Voice/Video/Chat)"] -->|Audio Tone/Speed| Vibe["Vibe Telemetry<br/>(Anxiety/Fatigue)"]
        Live -->|Visuals| Vision["Visual Context<br/>(Messy Desk/Textbooks)"]
        Live -->|Explicit Statement| Health["Health State<br/>(Sick/Recovering)"]
        
        UserAmbition["User Ambition Vector<br/>(Goals: A+ vs Pass)"] --> Core
        Constraints["Hard Constraints<br/>(Job, Visa, Sleep)"] --> Core
    end

    %% --- LAYER 2: GEMINI 3 REASONING CORE (BRAIN) ---
    subgraph "Layer 2: The Strategist (Gemini 3 Pro)"
        Cache --> Core
        Vibe --> Core
        Vision --> Core
        Health --> Core
        
        Core["Gemini Reasoning Core<br/>(Thinking Level: HIGH)"]:::gemini
        Core -->|Proposed Plan| Simulator{"Deep Think<br/>Simulator"}:::gemini
        
        Simulator -->|High Failure Probability| Core
        Simulator -->|Viable Plan| DecisionMatrix{"Decision Matrix<br/>(Pressure vs. Stakes)"}
    end

    %% --- LAYER 3: GOVERNANCE & MEMORY (SAFETY) ---
    subgraph "Layer 3: Governance & Thought Vault"
        MetaAuditor["Meta-Cognitive Auditor<br/>(Velocity Score)"]:::memory --> Core
        
        ThoughtVault[("Thought Signature<br/>Vault")]:::memory
        Core -.->|Log Reasoning| ThoughtVault
        
        %% The Rejection Loop (The "Marathon" Feature)
        RejectionEvent(("Emergency<br/>Override")):::critical -->|Tag: TOXIC PATTERN| ThoughtVault
        ThoughtVault -->|Block Bad Logic| Core
    end

    %% --- LAYER 4: ADAPTIVE ACTION (EXECUTION) ---
    subgraph "Layer 4: Execution & Resilience"
        DecisionMatrix -->|Low Pressure| Routine["Routine Mode<br/>(Proactive Growth)"]
        DecisionMatrix -->|High Pressure| Crisis["Crisis Mode<br/>(Curriculum Triage)"]
        
        Routine --> Prep["Resource Orchestrator<br/>(Fetch Full Readings)"]:::action
        Crisis --> Triage["Compression Engine<br/>(Generate Audio Summaries)"]:::action
        
        Prep --> Negot["Negotiator"]
        Triage --> Negot["Negotiator"]
        
        Negot["Gemini Live Negotiator<br/>(Persuasive Coach)"]:::gemini --> UserAction(("User Action"))
        
        UserAction -->|Success| Mastery["Concept Mastery Check"]
        UserAction -->|Fail/Refuse| RejectionEvent
        
        Mastery -->|Score Update| MetaAuditor
    end

    %% --- CONNECTIONS ---
    class Core,Simulator,Negot gemini;
    class ThoughtVault,Cache,MetaAuditor,Cache memory;
    class Prep,Triage,Routine,Crisis action;
    class RejectionEvent,Health critical;
