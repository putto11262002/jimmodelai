# Product Design System Document: Problem & Opportunity Definition

---

## Component Overview

This document outlines the **Problem & Opportunity Definition** component of our
Product Design System. It is the foundational "why" for any product or feature,
ensuring all subsequent work is aligned with a clearly identified problem and
desired business outcomes.

### Purpose of this Component (`problem_definition.md`)

This file provides the **template and guidelines** for the AI Agent to define
the **problem statement, target audience, success metrics, and strategic
alignment** for a given initiative. It acts as the blueprint for creating the
corresponding `Problem & Opportunity Artifact` in the `artifacts/` directory.

### How this Component Fits in the Workflow

- **Upstream Dependencies:** This component has no direct upstream dependencies
  within the system; it is the **starting point** for any new product or feature
  initiative.
- **Downstream Impact:** All subsequent product design and technical decisions
  in components like `Product Concept & Core Requirements` and
  `Technical Design & Architecture` must **directly refer back to and justify
  their alignment** with the definitions established here. It sets the scope and
  validates the necessity of all later work.

---

## Guidance for AI Agent: Problem & Opportunity Definition (The "HOW-TO")

This section provides specific instructions and methodologies for the AI Agent
when assisting in the creation of the Problem & Opportunity Definition artifact.
The agent MUST strictly adhere to these guidelines, applying its core
operational rules (defined in `docs/pm/index.md`) contextually here.

### Agent & Human Collaboration Behavior for Problem & Opportunity Definition

- **Principle:** The agent's goal is to collaboratively guide the human user
  through a structured definition process, ensuring precision and strategic
  alignment, while enabling human oversight and decision-making at critical
  junctures. This refines the "Collaborative Guidance with Explicit
  Confirmation" rule from the agent's core prompt.
- **Sequential Progression & Confirmation:**
  - The definition process should follow the artifact sections sequentially
    (1.1, then 1.2, then 1.3, then 1.4).
  - The **Agent MUST obtain explicit human confirmation** after sufficient
    clarity and content are achieved for each major section (1.1, 1.2, 1.3, 1.4)
    before proceeding to the next.
  - This confirmation is also required before any substantive draft content is
    committed to the artifact.
- **Proactive Contribution (Challenge & Suggestion):**
  - The agent is empowered to **proactively challenge** any unclear,
    inconsistent, or unvalidated input. Challenges must always be accompanied by
    a clear _rationale_ (e.g., "This seems inconsistent with X because Y,"
    "Clarifying this will improve downstream alignment").
  - The agent **MAY proactively suggest** alternative phrasings, additional
    considerations, or different approaches to offload human cognitive load or
    widen perspective. Suggestions must be presented with their _rationale_ and
    _potential benefit_.
- **Flagging for Human Review (Escalation):** Beyond standard clarification, the
  agent **MUST flag for explicit human review** (as per the Critical Review
  Flagging directive in its core prompt) if:
  - After applying internal frameworks and exhausting clarification,
    unresolvable ambiguity or conflicting information persists about the core
    problem or target audience.
  - The viability of the problem (e.g., lack of significant impact, no clear
    target persona) cannot be established despite elicitation.
  - External input (e.g., market research data, deep domain expertise beyond
    logical deduction) is critically needed to proceed.

### Specific Elicitation Techniques & Frameworks for Problem & Opportunity Definition

This section details the methodologies to be applied by the AI agent for
structured elicitation to populate each section of the artifact.

- **For Section 1.1: Problem Statement**

  - **Objective:** Formulate a concise, user-centric problem statement and
    quantify its negative impact.
  - **Elicitation Technique:** Employ iterative questioning akin to the **"5
    Whys"** to uncover root causes, or a **"Jobs-to-be-Done (JBTD)"** light
    approach to understand underlying user needs and obstacles.
  - **Elicitation Focus:** Guide the user to clearly define:
    - **Who** (the target user experiencing the problem)
    - **What** (the struggle/obstacle they face)
    - **When/Where** (the context in which it occurs)
    - **Why** (the underlying need/job that is unmet)
    - The **Direct, Quantifiable/Qualifiable Negative Impact** of the problem.
  - **Iteration Guidance:** Continue rounds of questioning until the problem
    statement is specific enough to clearly identify the user, their activity,
    their obstacle, and its impact, and can be concisely summarized.
  - **Sufficient Clarity & Completeness:** Achieved when all bracketed
    placeholders (`[ ]`) for Section 1.1 can be accurately populated.
  - **Fallback Logic:** If, after a maximum of **5 targeted rounds** of
    questioning, a clear and concise problem statement, sufficient to fill `[ ]`
    placeholders, cannot be formed, the agent **MUST flag for human review** and
    suggest a dedicated discovery session.

- **For Section 1.2: Target Audience**

  - **Objective:** Define the primary and secondary users impacted by the
    problem, leading to a concise persona summary.
  - **Elicitation Technique:** Structured elicitation for persona definition.
  - **Elicitation Focus:** Guide the user to define for each persona:
    - Their **Role** (e.g., "Marketing Manager").
    - Key **Daily Activities** impacted by the problem.
    - Specific **Pain Points** directly mapped from Section 1.1 affecting _this
      persona_.
    - Existing **Tools** or workarounds they currently use.
    - Their **Aspirations** related to the problem.
  - **Iteration Guidance:** Continue elicitation until a clear picture of how
    the problem manifests for each key persona is established.
  - **Sufficient Clarity & Completeness:** Achieved when all bracketed
    placeholders (`[ ]`) for Section 1.2 can be accurately populated and
    sufficient detail is collected for primary and any relevant secondary
    personas.

- **For Section 1.3: Desired Business Outcomes (Success Metrics)**

  - **Objective:** Define measurable objectives and key results (KPIs) that
    quantifiably define success.
  - **Elicitation Technique:** Guide the definition of KPIs using the **SMART**
    (Specific, Measurable, Achievable, Relevant, Time-bound) criteria. Link
    objectives directly to the negative 'Impact' defined in Problem Statement
    (Section 1.1).
  - **Elicitation Focus:** Guide the user to define:
    - A high-level **Objective** that directly addresses the 'Impact' from
      Section 1.1.
    - Specific, quantifiable **Key Results (KPIs)** that align with the
      objective.
    - **Baselines** (current state value) and **Targets** (desired state value)
      for each KPI.
  - **Iteration Guidance:** Refine each metric until it meets all SMART criteria
    and is unambiguously measurable. If quantification is difficult, prompt for
    qualitative proxies that can be eventually measured.
  - **Sufficient Clarity & Completeness:** Achieved when all bracketed
    placeholders (`[ ]`) for Section 1.3 are accurately populated, and each KPI
    is SMART compliant.

- **For Section 1.4: Strategic Alignment**
  - **Objective:** Position the initiative within broader organizational goals
    and identify explicit (non-technical) dependencies.
  - **Elicitation Technique:** Direct connection elicitation and dependency
    mapping.
  - **Elicitation Focus:** Guide the user to define:
    - How this initiative **supports broader company strategy** or key strategic
      pillars.
    - Any **non-technical business dependencies or prerequisites** (e.g.,
      external partnerships, policy changes, other internal initiatives).
  - **Iteration Guidance:** Continue elicitation until a clear, concise
    rationale for strategic fit and a comprehensive list of known non-technical
    prerequisites are established.
  - **Sufficient Clarity & Completeness:** Achieved when all bracketed
    placeholders (`[ ]`) for Section 1.4 are accurately populated.

---

## Validation Strategy for this Component (for AI Agent)

As the AI Agent, before marking this component's artifact as complete, you must
perform the following validation checks:

- **Completeness Check:**
  - Confirm all sections (1.1 to 1.4) and their sub-components are fully
    populated.
  - Verify that no bracketed placeholders (`[ ]`) remain in the generated
    artifact.
- **Consistency & Cohesion Check:**
  - **Problem-Target Audience Link:** Ensure the identified "Key Pain Points
    Addressed" for each persona directly map to the "Problem Statement" (1.1).
  - **Impact-Outcome Link:** Validate that "Desired Business Outcomes (Success
    Metrics)" directly address and quantify the resolution of the negative
    "Impact" defined in the Problem Statement.
- **Measurability & Specificity Check (for Metrics):**
  - For each KPI, verify that a clear "Baseline" and "Target" (where applicable)
    are provided and are quantifiable.
  - Ensure metrics are unambiguous and not open to subjective interpretation.
- **Logical Flow Check:**
  - Read through the entire generated artifact to ensure a coherent narrative
    from problem to strategic alignment. Is the "why" clearly articulated and
    justified?
- **Proactive Challenge on Inconsistency:** If any ambiguities or
  inconsistencies are detected during validation that cannot be resolved
  automatically (e.g., conflicting information received, missing critical
  context), the agent MUST proactively challenge the user/data, provide
  rationale, and if unresolved, **flag the artifact for human review** with
  specific observations and suggested questions.

---

## Artifact Definition: Problem & Opportunity Artifact

This section defines the content structure for the **Problem & Opportunity
Artifact** that will be generated and managed by the AI Agent.

### Artifact Storage Location:

`artifacts/problem_definition/[PRODUCT_OR_FEATURE_NAME].md`

### Artifact Structure & Content Requirements:

- All bracketed placeholders (`[ ]`) within the artifact MUST be populated with
  specific, relevant information.
- All `AI Agent Guideline` comments within the template are for the AI Agent's
  internal process and should **NOT** be included in the final generated
  artifact.

---

### 1.1 Problem Statement

- **Purpose:** To clearly articulate the core problem(s) that the product or
  feature aims to solve.
- **Content:**
  - **Problem:** [Briefly yet comprehensively state the core problem being
    addressed. Focus on: who experiences it, what they are trying to do, and the
    obstacles they face. Use specific examples if possible.]
    - `[Example - User facing problem that impacts their workflow or experience]`
  - **Impact:** [Quantify the negative impact of this problem (e.g., lost
    revenue, increased churn, reduced efficiency). Provide metrics or anecdotal
    evidence. State the current undesirable state.]
    - `[Example - Quantifiable impact in terms of time, money, or user satisfaction]`

---

### 1.2 Target Audience

- **Purpose:** To define the primary and secondary users who experience the
  problem and will benefit from the solution.
- **Content:**
  - **Primary Users:**
    - `Role`: [Specific user role, e.g., Marketing Manager, Internal
      Administrator, External Customer]
    - `Persona Summary`: [Brief description of their goals, typical day,
      existing tools, and how they are affected by the problem. Emphasize their
      direct relationship to the "Problem & Impact" defined above.]
    - `Key Pain Points Addressed`: [Specific pain points from section 1.1 that
      this user role experiences and this initiative directly resolves.]
  - **Secondary Users (if any):**
    - `Role`: [Another user role]
    - `Persona Summary`: [Brief description of their auxiliary role or indirect
      impact.]
    - `Key Pain Points Addressed`: [Specific pain points relevant to them.]

---

### 1.3 Desired Business Outcomes (Success Metrics)

- **Purpose:** To define the measurable objectives and key results that quantify
  the success of addressing the identified problem.
- **Content:**
  - **Objective:** [High-level business goal. What strategic objective does this
    initiative support? This should directly address the "Impact" from section
    1.1.]
  - **Key Results (KPIs):** [Measurable metrics to track progress towards the
    objective. Define baseline and target values. KPIs must be SMART (Specific,
    Measurable, Achievable, Relevant, Time-bound).]
    - `Metric 1`: [Specific, measurable metric]
      - `Baseline`: [Current state value (e.g., "0 support tickets," "5%
        churn")]
      - `Target`: [Desired state value (e.g., "Reduce to 0.5 support
        tickets/day," "Reduce churn to 3% within 6 months")]
    - `Metric 2`: [Specific, measurable metric]
      - `Baseline`: [Current state value]
      - `Target`: [Desired state value]

---

### 1.4 Strategic Alignment

- **Purpose:** To position the initiative within the broader organizational
  goals and identify external factors influencing its execution.
- **Content:**
  - **Link to Company Strategy:** [Explain how this initiative supports broader
    company goals or strategic pillars (e.g., "Supports 'Customer-First'
    Initiative," "Increases Market Share in X Segment").]
  - **Dependencies/Prerequisites (Business):** [Are there any strategic business
    activities, external partnerships, policy decisions, or existing systems
    that this initiative relies upon or impacts before it can proceed? This
    helps identify non-technical external blockers.]
