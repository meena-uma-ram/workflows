# Global CRM Transformation — Operating Model Workflow

> A global CRM transformation is not just a technology project. It's a people, process, and governance project.

Guiding question: **How do we help salespeople spend less time on administration and more time finding leads, building relationships, and closing deals?**

The model is split into connected sub-workflows. Each diagram below is a node graph (rendered by GitHub's Mermaid support). The same nodes and edges are available in machine-readable form in [`workflow.json`](workflow.json).

**Interactive version:** [`index.html`](index.html) is a self-contained node map of all eight sub-workflows. Download it and open it in a browser (or serve the repo with GitHub Pages). It supports pan and zoom, click-through to each node's inputs and outputs, a step-by-step walk-through, search, and per-node "done" tracking saved in your browser.

| # | Sub-workflow | Source principle |
| --- | --- | --- |
| A | [End-to-end customer journey](#a-end-to-end-customer-journey) | 1, 5, 6 |
| B | [Tool integration](#b-tool-integration) | 2 |
| C | [Global standard, local flexibility](#c-global-standard-local-flexibility) | 3 |
| D | [Change control and decision rights](#d-change-control-and-decision-rights) | 4 |
| E | [Country-by-country rollout](#e-country-by-country-rollout) | 7 |
| F | [Balanced scorecard](#f-balanced-scorecard) | 8 |
| G | [Continuous improvement cadence](#g-continuous-improvement-cadence) | 9 |
| H | [Guiding principles](#h-guiding-principles) | 10 |

---

## A. End-to-end customer journey

One connected workflow across the whole lifecycle, with evidence-driven gates so customer information never disappears between teams.

```mermaid
flowchart TD
    A1["1. Lead generation"] --> G1{"ICP fit AND enough info<br/>to reach the right person?"}
    G1 -- No --> X1["Nurture or disqualify<br/>(reason logged)"]
    G1 -- Yes --> A2["2. Research & ICP assessment"]
    A2 --> A3["3. Personalized outreach sequence<br/>clear next action at every step"]
    A3 --> G2{"Engaged?"}
    G2 -- "No, sequence complete" --> X2["Exit or nurture path"]
    X2 -. "re-engages" .-> A3
    G2 -- Yes --> A4["4. Discovery & meeting management"]
    A4 --> A5["5. Structured meeting notes & action tracking<br/>needs · objections · stakeholders · decisions · owners"]
    A5 --> A6["6. Business case & ROI validation"]
    A6 --> G3{"Original value<br/>proposition strong?"}
    G3 -- No --> A6b["Investigate alternative value drivers<br/>revenue growth · retention · risk reduction"]
    A6b --> G4{"Credible business case?"}
    G4 -- No --> X3["Document reason &<br/>reconsider opportunity"]
    G4 -- Yes --> A7
    G3 -- Yes --> A7["7. Proposal tied to business case<br/>(actively followed up)"]
    A7 --> A8["8. Negotiation, legal review<br/>& contract signature"]
    A8 --> A9["9. Closed-Won handoff package<br/>objectives · expected ROI · tech requirements<br/>stakeholders · risks · commitments · milestones"]
    A9 --> A10["10. Implementation<br/>deployment & training"]
    A10 --> A11["11. Customer Success<br/>onboarding · adoption · time-to-value"]
    A11 --> A12["12. Measure outcomes<br/>time-to-value & customer outcomes,<br/>not just logins"]
    A12 --> CI(["Continuous improvement<br/>(see G)"])
    CI -. "process refinements" .-> A1

    classDef gate fill:#fff4d6,stroke:#c99a00,color:#222;
    classDef exit fill:#f3f3f3,stroke:#999,color:#555;
    classDef post fill:#e3f4ea,stroke:#2e8b57,color:#222;
    class G1,G2,G3,G4 gate;
    class X1,X2,X3 exit;
    class A9,A10,A11,A12 post;
```

**Ownership after signature:** Implementation owns deployment and training. Customer Success owns long-term adoption and value realization. Sales supports the transition where needed.

---

## B. Tool integration

Integrate the tools people already use instead of forcing them to abandon them. The objective is less administrative friction, not more CRM activity.

```mermaid
flowchart LR
    E["Email"] --> S["Sync & capture layer<br/>no duplicate data entry"]
    C["Calendar"] --> S
    N["Notes"] --> S
    O["Other sales tools"] --> S
    S --> H[("HubSpot CRM<br/>single source of truth")]
    H --> V["Rep view:<br/>pipeline & next actions"]
    H --> R["Leadership reporting"]
    V --> SE["Less admin,<br/>better sales execution"]
```

---

## C. Global standard, local flexibility

One global system, not eight disconnected ones.

```mermaid
flowchart TD
    subgraph GLOBAL["Global RevOps owns"]
        G1["System architecture"]
        G2["Core data structures"]
        G3["Global pipeline definitions"]
        G4["KPI definitions"]
        G5["Minimum standards"]
    end
    subgraph LOCAL["Country leadership owns"]
        L1["Day-to-day execution"]
        L2["Local practice adaptations<br/>within agreed boundaries"]
    end
    GLOBAL -- "boundaries" --> L2
    L2 --> EX["Local experiment"]
    EX --> EV["RevOps evaluates results"]
    EV --> D{"Evidence supports<br/>wider adoption?"}
    D -- Yes --> AD["Proposed as global standard<br/>(via Change Control, see D)"]
    D -- No --> KL["Stays local or retired"]
    AD --> GLOBAL
```

---

## D. Change control and decision rights

Every proposed change has a clear **driver, approver, consulted stakeholders, and informed teams**.

```mermaid
flowchart TD
    R["Change request<br/>driver · approver · consulted · informed"] --> CCB
    subgraph CCB["CRM Change Control Board"]
        direction LR
        RO["RevOps<br/>protects architecture & data integrity"]
        SA["Sales & Customer Success<br/>define needs, challenge friction"]
        LE["Legal & Privacy<br/>protect compliance"]
        CL["Country leaders<br/>local knowledge"]
    end
    CCB --> AS["Assess impact"]
    AS --> CF{"Major conflict?"}
    CF -- Yes --> ESG["Executive steering group<br/>decides"]
    ESG --> T
    CF -- No --> T["Test"]
    T --> DOC["Document"]
    DOC --> AP{"Approved?"}
    AP -- No --> RJ["Rejected / returned<br/>with rationale"]
    AP -- Yes --> REL["Controlled release"]
    REL --> INF["Inform affected teams"]
```

---

## E. Country-by-country rollout

Eight countries, one at a time. A country does not go live just because configuration is finished — **technical readiness and business readiness both matter**.

```mermaid
flowchart TD
    S(["Next country"]) --> P1["1. Map & validate existing process"]
    P1 --> P2["2. Design global workflow +<br/>country-specific adaptations"]
    P2 --> P3["3. Integrate tools & configure HubSpot"]
    P3 --> P4["4. Test workflows, data quality,<br/>reporting & handoffs"]
    P4 --> P5["5. Train users & prepare local support"]
    P5 --> GT{"Technical AND<br/>business ready?"}
    GT -- No --> FIX["Close gaps"]
    FIX --> P4
    GT -- Yes --> P6["6. Joint sign-off<br/>RevOps + country leadership"]
    P6 --> P7["7. Launch"]
    P7 --> P8["8. Hypercare (2–4 weeks)"]
    P8 --> ST{"System stable?"}
    ST -- No --> P8
    ST -- Yes --> P9["9. Transition to standard support"]
    P9 --> P10["10. Evaluate performance"]
    P10 --> MORE{"More countries<br/>remaining?"}
    MORE -- Yes --> S
    MORE -- No --> DONE(["All 8 countries live"])
```

---

## F. Balanced scorecard

```mermaid
flowchart LR
    AD["📊 Adoption<br/>Are employees using the<br/>intended workflows?"] --> SC
    DQ["📊 Data quality<br/>Can leadership trust the<br/>CRM and its reports?"] --> SC
    PE["📊 Process efficiency<br/>Are admin effort and<br/>delays decreasing?"] --> SC
    BO["📊 Business outcomes<br/>Conversion · pipeline health ·<br/>sales cycle · revenue"] --> SC
    SC[["Global scorecard<br/>consolidated by RevOps"]]
```

| Metric area | Owner |
| --- | --- |
| CRM and process metrics | RevOps |
| Sales outcomes | Sales |
| Post-sale outcomes | Customer Success |
| Global scorecard consolidation | RevOps |

---

## G. Continuous improvement cadence

```mermaid
flowchart TD
    W["Weekly country reviews<br/>identify operational problems, unblock teams"] --> M
    M["Monthly global reviews<br/>compare trends, recurring issues,<br/>evaluate successful local practices"] --> Q
    Q["Quarterly executive reviews<br/>business impact, resources,<br/>readiness for expansion"]
    Q -. "priorities" .-> W

    W --> CHK{"Mandatory standard<br/>missed?"}
    CHK -- Yes --> CA["RevOps sets corrective actions<br/>and deadline"]
    CA --> EXE["Country leadership executes"]
    EXE --> RE{"Resolved by deadline?"}
    RE -- Yes --> W
    RE -- "No (repeated failure)" --> ESC["Escalate to<br/>executive steering group"]
```

---

## H. Guiding principles

Governance is an enabler, not bureaucracy.

```mermaid
flowchart LR
    GS["Global standards"] --> CO["Consistency"]
    LO["Local ownership"] --> FL["Flexibility"]
    CA["Clear accountability"] --> AC["Action"]
    RD["Reliable data"] --> VI["Visibility"]
    CI["Continuous improvement"] --> SC["Scale"]
    CO & FL & AC & VI & SC --> OS(["An operating system<br/>for commercial growth"])
```

**Takeaway:** a CRM transformation succeeds when technology, processes, governance, and employee behaviour are designed together — not when a new system is simply switched on.
