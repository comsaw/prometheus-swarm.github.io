---
title: Usage Process
nav_order: 2
parent: How It Works
---

# From Idea to Code: The Prometheus Swarm Usage Process

Using Prometheus Swarm transforms your ideas into functional software through a structured, AI-driven workflow. Here's a step-by-step guide to the journey:

*   **1. Ideation & Scoping (Defining Your Vision):**
    *   **User Action:** You start by describing your project idea, goals, features, and any specific requirements in natural language. This can be a simple text description, a more detailed specification, or even a transcript of a design discussion.
    *   **Prometheus Action:** The system, often through an initial interaction with the Planner Agent, helps refine this input into a clear **Scope of Work**. It may ask clarifying questions to ensure all aspects are covered and ambiguities are minimized. The more detailed and clear your initial input, the better the outcome. The principle of "scope narrowly" is applied here, breaking the larger project into manageable pieces.

*   **2. Planning (The Blueprint by the Planner Agent):**
    *   **Prometheus Action:** Once the scope is finalized, the **Planner Agent** (utilizing a powerful LLM like GPT-4) converts the specification into a comprehensive development plan. This plan typically includes a list of software components, modules, features, their relationships, and acceptance criteria for each.
    *   **User Action (Optional):** You may have an opportunity to review and approve this plan, ensuring it aligns with your vision before full-scale code generation begins.

*   **3. Code Generation (The Swarm at Work - Builder Agents):**
    *   **Prometheus Action:** The development plan is broken down into tasks, which are then dispatched to a swarm of **Feature Builder Agents** operating in parallel across the decentralized Koii Network. Each agent takes on a specific module or feature, writing the necessary code, and often generating initial unit tests and documentation for its assigned piece. Each agent uses localized context (via `.kno` embeddings) to understand its specific task thoroughly.
    *   **User Action (Observation):** You can often monitor this process in real-time. Code commits and pull requests made by the agents may appear in the designated Git repository, offering transparency into the swarm's activity.

*   **4. Automated Testing (Quality Assurance by Red Team & Bug Finder Agents):**
    *   **Prometheus Action:** As code modules are completed, or once an initial version of the application is assembled, specialized QA agents swing into action:
        *   **Red Team Agents:** These agents attempt to "break" the software. They pull the codebase, deploy it in a sandbox, and run various tests, including potentially writing and executing attack scripts or use-case scenarios from an end-user perspective to find functional flaws.
        *   **Bug Finder Agents:** These agents perform static code analysis, security vulnerability scans, and other checks to identify issues in the codebase.
    *   **Iteration:** If tests fail or bugs are detected, the issues are reported. Builder agents (or specialized fixer agents) then address these problems, and the code is re-tested. This iterative loop continues until the generated code meets the quality standards and passes all checks.

*   **5. Optimization & Review (Refinement by the Architect Agent):**
    *   **Prometheus Action:** Once all components have been built and individually tested, an **Architect/Optimizer Agent** reviews the entire integrated codebase. This agent looks for opportunities to refactor, remove redundancies, improve overall structure, and ensure all parts fit together efficiently and coherently. Final documentation is also generated or polished during this phase.

*   **6. Delivery (Receiving Your Software):**
    *   **Prometheus Action:** The final, tested, and optimized codebase is made available to you.
    *   **User Action:** Since Prometheus Swarm uses Git for version control, the completed project is typically delivered as a Git repository (e.g., a main branch in your designated repo, or a fork you can merge or clone). This repository contains all the source code, tests, documentation, and potentially the `.kno` knowledge embeddings for future work.
    *   You can now run, deploy, and use your new software.

*   **7. Feedback & Iteration (Continuous Improvement):**
    *   **User Action:** Review the delivered software. If you need modifications, want to add new features, or have identified areas for improvement, you can re-engage Prometheus Swarm.
    *   **Prometheus Action:** The process can be repeated, using the existing codebase and your new requirements as input. The swarm will then work to update and enhance your project.

*   **Tips for Best Results:**
    *   **Be Specific:** The clearer and more detailed your initial idea and requirements, the better the swarm can interpret your needs.
    *   **Break Down Big Ideas:** If you have a very large project, consider breaking it into smaller, manageable phases or features for the swarm to tackle sequentially or in parallel.
    *   **Engage in Clarification:** If the system asks questions during the scoping phase, provide thorough answers.

*   **Visual Aid:** (Consider a flowchart here: Idea -> Scope -> Plan -> Code (Builder Agents) -> Test (Red Team/Bug Finder) -> Optimize (Architect) -> Deliver -> Iterate) 