# Product Design System Document: Task Scoping & Construction

---

## Component Overview

This document outlines the **Task Scoping & Construction** component of our
Product Design System. Its purpose is to systematically identify and consolidate
all required tasks (functional, foundational, non-functional, research, etc.) by
analyzing granular details from upstream product and technical specifications.
It then structures these tasks for direct creation in **GitHub Issues** and
management within **GitHub Projects** boards.

### Purpose of this Component (`task_scoping.md`)

This file provides the **template and guidelines** for the AI Agent to perform
the overall process of **task identification, de-duplication, consolidation,
scoping, and formatting** into executable GitHub CLI commands. It ensures that
each GitHub Issue (for Epic, Feature, or granular Task) is self-contained and
actionable for LLM Development Agents.

### How this Component Fits in the Workflow

- **Upstream Dependencies:** This component is primarily a consumer of detailed
  specifications. It **draws heavily from:**
  - `Product Concept & Core Requirements`: For identifying Epics and high-level
    Feature concepts.
  - `Product Feature Specifications`: For detailed Feature scope, User Stories,
    Functional Requirements, and Acceptance Criteria.
  - `Technical Planning (Component Level)`: For detailed technical
    implementation aspects, research spikes, and non-functional work.
  - `High-Level Technical Design`: For foundational architectural tasks.
  - `Problem & Opportunity Definition`: For ensuring tasks ultimately tie back
    to the problem being solved and strategic alignment.
  - **Relevant Upstream Links:**
    - Problem & Opportunity Definition:
      [`docs/pm/problem_definition.md`](./problem_definition.md)
    - Product Concept & Core Requirements:
      [`docs/pm/product_concept_requirements.md`](./product_concept_requirements.md)
    - High-Level Technical Design:
      [`docs/pm/technical_design.md`](./technical_design.md)
    - Product Feature Specifications:
      [`docs/pm/product_feature_specifications.md`](./product_feature_specifications.md)
    - Technical Planning:
      [`docs/pm/technical_planning.md`](./technical_planning.md)
- **Downstream Impact:** The output of this component is a set of `gitHub CLI`
  commands that directly create structured issues in GitHub, ready for execution
  and tracking within a GitHub Project board. These issues are designed to be
  consumed by both human engineers and **LLM Development Agents** due to their
  self-contained nature.
  - **Relevant Downstream Systems:** GitHub Issues, GitHub Projects.

---

## Guidance for AI Agent: Task Scoping & Construction (The "HOW-TO")

This section provides specific instructions and methodologies for the AI Agent
when assisting in task scoping and construction for GitHub. The agent MUST
strictly adhere to these guidelines, applying its core operational rules
(defined in `docs/pm/index.md`) contextually here.

### Agent & Human Collaboration Behavior for Task Scoping & Construction

- **Principle:** The agent should act as a meticulous orchestrator, synthesizing
  information from diverse sources into a coherent, actionable task inventory,
  formatted for direct GitHub CLI creation, while seeking human clarification
  for ambiguities in scope or priority. Each generated GitHub Issue must be
  self-contained and actionable for an LLM Development Agent.
- **Sequential Progression & Confirmation:**
  - The agent should first confirm access to all required upstream artifacts.
  - The **Agent MUST obtain explicit human confirmation** after generating a
    consolidated draft of the `gh issue create` command scripts, and again after
    proposed refinements or prioritization changes.
- **Proactive Contribution (Challenge & Suggestion):**
  - The agent is empowered to **proactively challenge** any identified work item
    (Epic, Feature, Task) that seems redundant, vaguely defined, or lacking
    clear linkage to a parent requirement (feature/component/NFR). Challenges
    must include a clear _rationale_.
  - The agent **MAY proactively suggest** common task breakdowns, optimal
    grouping strategies, or propose standard labels based on GitHub best
    practices.
- **Flagging for Human Review (Escalation):** The agent **MUST flag for explicit
  human review** (as per the Critical Review Flagging directive in its core
  prompt) if:
  - Conflicting requirements from different upstream documents lead to
    unresolvable task ambiguities.
  - The estimated scope of generated work items seems to grossly exceed the
    defined MVP or target iteration scope.
  - Critical prioritization decisions are required due to identified
    inter-dependencies or resource constraints.

### Specific Agent Elicitation Techniques & Frameworks for Task Scoping & Construction

This section details the methodologies to be applied by the AI agent for
structured elicitation and generation of GitHub CLI commands.

- **Initial Setup & Project Context:**

  - **Objective:** Obtain the target GitHub Project context.
  - **Elicitation:** The agent **MUST ask the human user to provide the exact
    GitHub Project Name** (as it appears in GitHub) where these issues should be
    created. This value will be used directly in the `gh issue create` commands.
  - **Agent Action:** Store this project name for all subsequent `gh` commands
    created in the separate script files.

- **For Epic Identification & `gh issue create` Generation:**

  - **Objective:** Identify overarching Epics and generate their corresponding
    GitHub `type:epic` issues.
  - **Elicitation Technique:** Parse `Product Concept & Core Requirements`
    (e.g., from `Objective` or major feature groupings) to identify top-level
    work initiatives.
  - **Content Generation for `--body`:**
    - Summarize the Epic’s overarching goal, alignment with
      `Problem & Opportunity Definition`, and key value proposition.
    - **Crucially:** Directly embed relevant excerpts from
      `Product Concept & Core Requirements` that define the Epic's scope and
      purpose.
    - Include a link to the full `Product Concept & Core Requirements` document
      for deep context.
  - **Command Formulation:** Generate
    `gh issue create --title "[Epic Title]" --body "[Formatted Description]" --label "type:epic" --project "$GITHUB_PROJECT_NAME"`
  - **Linking:** Establish an internal placeholder (e.g., `_EPIC_[Epic Title]_`)
    for subsequent Feature issues to link to.

- **For Feature Identification & `gh issue create` Generation:**

  - **Objective:** Identify individual Features for each Epic and generate their
    corresponding GitHub `type:feature` issues.
  - **Elicitation Technique:** Parse `Product Feature Specifications` to
    enumerate features within an Epic.
  - **Content Generation for `--body`:**
    - Summarize the Feature's purpose and its contribution to the parent Epic.
    - **Crucially:** Directly embed **all associated User Stories, Functional
      Requirements, and Acceptance Criteria** from
      `Product Feature Specifications`. Ensure ACs are clear, testable, and
      actionable for an LLM Development Agent (consider Gherkin format where
      suited).
    - Include a placeholder link to its parent Epic issue
      (`#[Epic Issue Number]`).
    - Include a link to the full `Product Feature Specifications` document for
      deep context.
  - **Command Formulation:** Generate
    `gh issue create --title "[Feature Title]" --body "[Formatted Description]" --label "type:feature" --project "$GITHUB_PROJECT_NAME"`
  - **Linking:** Establish an internal placeholder (e.g.,
    `_FEATURE_[Feature Title]_`) for subsequent granular Tssk issues to link to.

- **For Granular Task Identification & `gh issue create` Generation:**

  - **Objective:** Break down Features and Technical Plans into atomic,
    actionable development tasks and generate their corresponding GitHub Issue
    commands.
  - **Elicitation Technique:** Detailed analysis of
    `Product Feature Specifications` (for user stories, FRs, ACs) and
    `Technical Planning (Component Level)` (for design decisions, research
    spikes, specific implementation details).
  - **Content Generation for `--body`:**
    - Provide a clear, concise task description.
    - **Crucially:** For functional tasks, embed the relevant
      `Acceptance Criteria`. For technical tasks, embed critical technical
      details like API contracts, algorithm specifics, or a direct excerpt from
      the `Technical Planning` document relevant to this task.
    - Include a placeholder link to its parent Feature issue
      (`#[Feature Issue Number]`).
    - Include links to relevant sections of source `docs/` and `artifacts/` for
      human traceability (e.g., specific ACs from
      `product_feature_specifications.md`, design decision from
      `technical_planning.md`).
  - **Command Formulation:** Generate
    `gh issue create --title "[Task Title]" --body "[Formatted Description]" --label "type:[story/bug/spike/tech-debt]" --project "$GITHUB_PROJECT_NAME"`

- **Overall Command Consolidation & Human Instruction:**
  - **Output Per Epic:** The agent **MUST** generate a separate executable bash
    script (`.sh`) for _each Epic identified_.
  - **Script Content:** Each script will contain the `gh issue create` command
    for its Epic, followed by commands for all its Features, and then all the
    tasks for those Features.
  - **Placeholder Management:**
    1.  Each script will start with an intro/instruction block.
    2.  Human user will need to execute the script for each Epic sequentially.
    3.  Human user **MUST capture the actual GitHub Issue Numbers** assigned by
        GitHub for Epics and Features.
    4.  Human user **MUST manually replace the placeholder links**
        (`_EPIC_[Title]_`, `_FEATURE_[Title]_`) in the script itself (and the
        issue bodies if not handled by `gh cli` linking) with the actual GitHub
        Issue numbers (e.g., `#123`) for parent-child linking after issues are
        created.
  - **Output Example:** Demonstrate the bash script structure.

---

## Validation Strategy for this Component (for AI Agent)

As the AI Agent, before marking this component's artifact as complete, you must
perform the following validation checks:

- **Completeness Check:**
  - Confirm all required fields in the generated `gh issue create` commands are
    populated and correctly formatted.
  - Verify that no generic bracketed placeholders (`[ ]`) remain in the
    generated output.
- **Traceability Check:**
  - Ensure every generated Epic, Feature, and Task issue's description
    explicitly or implicitly links back to its higher-level requirement in the
    source `docs/` or `artifacts/` hierarchy.
  - Validate that placeholder links for parent/child relationships are correctly
    formatted to guide human linking.
- **Actionability & Self-Contained Check (for LLM Development Agents):**
  - Verify that the `--body` content for each Epic, Feature, and Task issue
    contains sufficient context, specific requirements (e.g., ACs), and relevant
    technical details to allow an LLM Development Agent to understand and
    execute the work item without excessive external lookups.
  - Ensure clarity, conciseness, and precision are maintained in all issue
    descriptions.
- **Consistency & Cohesion Check:**
  - Review the entire generated command set for internal consistency and logical
    flow, especially parent-child relationships.
- **Proactive Challenge on Inconsistency:** If any ambiguities or
  inconsistencies are detected during validation that cannot be resolved
  automatically, the agent MUST proactively challenge the user/data, provide
  rationale, and if unresolved, **flag the artifact for human review** with
  specific observations and suggested questions.

---

## Artifact Definition: Task Scoping & Construction Artifact (GitHub CLI Output)

This section defines the content structure for the **Task Scoping & Construction
Artifact** that will be generated and managed by the AI Agent. This output is
designed for direct execution via the GitHub CLI.

### Artifact Storage Location:

`artifacts/scripts/[EPIC_NAME].sh`

### Artifact Structure & Content Requirements:

Each generated artifact will be an executable bash script containing
`gh issue create` commands.

- Each script will begin with a clear explanation of its purpose and
  instructions for the human user.
- It will explicitly specify the GitHub Project Name derived from agent
  interaction.
- Commands will be ordered (Epic -> Features -> Tasks) to facilitate sequential
  execution and linking.
- Placeholders will be used for issue numbers (`_EPIC_[Title]_`,
  `_FEATURE_[Title]_`, etc.).

```bash
#!/bin/bash

# GitHub Issue Creation Script for Epic: [Epic Title]
# Generated by the AI Product Design System
# Date: [Current Date]
#
# This script contains GitHub CLI commands to create one Epic, its associated Features,
# and all their constituent Tasks. Each issue is designed to be self-contained for
# easy consumption by LLM Development Agents.
#
# GitHub Project Name: [User Provided Project Name - to be populated by agent interaction]
#
# Instructions for User:
# 1. Ensure you are authenticated with 'gh auth login' and have appropriate permissions.
# 2. Make sure the specified GitHub Project Name exists.
# 3. Before running, replace '$GITHUB_PROJECT_NAME' with the actual project name if you're not using an environment variable.
# 4. EXECUTE THIS SCRIPT.
# 5. IMMEDIATELY CAPTURE THE ISSUE NUMBER for the Epic created. You will need it for the Feature commands.
# 6. IMMEDIATELY CAPTURE THE ISSUE NUMBERS for the Features created. You will need them for the Task commands.
# 7. You will need to manually update the issue body's parent links (e.g., '_EPIC_Enhancing User Authentication_')
#    with the actual GitHub issue numbers (e.g., #123) AFTER all issues are created. These are placeholders only.

# Set the GitHub Project Name variable (ensure this matches your environment or replace it)
GITHUB_PROJECT_NAME="[User Provided Project Name - to be populated by agent interaction]"

# --- 1. Epic Creation Command ---
echo "Creating Epic: [Epic Title N]"
EPIC_ISSUE_URL=$(gh issue create --title "Epic: [Epic Title N]" \
  --body "### Goal & Value\n[Summarize Epic goal and value, from Product Concept & Core Req.]\n\n### Problem Alignment\n[Directly embed relevant Problem Def context.]\n\n### High-Level Scope\n[Overview of included deliverables.]\n\n[Link to relevant Product Concept & Core Requirements document, e.g., docs/pm/product_concept_requirements.md#epic-user-authentication]" \
  --label "type:epic" \
  --project "$GITHUB_PROJECT_NAME" | tail -1)
EPIC_ISSUE_NUM=$(basename "$EPIC_ISSUE_URL")
echo "Created Epic: $EPIC_ISSUE_URL (Issue #$EPIC_ISSUE_NUM)"
echo "Remember to link child Features to #$EPIC_ISSUE_NUM"

# --- 2. Feature Creation Commands for Epic: [Epic Title N] ---

echo "Creating Features for Epic: [Epic Title N]"

FEATURE_A_ISSUE_URL=$(gh issue create --title "Feature: [Feature Title A, e.g., Implement MFA via Authenticator App]" \
  --body "### Purpose\n[Summarize feature purpose from Product Feature Specs.]\n\n### Parent Epic\n#$EPIC_ISSUE_NUM\n\n### User Stories\n[Directly embed User Stories from Product Feature Specs.]\n\n### Functional Requirements\n[Directly embed Functional Requirements.]\n\n### Acceptance Criteria\n[Directly embed Acceptance Criteria (e.g., Gherkin) for LLM Dev Agent execution.]\n\n[Link to relevant Product Feature Specifications document, e.g., docs/pm/product_feature_specifications.md#feature-mfa-authenticator]" \
  --label "type:feature" \
  --project "$GITHUB_PROJECT_NAME" | tail -1)
FEATURE_A_ISSUE_NUM=$(basename "$FEATURE_A_ISSUE_URL")
echo "Created Feature: $FEATURE_A_ISSUE_URL (Issue #$FEATURE_A_ISSUE_NUM)"
echo "Remember to link child Tasks to #$FEATURE_A_ISSUE_NUM"

FEATURE_B_ISSUE_URL=$(gh issue create --title "Feature: [Feature Title B]" \
  --body "### Purpose\n[Summarize feature purpose.]\n\n### Parent Epic\n#$EPIC_ISSUE_NUM\n\n[... other feature details ...]" \
  --label "type:feature" \
  --project "$GITHUB_PROJECT_NAME" | tail -1)
FEATURE_S_ISSUE_NUM=$(basename "$FEATURE_B_ISSUE_URL")
echo "Created Feature: $FEATURE_B_ISSUE_URL (Issue #$FEATURE_B_ISSUE_NUM)"
echo "Remember to link child Tasks to #$FEATURE_B_ISSUE_NUM"


# --- 3. Task Creation Commands for Feature: [Feature Title A] ---
echo "Creating Tasks for Feature: [Feature Title A]"

gh issue create --title "Task: [Task Title 1 for Feature A, e.g., Backend API for MFA Setup]" \
  --body "### Description\n[Detailed task description. Directly embed ACs, relevant technical details from Tech Planning, HLD for LLM Dev Agent.]\n\n### Parent Feature\n#$FEATURE_A_ISSUE_NUM\n\n[Link to relevant Technical Planning document or Product Feature Specs section, e.g., docs/pm/technical_planning.md#component-auth-service]"\
  --label "type:story" \
  --project "$GITHUB_PROJECT_NAME"

gh issue create --title "Task: [Task Title 2 for Feature A, e.g., Develop Frontend MFA Setup UI]" \
  --body "### Description\n[Detailed task description. Directly embed ACs, relevant technical details from Tech Planning, HLD for LLM Dev Agent.]\n\n### Parent Feature\n#$FEATURE_A_ISSUE_NUM\n\n[Link to relevant Technical Planning document or Product Feature Specs section, e.g., docs/pm/technical_planning.md#component-frontend-ui]" \
  --label "type:story" \
  --project "$GITHUB_PROJECT_NAME"

# --- 4. Task Creation Commands for Feature: [Feature Title B] ---
echo "Creating Tasks for Feature: [Feature Title B]"
# ... similar gh issue create commands for tasks under Feature B ...

# --- End of Script ---
echo "Script complete. Please review created issues in GitHub."
echo "Remember to manually update any parent/child links in issue descriptions with actual issue numbers if they haven't auto-linked."
```
