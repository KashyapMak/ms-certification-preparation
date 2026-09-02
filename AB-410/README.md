# AB-410 Complete Exam Study Guide

## Index

- [1. Exam Snapshot](#1-exam-snapshot)
- [2. Domain Coverage Matrix](#2-domain-coverage-matrix)
- [3. Blueprint Changes and Course Gap Analysis](#3-blueprint-changes-and-course-gap-analysis)
- [4. Objective-by-Objective Study Notes](#4-objective-by-objective-study-notes)
  - [4.1 Design Microsoft Power Platform Solutions by Using AI-Enabled Tools](#41-design-microsoft-power-platform-solutions-by-using-ai-enabled-tools)
  - [4.2 Build Data Models](#42-build-data-models)
  - [4.3 Create Model-Driven Apps](#43-create-model-driven-apps)
  - [4.4 Create Canvas Apps](#44-create-canvas-apps)
  - [4.5 Create Cloud Flows](#45-create-cloud-flows)
  - [4.6 Create Prompts and Models in AI Hub](#46-create-prompts-and-models-in-ai-hub)
  - [4.7 Implement Business and Process Logic](#47-implement-business-and-process-logic)
- [5. High-Yield Facts Reference](#5-high-yield-facts-reference)
- [6. Service Selection Cheat Sheet](#6-service-selection-cheat-sheet)
- [7. Practice Questions](#7-practice-questions)
- [8. Final Revision Section](#8-final-revision-section)
- [9. REACT Scenario-Question Framework](#9-react-scenario-question-framework)
- [10. Environment, Security and ALM Quick References](#10-environment-security-and-alm-quick-references)
- [11. Power Fx Quick Reference](#11-power-fx-quick-reference)
- [12. Business Logic Decision Tree](#12-business-logic-decision-tree)
- [13. Prompt Engineering and Copilot Studio Cheat Sheets](#13-prompt-engineering-and-copilot-studio-cheat-sheets)
- [14. ALM Deployment Checklist](#14-alm-deployment-checklist)
- [15. Seven-Day Revision Plan](#15-seven-day-revision-plan)
- [16. Official Skills Coverage Matrix](#16-official-skills-coverage-matrix)
- [17. Extended 100-Question Practice Bank](#17-extended-100-question-practice-bank)
- [18. Five-Page Exam Cram](#18-five-page-exam-cram)
- [19. One-Page Revision Poster](#19-one-page-revision-poster)
- [20. References](#20-references)

> **Research status:** Researched on **2 September 2026** against the current Microsoft Learn certification page, AB-410 study guide (last updated 15 May 2026), official AB-410T00-A course, and every learning path/module listed in that course. The study guide is treated as the authoritative exam blueprint. Where Microsoft does not publish a fixed limit, command, or licensing entitlement, this guide says so rather than guessing.

## 1. Exam Snapshot

| Item | Official information |
|---|---|
| Exam name | **Exam AB-410: Building Intelligent Applications** |
| Exam code | **AB-410** |
| Certification earned | **Microsoft Certified: Intelligent Applications Builder Associate** |
| Level | Intermediate |
| Role focus | Developer; intelligent application building with Microsoft Power Platform |
| Skills measured | Foundation for intelligent applications; intelligent applications; business application logic and automation |
| Exam time | 120 minutes to complete the assessment |
| Passing score | **700 or greater** |
| Exam language currently listed | English |
| Date researched | 2 September 2026 |


### Direct official sources

- [Certification page](https://learn.microsoft.com/en-us/credentials/certifications/intelligent-applications-builder-associate)
- [AB-410 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-410)
- [Official course AB-410T00-A](https://learn.microsoft.com/en-us/training/courses/ab-410t00)
- [Exam sandbox](https://aka.ms/examdemo)
- [Exam scoring and score reports](https://learn.microsoft.com/en-us/credentials/certifications/exam-scoring-reports)

## 2. Domain Coverage Matrix

| Domain | Weight | Related official learning paths | Priority |
|---|---:|---|---|
| Create a foundation for intelligent applications | 25–30% | Get started with AI-first solutions; Build your data model with Microsoft Dataverse | 🔥 High Priority |
| Create intelligent applications | 25–30% | Build intelligent apps and portals with Microsoft Power Apps | 🔥 High Priority |
| Build business application logic and automation | 40–45% | Automate and extend your solutions with AI in Microsoft Power Automate; parts of the Dataverse path | 🔥 High Priority |

**Study allocation:** Spend roughly 45% of revision time on automation/business logic and divide the remainder across foundation and app creation. All three domains are high priority because even the smallest domain can represent around one quarter of the scored content.

## 3. Blueprint Changes and Course Gap Analysis

### Authoritative baseline

The current study guide was last updated **15 May 2026**. Microsoft states that most questions cover generally available features, but commonly used Preview features can appear. Microsoft does not publish a change log comparing this first/current AB-410 blueprint with an earlier version on the reviewed page.

### Course-to-blueprint mapping gaps

| Blueprint area | Course coverage | Gap/action |
|---|---|---|
| Solution analysis, built-in agents, extensibility, environment types, ALM | AI-first path gives design context and Plans | Blueprint is broader. Study environments, solutions, connection references, environment variables, pipelines, managed/unmanaged solutions, and agent selection separately. |
| Dataverse relationships, prompt columns, row summaries, public views, main forms | Data path emphasizes tables, columns, and security roles | Significant gap. Perform hands-on configuration of every listed artifact. |
| Generative pages, access to forms/views/apps, charts and dashboards | Model-driven modules cover core app composition and visual elements | Verify generative pages and role-based access separately in current product documentation. |
| Accessibility, responsiveness, Monitor, error handling, named formulas, user-defined functions, component libraries | Canvas modules provide broad app-building coverage | Blueprint requires greater implementation depth than the introductory course. |
| Create a Copilot Studio agent from a canvas app | Course introduces AI/agents broadly | Explicit blueprint objective, but not a dedicated AB-410 course module. Practise the maker experience. |
| Connector evaluation, conditions, loops, testing/troubleshooting | Power Automate path covers cloud flows, Dataverse, approvals | Study connector classification, trigger/action selection, run history, retries, expressions, loops and conditions in more depth. |
| AI Hub prompts: templates/blank, knowledge, model settings, inputs, app/flow consumption; AI models | One module focuses on Dataverse-grounded prompts | Major depth gap. Cover the full AI Hub objective independently. |
| Business process flows, calculated/rollup/formula columns, use-case evaluation | Business rules are mentioned in the data path | Blueprint extends further than course syllabus. Build each logic type hands-on. |
| Power Pages | Two course modules cover it | Power Pages is in the audience profile/prerequisites and course, but **no Power Pages task appears in the current detailed skills-measured bullets**. Treat as supporting context, not a weighted standalone objective. |

### New, retired, deprecated and preview status

- **New topics:** No official topic-change history was available on the reviewed study guide, so no topic is labelled “new” relative to an earlier blueprint.
- **Retired topics:** No retired objective list was published for AB-410 in the reviewed official sources.
- **Deprecated features:** The current blueprint does not identify any objective as deprecated. Do not infer deprecation from older names in module URLs.
- **Preview features:** The blueprint does not mark individual objectives as Preview. Microsoft explicitly warns that commonly used Preview features may be assessed. Check the status banner in the current product documentation and maker portal before the exam.
- **Terminology mismatch:** Some learning-module URLs retain historical terms such as “Common Data Service” or “entity,” while current exam language uses **Microsoft Dataverse**, **table**, and **column**.

## 4. Objective-by-Objective Study Notes

## Domain 1: Create a Foundation for Intelligent Applications (25–30%)

### 4.1 Design Microsoft Power Platform Solutions by Using AI-Enabled Tools

#### What You Need to Know

Official tasks:

- Analyze requirements to identify components and implementation options.
- Evaluate built-in agents to include in the solution.
- Recommend extensibility options.
- Recommend environment types.
- Apply a Microsoft Power Platform solution and ALM strategy.

**Core architecture mental model**

1. **Experience layer:** canvas app for task-focused, tailored UX; model-driven app for data/process-centric experiences; Power Pages for external web audiences.
2. **Data layer:** Dataverse for relational business data, metadata, security, auditing and native Power Platform integration.
3. **Automation layer:** Power Automate cloud flows for event-driven, scheduled, approval and cross-service automation.
4. **Intelligence layer:** AI Hub prompts/models and Copilot Studio agents.
5. **Lifecycle layer:** environments, solutions, pipelines, connection references, environment variables, governance and monitoring.

| Requirement | Prefer | Why |
|---|---|---|
| Highly tailored interaction or mobile task | Canvas app | Control-level layout and Power Fx behavior |
| Relational, process-heavy internal solution | Model-driven app | Metadata-driven forms, views, charts and security |
| External customer/partner self-service | Power Pages | Web experience over Dataverse with external identity/security |
| Deterministic event or scheduled orchestration | Cloud flow | Trigger/action workflow model |
| Conversational, multi-turn work using knowledge/actions | Copilot Studio agent | Agent orchestration and conversational experience |
| Natural-language generation inside an app/flow | AI Hub prompt | Reusable generative capability with defined inputs |

#### Mental Model & Decision Rules

- **Use built-in capability first** when it meets the requirement, is supportable, and reduces custom maintenance.
- **Use low-code extension** through connectors, custom connectors, Power Fx, components, flows and agents before custom code.
- **Use pro-code extension** only for requirements that low-code cannot satisfy, such as specialized APIs, plug-ins, PCF controls, Azure services or complex integrations.
- Separate **development**, **test**, and **production** when release control and risk justify it. Use a developer environment for individual development. Do not treat the default environment as a production ALM strategy.
- Build in **unmanaged solutions** in development. Deploy **managed solutions** to downstream controlled environments unless a specific lifecycle requirement dictates otherwise.
- Store configurable values in **environment variables** and connector bindings in **connection references**. Avoid environment-specific hard-coding.

#### Implementation Example

**Portal workflow**

1. In `make.powerapps.com`, select the correct development environment.
2. Create an unmanaged solution with an intentional publisher and prefix.
3. Add tables, apps, flows, prompts and required dependencies to the solution.
4. Replace hard-coded values with environment variables.
5. Ensure solution-aware flows use connection references.
6. Validate, export and deploy through a pipeline or controlled import.
7. Supply deployment settings for target-specific connections and variables.
8. Test security, functionality and automation in the target environment.

> **Command caution:** The AB-410 objectives are maker-focused and Microsoft does not require a specific CLI or PowerShell command in the blueprint. Power Platform CLI syntax can change. Use the current [Power Platform CLI documentation](https://learn.microsoft.com/en-us/power-platform/developer/cli/introduction) if command-line ALM is part of your practice; do not memorize unverified command switches.

#### Security, Governance & Operations

- Apply least privilege with environment roles, Dataverse security roles, app sharing and connector permissions.
- Use data policies to govern connector combinations and data movement.
- Treat prompts, agent knowledge and flow connections as governed solution assets.
- Use solutions for dependency tracking and repeatable deployment.
- Monitor flows, apps and downstream AI behavior after release.
- Cost depends on licenses, premium connectors, Dataverse capacity, AI consumption and agent usage. Microsoft does not publish one universal AB-410 license bundle or fixed cost.

#### Exam Gotchas ⚠️

- A solution is a container for ALM; it does not by itself grant users access to apps or data.
- Sharing an app does not automatically give the user Dataverse table privileges or access to every underlying connection.
- A conversational requirement does not automatically mean “build an agent.” A deterministic flow or embedded prompt may be simpler.
- Environment type selection and solution type are separate decisions.
- Preview status can change. Use the current maker-portal/documentation status, not old screenshots.

#### Scenario Patterns

**Scenario:** Values and connections differ between test and production.  
**Best choice:** Package assets in a solution, use environment variables for values and connection references for connector bindings. This avoids hard-coded environment dependencies and supports repeatable deployment.

**Scenario:** Users need to ask follow-up questions and invoke business actions.  
**Best choice:** A Copilot Studio agent, potentially calling flows/actions. A single AI prompt is not a complete multi-turn orchestration layer.

#### Quick Revision Summary

- Translate requirements into experience, data, automation, intelligence and lifecycle components.
- Prefer standard capability, then low-code extension, then pro-code.
- Build unmanaged in development; normally deploy managed downstream.
- Use environment variables and connection references.
- Security and sharing are separate from solution transport.
- Select agents for conversational, multi-turn orchestration rather than every AI use case.

### 4.2 Build Data Models

#### What You Need to Know

Official tasks cover: tables in the data workspace; standard tables; table properties; columns; relationships; prompt columns; row summaries; public views; main forms; and security.

**Key terms**

- **Table:** Metadata-defined business entity storing rows.
- **Standard table:** Microsoft-provided table that can often be extended.
- **Custom table:** Maker-created table for solution-specific data.
- **Primary name column:** Human-readable row identifier.
- **Choice:** Controlled option set; local or reusable/global depending on design.
- **Lookup:** Column representing a relationship to another table.
- **One-to-many / many-to-one:** One parent can relate to many child rows.
- **Many-to-many:** Rows on both sides can relate to multiple rows through an intersect relationship.
- **Ownership:** User/team-owned supports row-level ownership; organization-owned is shared at organization scope.
- **Public view:** Reusable Dataverse view available according to app/table access.
- **Main form:** Primary model-driven form experience for a row.
- **Prompt column:** AI-generated content configured at the data layer. Verify availability and feature status in the target environment.
- **Row summary:** AI-generated summary of row information. Verify current availability and supported configuration in official documentation/product UI.

#### Mental Model & Decision Rules

| Need | Choose |
|---|---|
| Reuse an established business concept | Extend an appropriate standard table |
| Unique domain concept | Create a custom table |
| Per-owner row access | User/team-owned table |
| Reference data available broadly | Organization-owned table |
| Controlled finite values | Choice column |
| Relate records and preserve relational behavior | Lookup/relationship, not duplicated text |
| Derived value evaluated from fields | Formula or calculated column, according to supported functions/behavior |
| Aggregate child rows | Rollup column |
| Human-friendly list for a persona | Public view with intentional columns, filtering and sorting |

Normalize data enough to avoid duplication, but design for the app and reporting patterns. Define relationship behavior deliberately, especially cascading assignment, sharing and deletion.

#### Implementation Example

1. Open a solution, then **Tables > New table**.
2. Set display/plural names, ownership and primary column.
3. Create required columns with correct data types, requirement levels and searchable/auditing settings.
4. Add lookups or explicit relationships.
5. Configure relationship behavior and validate cascade consequences.
6. Build a public view with only useful columns and filters.
7. Configure the main form, sections, tabs, controls and subgrids.
8. Add table privileges to a security role and test with a non-admin persona.
9. Add all assets to the solution and publish changes.

**Dataverse Web API conceptual example**

```http
POST https://<environment>.api.crm.dynamics.com/api/data/v9.2/<entity-set-name>
Authorization: Bearer <access-token>
Content-Type: application/json

{
  "<logical-name>": "Example value"
}
```

The concrete entity-set and logical column names come from the environment metadata. Do not substitute display names. Authentication and permission setup are outside this example.

#### Security, Governance & Operations

- Dataverse privileges include create, read, write, delete, append, append to, assign and share, with access depths where applicable.
- Users receive cumulative privileges from assigned security roles and team membership.
- Field security profiles can protect eligible sensitive columns, but do not replace table/row security.
- Use auditing where required and permitted; consider storage impact.
- Test as representative users. System Administrator behavior can hide security defects.
- Minimize unnecessary columns, relationships, synchronous logic and broad privileges.

#### Exam Gotchas ⚠️

- **Append** applies to the row being associated; **Append To** applies to the target row receiving the association.
- Hiding a form field is not data security.
- A view controls presentation, not row authorization.
- A lookup is not merely text; it creates a relationship.
- Organization-owned tables do not use user/team row ownership in the same way.
- Microsoft does not publish one exam-wide maximum for every table/column/relationship type. Limits vary by feature and tenant configuration; verify current service-protection and capacity documentation.

#### Scenario Patterns

**Scenario:** Regional managers should read all rows in their business unit, while staff work only with their own rows.  
**Best choice:** A user/team-owned table plus roles with appropriate business-unit and user access depths. A filtered view is not a security boundary.

**Scenario:** Orders must reference one customer, and one customer can have many orders.  
**Best choice:** A many-to-one lookup from Order to Customer, yielding a one-to-many relationship from Customer to Order.

#### Quick Revision Summary

- Start with business entities and relationships, then columns and UX artifacts.
- Extend standard tables when semantics match.
- Choose ownership before relying on row-level access.
- Know lookup and relationship cardinality.
- Views/forms shape experience; roles/ownership secure data.
- Prompt columns and row summaries are explicit blueprint items; verify current status hands-on.

## Domain 2: Create Intelligent Applications (25–30%)

### 4.3 Create Model-Driven Apps

#### What You Need to Know

Official tasks: forms, views, generative pages, app composition, access to forms/views/apps, charts and dashboards.

A model-driven app is composed from Dataverse metadata. The key assets are tables, forms, views, navigation, charts, dashboards and security roles.

#### Mental Model & Decision Rules

- Use model-driven apps where the data model and business process determine the experience.
- Use **main forms** for full row editing, **quick create** for rapid creation, **quick view** for read-only related information, and other form types only where their supported purpose matches.
- Use views to present persona-specific lists with deliberate filtering, sorting and columns.
- Use charts/dashboards for operational visualization, not as a replacement for Power BI when advanced analytics is required.
- Restrict forms using security-role assignments where appropriate; ensure users still have a form they can access.
- App access and Dataverse permissions must both be satisfied.

#### Implementation Example

1. Create a model-driven app inside a solution.
2. Add required Dataverse pages/tables.
3. Configure navigation groups and labels.
4. Select forms and views to include.
5. Create charts and a dashboard if required.
6. Save, validate and publish.
7. Share the app with users or groups and associate required security roles.
8. Test form/view availability and table privileges with target personas.

**Generative pages:** Use the current maker experience to describe the required page in natural language, inspect the generated result, then validate data bindings, accessibility, responsive behavior, security and maintainability. Generated output is a starting point, not proof of production readiness.

#### Security, Governance & Operations

- App sharing does not override Dataverse security.
- Form assignment can tailor UX, but must not be relied on to protect sensitive data.
- Include assets in solutions for ALM.
- Review dependencies before removing forms/views.
- Use role-appropriate dashboards and avoid exposing data through overly broad privileges.

#### Exam Gotchas ⚠️

- Publishing a form or app does not share it.
- A user can have table permission but no app access, or app access but insufficient table permission.
- A view filter is not authorization.
- Generated pages still require maker validation.
- Charts depend on data and view context; dashboards aggregate components but do not grant data access.

#### Scenario Patterns

**Scenario:** Sales and service users need different layouts over the same table.  
**Best choice:** Create role-appropriate main forms and assign form access by security role, while maintaining correct table/column security.

**Scenario:** The required application is strongly relational, needs standard grids/forms and rapid delivery.  
**Best choice:** Model-driven app rather than pixel-level canvas construction.

#### Quick Revision Summary

- Model-driven apps are metadata and Dataverse driven.
- Know form types, views, charts, dashboards and navigation composition.
- Separate app access, form access and data security.
- Treat generative output as editable, testable solution content.
- Build and transport app assets in a solution.

### 4.4 Create Canvas Apps

#### What You Need to Know

Official tasks include data-based creation; accessibility, performance, responsiveness and usability; process automation; reusable components, named formulas, user-defined functions and component libraries; variables/collections; error handling; testing with Monitor; and creating a Copilot Studio agent from a canvas app.

**State types**

| State | Scope/use |
|---|---|
| Global variable (`Set`) | App-wide mutable value |
| Context variable (`UpdateContext`) | Screen-scoped state |
| Collection (`Collect`, `ClearCollect`) | In-memory tabular data; useful for temporary/local manipulation |
| Named formula | Declarative, automatically recalculated reusable expression |
| User-defined function | Reusable formula behavior with defined parameters/return behavior where supported |
| Component/component library | Reusable UI/logic; library supports reuse across apps |

#### Mental Model & Decision Rules

- Prefer delegation-capable queries against large data sources. A formula can be logically correct but return incomplete results if nondelegable processing is limited to a client subset.
- Use responsive containers and relative sizing rather than fixed coordinates for multi-device experiences.
- Prefer named formulas for declarative reusable calculations; use variables only when mutable state is required.
- Use components for reuse within an app and component libraries for governed cross-app reuse.
- Call flows from apps for server-side/cross-service automation, but design clear input/output contracts and user feedback.
- Use an agent when the experience requires conversational reasoning or actions; do not replace straightforward forms/navigation with chat without benefit.

#### Implementation Examples

**Error-aware submit**

```powerfx
IfError(
    SubmitForm(frmRequest),
    Notify(
        "The request could not be saved. Review the fields and try again.",
        NotificationType.Error
    )
)
```

**Explicit patch pattern**

```powerfx
IfError(
    Patch(
        Requests,
        Defaults(Requests),
        {
            Title: txtTitle.Text,
            Priority: drpPriority.Selected
        }
    ),
    Notify("Save failed.", NotificationType.Error),
    Notify("Saved successfully.", NotificationType.Success)
)
```

**Call a flow**

```powerfx
Set(
    varResult,
    SubmitRequestFlow.Run(txtRequestId.Text)
)
```

The actual flow name, parameter types and returned fields depend on the flow contract.

**Test with Monitor**

1. Open Monitor from the app authoring/testing experience.
2. Start a monitoring session and reproduce the issue.
3. Inspect network calls, connector operations, formula events, timings, errors and warnings.
4. Identify delegation, repeated calls, payload or connector failures.
5. Change the app, rerun the scenario and compare.

#### Accessibility, Security, Governance & Operations

- Set meaningful accessible labels; support keyboard navigation, contrast, focus order and non-color cues.
- Do not expose secrets in formulas, variables or collections.
- Share the app and separately grant data-source/connection permissions where required.
- Validate delegation warnings and minimize repeated network calls.
- Use `Concurrent` only when operations are independent and parallel execution is safe.
- Use App Checker, Monitor and representative device tests.
- Handle failures and provide actionable feedback rather than silent errors.

#### Exam Gotchas ⚠️

- Collections are not a substitute for a durable data store.
- `Set` creates global state; `UpdateContext` is screen scoped.
- Hiding a control does not secure its data.
- Delegation warnings can indicate incomplete results, not just slow performance.
- A flow connection executes under its configured connection model; app sharing alone does not guarantee authorization.
- Microsoft changes the nondelegation row-limit configuration and connector support over time; verify current documentation rather than memorizing an unverified value from old material.

#### Scenario Patterns

**Scenario:** A formula queries a large remote list and users report missing rows.  
**Best choice:** Rewrite the query using delegable operations or move filtering to a delegable source/server-side design. Increasing a client row limit does not make a nondelegable formula complete for arbitrary data size.

**Scenario:** A standardized header and validation behavior must be reused across many apps.  
**Best choice:** A governed component library, not copied controls in each app.

#### Quick Revision Summary

- Know state scopes and reusable formula/component options.
- Delegation is correctness and scale, not merely performance.
- Build responsive and accessible experiences deliberately.
- Use `IfError`, user notifications, App Checker and Monitor.
- Share app and data access separately.
- Understand the app-to-flow and app-to-agent integration patterns.

## Domain 3: Build Business Application Logic and Automation (40–45%)

### 4.5 Create Cloud Flows

#### What You Need to Know

Official tasks: recommend triggers; evaluate connectors; approvals; actions; conditions/loops; testing/troubleshooting.

**Trigger types**

| Requirement | Trigger pattern |
|---|---|
| Respond to an event | Automated cloud flow |
| User explicitly starts work | Instant cloud flow |
| Run at time/interval | Scheduled cloud flow |
| Canvas app initiates automation | Power Apps trigger |
| Dataverse row change | Microsoft Dataverse trigger with change type, table and scope/filter configuration |

#### Mental Model & Decision Rules

- Choose the most specific event trigger and apply trigger conditions/filtering early to reduce unnecessary runs.
- Prefer standard connectors when they satisfy security and functionality. Premium/custom connectors can add licensing and governance requirements.
- Use conditions for branching, `Switch` for clear multi-value paths, and loops for collections.
- Avoid unnecessary nested loops; select/filter data before iteration where possible.
- Use child flows for reusable logic in solution-aware designs where supported.
- Design idempotency when retries or duplicate events could otherwise repeat side effects.

#### Implementation Examples

**Condition expression**

```text
@equals(triggerBody()?['statuscode'], 1)
```

**Null-safe access**

```text
coalesce(triggerBody()?['description'], 'No description supplied')
```

**Dataverse flow sequence**

1. Create the flow in a solution.
2. Select **When a row is added, modified or deleted**.
3. Configure change type, table and scope.
4. Add supported filtering/select-column configuration to reduce runs where appropriate.
5. Add actions with connection references.
6. Add conditions, `Apply to each`, error paths and meaningful names.
7. Save and test with representative data.
8. Review run history and action inputs/outputs, protecting sensitive data where necessary.

**Approval pattern**

1. Trigger on request submission.
2. Create/start and wait for approval using the required approval type.
3. Branch on outcome.
4. Update the source system and notify stakeholders.
5. Handle rejection, timeout/cancellation and failed actions according to the business requirement.

#### Security, Governance & Operations

- Use least-privileged service or user connections appropriate to ownership and support.
- Review connector tier and data-policy classification before design commitment.
- Put flows in solutions for ALM and use connection references/environment variables.
- Use run history, static results/test tooling where available, and resubmission carefully.
- Configure action retry/run-after behavior based on idempotency and failure semantics.
- Licensing depends on connectors, flow type, process ownership and tenant licensing. Verify with the current [Power Automate licensing guide](https://learn.microsoft.com/en-us/power-platform/admin/powerapps-flow-licensing-faq).

#### Exam Gotchas ⚠️

- Trigger conditions prevent unwanted runs; a condition as the first action still consumes a run.
- `Apply to each` may be added automatically when dynamic content is an array.
- A successful trigger does not mean every action succeeded; inspect run status and branches.
- Retrying a non-idempotent operation can create duplicates.
- Connection ownership and sharing affect continuity when makers leave.
- No single timeout, retention period or request quota applies to every flow/plan/connector. Consult current [Power Automate limits](https://learn.microsoft.com/en-us/power-automate/limits-and-config) and connector documentation.

#### Scenario Patterns

**Scenario:** A flow should run only when an approved flag becomes true.  
**Best choice:** Use narrow trigger configuration/trigger conditions rather than triggering for every update and immediately terminating.

**Scenario:** The same sequence is required by several solution flows.  
**Best choice:** Evaluate a solution-aware child flow to centralize reusable automation, assuming supported connector/connection requirements are met.

#### Quick Revision Summary

- Map event, manual and time requirements to the right trigger type.
- Filter at the trigger/source where possible.
- Understand connector capability, licensing and data policy.
- Know approval, branching, loop and expression patterns.
- Design retries and idempotency together.
- Troubleshoot through run history, inputs, outputs and error details.

### 4.6 Create Prompts and Models in AI Hub

#### What You Need to Know

Official tasks:

- Build prompts from templates or blank.
- Consume a prompt in apps and cloud flows.
- Add knowledge to a prompt.
- Customize prompt settings, including models.
- Add prompt inputs.
- Consume an AI model in apps and cloud flows.

**Terminology**

- **Prompt:** Reusable instruction configuration that can accept inputs and generate output.
- **Grounding/knowledge:** Approved business context supplied to improve relevance and factuality.
- **Input:** Runtime value inserted into the prompt.
- **Model setting:** Supported model/configuration choice exposed by the current AI Hub experience.
- **AI model:** Prebuilt or custom AI capability consumed by apps/flows, depending on current availability and licensing.

#### Mental Model & Decision Rules

- Use a **template** to accelerate a recognized scenario; use **blank** when requirements need custom instructions/inputs.
- Separate stable instructions from runtime inputs.
- Ground the prompt when answers must reflect approved organizational data.
- Use deterministic Power Fx/flow expressions for exact calculations and rules. Do not use generative AI where exact, repeatable logic is required.
- Treat model output as untrusted and potentially variable. Validate output and introduce human review for consequential actions.
- Select a model based on supported capability, quality, latency, cost, regional availability and governance. The blueprint does not prescribe one universal model.

#### Implementation Examples

**Prompt design structure**

```text
Role: You classify incoming service requests.
Task: Return one category and a short rationale.
Allowed categories: Access, Hardware, Software, Other.
Input: <RequestText>
Constraints: Use only the allowed categories. If evidence is insufficient, select Other.
Output: JSON with category and rationale.
```

**Cloud flow pattern**

1. Trigger on a new business record.
2. Retrieve only the required grounding data.
3. Run the configured prompt/model action.
4. Validate that required output fields exist.
5. Route low-confidence/invalid responses to human review.
6. Save approved output and operational metadata.

**Canvas app pattern**

1. Add the prompt/model capability as supported by the maker experience.
2. Pass sanitized, minimal input from the app.
3. Show a loading state and handle timeout/failure.
4. Present AI output as a suggestion unless automated use is explicitly safe and governed.

#### Security, Governance & Operations

- Minimize personal, confidential and regulated data sent to a model.
- Do not embed secrets in prompts.
- Restrict maker/user access and comply with data policies and environment governance.
- Test for prompt injection, irrelevant output, hallucination, unsafe content and data leakage.
- Log enough context for support without retaining unnecessary sensitive content.
- Monitor quality, latency, failures and consumption.
- AI Builder/AI capacity and licensing can change. Verify current tenant entitlements and [AI Builder licensing](https://learn.microsoft.com/en-us/ai-builder/administer-licensing) before implementation.

#### Exam Gotchas ⚠️

- Grounding reduces hallucination risk but does not guarantee truth.
- Temperature/model choice cannot convert probabilistic output into deterministic business logic.
- Prompt input is data, not trusted instruction; delimit and constrain it.
- An AI model in a flow and a Copilot Studio agent solve different problems.
- Availability, model names, regions, capacity and preview status change. The study guide does not provide fixed values, so none are invented here.

#### Scenario Patterns

**Scenario:** Categorize free-text requests but require a person to approve uncertain classifications.  
**Best choice:** AI Hub prompt/model in a flow, structured output validation, and a human approval path. This balances scale with responsible oversight.

**Scenario:** Calculate a contractual charge from fixed rates.  
**Best choice:** Formula/flow rule, not a generative prompt, because exact deterministic computation is required.

#### Quick Revision Summary

- Know prompt creation, inputs, knowledge, settings and consumption paths.
- Ground with approved data and validate output.
- Use deterministic logic for exact rules/calculations.
- Design for variable output, failures and human review.
- Review security, responsible AI, capacity and licensing.

### 4.7 Implement Business and Process Logic

#### What You Need to Know

Official tasks: business rules; business process flows; calculated, rollup and formula columns; and use-case evaluation.

| Capability | Best fit |
|---|---|
| Business rule | Declarative validation/defaulting/visibility or requirement logic within supported scope |
| Business process flow | Stage-based user guidance across a business process |
| Formula column | Power Fx-based derived value evaluated from row data within supported capabilities |
| Calculated column | Declarative calculated value using supported functions and related data behavior |
| Rollup column | Periodic/on-demand aggregate over related rows |
| Cloud flow | Asynchronous/cross-service/event-driven automation |
| Plug-in/custom code | Server-side logic requiring capabilities not met declaratively |

#### Mental Model & Decision Rules

- Put data integrity logic as close to the data layer as practical.
- Use a business rule for supported declarative validation or UI/data behavior.
- Use a business process flow to guide people through stages, not to replace system automation.
- Use a rollup for aggregates across related rows; do not expect instant transactional recalculation in every scenario.
- Use formula/calculated columns for derived values, considering supported data types/functions and evaluation behavior.
- Use cloud flows for integrations, approvals, notifications and asynchronous orchestration.

#### Implementation Example

**Business rule**

1. Open the table inside a solution.
2. Create a business rule.
3. Add condition: when Priority is High.
4. Add actions, such as make Escalation Reason required and show a business recommendation/message.
5. Validate, save and activate.
6. Test in every intended client/scope.

**Business process flow**

1. Create it in a solution for the required table(s).
2. Define stages, data steps and required fields.
3. Configure branching only when the process requires it.
4. Validate, activate and assign appropriate security-role access.
5. Test stage movement, table permissions and app inclusion.

#### Security, Governance & Operations

- Business process flow access and underlying table privileges both matter.
- Do not use client-only behavior as the sole enforcement mechanism for critical integrity.
- Document where logic runs to prevent duplicate or conflicting rules across app, table, flow and code layers.
- Monitor flow-based automation separately from column/business-rule behavior.
- Evaluate performance and recalculation timing before using rollups for time-critical decisions.

#### Exam Gotchas ⚠️

- A business process flow guides the user; it is not the same as a cloud-flow workflow.
- A rollup is not guaranteed to update instantly after every child-row change.
- Formula/calculated/rollup capabilities and supported functions differ.
- A UI visibility rule is not field-level security.
- Multiple logic layers can produce loops or contradictory updates.

#### Scenario Patterns

**Scenario:** Agents must follow Qualification, Investigation and Resolution stages.  
**Best choice:** Business process flow for guided stages, with cloud flows only for needed automation such as notifications.

**Scenario:** Show the total value of related open order rows.  
**Best choice:** Evaluate a rollup column if its supported filters and recalculation behavior meet the requirement. Use another approach if near-real-time transactional consistency is mandatory.

#### Quick Revision Summary

- Match business rule, BPF, column logic and flow to the execution need.
- BPF = guided stages; cloud flow = automation.
- Rollup = related-row aggregation with non-immediate behavior.
- Formula/calculated capabilities are not interchangeable.
- Avoid duplicate logic across layers.

## 5. High-Yield Facts Reference

### Verified exam facts

| Fact | Value/status | Exam implication |
|---|---|---|
| Passing score | 700 or greater | Scaled score; it is not stated as “70%” |
| Assessment time | 120 minutes | Plan time for review and possible interactive items |
| Domain 1 | 25–30% | Do not neglect architecture/Dataverse |
| Domain 2 | 25–30% | Balanced model-driven and canvas preparation |
| Domain 3 | 40–45% | Highest revision priority |
| Practice Assessment | Certification page says not currently available at research date | Use sandbox and original practice questions |
| GA vs Preview | Most questions cover GA; commonly used Preview features may appear | Check current feature status |

### Limits, quotas, retention, timeouts and licensing

| Area | Verified exam-safe statement | Where to verify current values |
|---|---|---|
| Power Automate limits | Limits vary by request type, profile, connector and configuration; no single blueprint value | [Power Automate limits](https://learn.microsoft.com/en-us/power-automate/limits-and-config) |
| Connector limits | Connector-specific throttling/operation limits apply | Individual connector reference pages |
| Dataverse API protection | Service-protection limits exist and can return throttling responses | [Dataverse API limits](https://learn.microsoft.com/en-us/power-apps/developer/data-platform/api-limits) |
| Canvas delegation | Support differs by data source and function | [Delegation overview](https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/delegation-overview) |
| Flow run retention | Depends on current platform/plan/policy; not specified in AB-410 blueprint | Current Power Automate limits/admin documentation |
| Flow timeout | Depends on flow/action/connector pattern; not specified in blueprint | Current limits and connector docs |
| Dataverse capacity | Tenant capacity and entitlement depend on licensing | Power Platform admin/licensing docs |
| AI capacity | Consumption and entitlement vary by capability and licensing | AI Builder licensing/admin docs |
| Premium connectors | May require premium licensing | Current Power Apps/Power Automate licensing guides |
| Power Pages | Licensing is capacity/authentication model dependent | Current Power Pages licensing guide |

> **Exam-safe rule:** Do not memorize an old blog’s number. If the official study guide does not call out a numeric limit, understand the design consequence: delegation, throttling, capacity, timeout, retention, licensing and regional availability must be checked for the selected service.

### Performance considerations

| Area | High-yield design action |
|---|---|
| Canvas app | Use delegable queries, minimize calls/payload, cache only when justified, avoid unnecessary control dependencies |
| Model-driven app | Keep forms/views purposeful; avoid excessive subgrids, scripts and synchronous processing |
| Dataverse | Select columns, filter early, design relationships/index-friendly queries, respect API protection |
| Cloud flows | Filter triggers, avoid nested loops, reduce connector calls, use concurrency only when safe |
| AI | Minimize prompt/context size, select fit-for-purpose model, handle latency and capacity |

## 6. Service Selection Cheat Sheet

| IF the requirement is... | AND the constraint is... | USE... |
|---|---|---|
| Build a highly tailored task UI | Detailed control over layout is essential | Canvas app |
| Build an internal relational process app | Rapid metadata-driven forms/views are preferred | Model-driven app |
| Serve external users through a website | Dataverse-backed external experience is required | Power Pages |
| React to an event across services | Low-code orchestration is suitable | Automated cloud flow |
| Run on a timetable | No user action should be necessary | Scheduled cloud flow |
| Start automation from an app/button | User initiates the action | Instant flow/Power Apps trigger |
| Provide multi-turn conversation and actions | Knowledge and orchestration are required | Copilot Studio agent |
| Generate/summarize/classify text in an app or flow | Reusable generative instruction with inputs is sufficient | AI Hub prompt |
| Apply exact business calculation | Output must be deterministic | Power Fx, formula/calculated logic or flow expression |
| Aggregate child-row values | Delayed/periodic aggregate semantics are acceptable | Rollup column |
| Guide users through stages | Human progression is central | Business process flow |
| Enforce supported declarative validation/defaulting | No custom code is needed | Business rule |
| Reuse UI within one app | Reuse scope is local | Component |
| Reuse governed UI across apps | Central reuse/versioning is required | Component library |
| Promote configuration between environments | Values/connections differ by environment | Solution + environment variables + connection references |
| Secure rows by owner/business unit | Persona access varies by record ownership | User/team-owned Dataverse table + security roles |

## 7. Practice Questions

### Question 1: ALM configuration

A solution uses a SharePoint site URL and a SQL connection that differ between development, test and production. What should you recommend?

A. Hard-code target values before each export  
B. Environment variables and connection references in a solution  
C. Separate canvas apps with copied formulas  
D. A filtered Dataverse view

**Correct answer: B**

**Why:** Environment variables externalize environment-specific values, while connection references bind solution-aware components to target connections.  
**Why not A:** Manual hard-coding is error-prone and undermines repeatable ALM.  
**Why not C:** Copies create drift and are not an ALM design.  
**Why not D:** Views do not manage configuration or connections.

### Question 2: Dataverse security

Users may open a model-driven app but receive access errors on Account rows. What is the most likely missing configuration?

A. A canvas collection  
B. Dataverse security-role privileges  
C. A public view  
D. A chart

**Correct answer: B**

**Why:** App access and Dataverse data permissions are separate.  
**Why not C:** A view cannot grant row/table authorization.  
**Why not A/D:** Neither provides Dataverse privileges.

### Question 3: Relationship design

Each Inspection belongs to one Asset, and each Asset can have many Inspections. What should you create?

A. Many-to-many relationship  
B. Text column containing asset name  
C. Lookup on Inspection to Asset  
D. Choice column on Asset

**Correct answer: C**

**Why:** The lookup creates a many-to-one relationship from Inspection to Asset and one-to-many from Asset to Inspection.  
**Why not B:** Duplicated text loses referential integrity.  
**Why not A/D:** They do not represent the stated cardinality.

### Question 4: Delegation

A canvas app filters 100,000 records. Users see incomplete results and the formula has a delegation warning. What is the best response?

A. Copy all rows into a collection at startup  
B. Replace the query with delegable operations/source-side filtering  
C. Hide the warning icon  
D. Add another screen

**Correct answer: B**

**Why:** Delegable processing lets the source evaluate the query across the full dataset.  
**Why not A:** Loading a huge collection is not a correct scalable fix.  
**Why not C/D:** They do not address data completeness.

### Question 5: Reuse

A company needs a consistent header and navigation component across 20 canvas apps. What should it use?

A. Copy/paste controls  
B. Global variables only  
C. Component library  
D. Business process flow

**Correct answer: C**

**Why:** A component library supports reuse across apps.  
**Why not A:** Copies drift.  
**Why not B:** Variables do not package UI.  
**Why not D:** BPFs guide process stages in model-driven scenarios.

### Question 6: Trigger efficiency

A Dataverse flow should run only when a row is modified and `ReadyForReview` is true. How should unnecessary runs be reduced?

A. Trigger on every change, then add a final condition  
B. Use specific trigger configuration and a trigger condition/filter where supported  
C. Add a ten-minute delay  
D. Create a dashboard

**Correct answer: B**

**Why:** Filtering at the trigger prevents irrelevant runs.  
**Why not A:** The flow still starts and consumes processing.  
**Why not C/D:** Neither selects the correct events.

### Question 7: Approval

An expense request needs one manager decision, source-row update and requester notification. Which core pattern is best?

A. Scheduled flow with no approval action  
B. Automated flow with start-and-wait approval, outcome condition and update/notify actions  
C. Rollup column  
D. Canvas context variable

**Correct answer: B**

**Why:** It models event, decision, branching and follow-up actions.  
**Why not A:** It lacks the decision mechanism.  
**Why not C/D:** They cannot orchestrate the approval.

### Question 8: Deterministic calculation

A regulated fee must always equal quantity multiplied by an approved fixed rate. What should the maker use?

A. Generative prompt  
B. Copilot Studio agent  
C. Deterministic formula/business logic  
D. Row summary

**Correct answer: C**

**Why:** Exact calculations require deterministic logic.  
**Why not A/B/D:** Generative output is probabilistic and inappropriate for an exact contractual fee.

### Question 9: Grounded generation

A flow must summarize a case using approved Dataverse case notes. What design best reduces unsupported content?

A. Prompt with no context  
B. Ground the prompt with the required Dataverse data, constrain output and validate it  
C. Increase randomness  
D. Replace case security with a public view

**Correct answer: B**

**Why:** Grounding, constraints and validation improve relevance and governance.  
**Why not A/C:** They increase unsupported-output risk.  
**Why not D:** Views are not security controls.

### Question 10: Process guidance

Service agents must complete Qualification, Diagnosis and Resolution stages and see required steps in each stage. What is the best primary capability?

A. Business process flow  
B. Scheduled cloud flow  
C. Rollup column  
D. Component library

**Correct answer: A**

**Why:** A BPF provides stage-based process guidance.  
**Why not B:** A cloud flow automates work but does not provide the same guided stage UI.  
**Why not C/D:** Neither models process stages.

### Question 11: Aggregation

A maker needs the total value of related open line items and can accept platform-defined recalculation timing. Which capability is most appropriate?

A. Rollup column  
B. Main form  
C. Security role  
D. Copilot agent

**Correct answer: A**

**Why:** Rollups aggregate related rows using supported filters.  
**Why not B/C/D:** They present, secure or converse; they do not provide the aggregate.

### Question 12: Troubleshooting

A canvas app intermittently fails while calling a connector. The maker needs detailed event and network timing information. What should be used?

A. Monitor  
B. Public view  
C. Business process flow  
D. Choice column

**Correct answer: A**

**Why:** Monitor exposes runtime events, connector calls, timings, warnings and errors.  
**Why not B/C/D:** None provides runtime diagnostics.

### Question 13: Agent vs prompt

Users need a multi-turn assistant that answers from knowledge and invokes actions. What is the best fit?

A. A single formula column  
B. Copilot Studio agent with appropriate knowledge/actions  
C. Rollup column  
D. Static chart

**Correct answer: B**

**Why:** The requirement is conversational and action-oriented.  
**Why not A/C/D:** These are neither conversational nor orchestration capabilities.

### Question 14: Form security trap

A field is removed from a form so users cannot see it. Is the data secured?

A. Yes, because the control is hidden  
B. Yes, if the form is published  
C. No; use appropriate table/row privileges and field security where eligible  
D. No; create a chart

**Correct answer: C**

**Why:** UI hiding is not a security boundary.  
**Why not A/B/D:** None establishes data authorization.

### Question 15: Extensibility

A requirement can be met by a certified connector and a cloud flow. The team proposes custom Azure code instead. What is the best recommendation?

A. Use custom code because it is always more scalable  
B. Prefer supported low-code capability unless nonfunctional requirements prove it insufficient  
C. Store credentials in Power Fx  
D. Use the default environment for all stages

**Correct answer: B**

**Why:** Start with standard/low-code capability to reduce custom maintenance while validating security, licensing and performance.  
**Why not A:** Custom code is not automatically superior.  
**Why not C:** Secrets must not be embedded.  
**Why not D:** It is not a controlled ALM strategy.

## 8. Final Revision Section

### 🔥 Top Must-Know Facts

1. The three weights are **25–30%, 25–30%, and 40–45%**.
2. Domain 3, automation and business logic, is the largest.
3. App sharing, form/view access and Dataverse data permissions are different controls.
4. Views and hidden controls are not security boundaries.
5. Use solutions, environment variables and connection references for ALM.
6. Build unmanaged in development and normally deploy managed downstream.
7. Canvas delegation affects completeness as well as performance.
8. Use Monitor for canvas runtime diagnostics and run history for cloud flows.
9. Trigger filtering is better than starting a flow and terminating immediately.
10. Design flow retries with idempotency.
11. Agent = multi-turn conversation/orchestration; prompt = reusable generation; flow = deterministic orchestration.
12. Grounding reduces, but does not eliminate, hallucination.
13. Use deterministic logic for exact calculations and policy rules.
14. BPF guides human stages; cloud flow automates actions.
15. Rollups aggregate related rows but should not be assumed to recalculate instantly.
16. Know variables, collections, named formulas, user-defined functions, components and component libraries.
17. Know tables, columns, relationships, ownership, roles, forms and views.
18. Prompt columns and row summaries are explicit blueprint objectives even though course coverage is limited.
19. AI Hub coverage extends well beyond the single grounded-prompts course module.
20. Microsoft may assess commonly used Preview features, so inspect current status labels.

### ⚠️ Common Traps

- Treating 700 as exactly 70 percent rather than a scaled passing score.
- Assuming course completion covers every blueprint bullet.
- Confusing certification title with exam title.
- Confusing app access with data access.
- Using view filters or hidden controls as security.
- Duplicating related data in text instead of using relationships.
- Ignoring Append versus Append To.
- Using collections to bypass delegation at scale.
- Choosing an agent for a simple deterministic automation.
- Choosing generative AI for an exact calculation.
- Assuming grounding guarantees factual output.
- Adding a condition after a trigger when a trigger condition could prevent the run.
- Retrying non-idempotent actions without duplicate protection.
- Expecting rollups to be instant.
- Hard-coding URLs and connections across environments.
- Memorizing old product limits, licensing or preview status.

### ✅ Rapid Revision Checklist

- [ ] I can state all three domains and weights.
- [ ] I can map a requirement to canvas, model-driven, Power Pages, flow, prompt or agent.
- [ ] I can explain environment type, solution type and ALM strategy separately.
- [ ] I can explain environment variables and connection references.
- [ ] I can model one-to-many and many-to-many relationships.
- [ ] I can explain ownership, roles, access depth, Append and Append To.
- [ ] I can configure forms, views, charts, dashboards and app access.
- [ ] I can explain generative pages and required post-generation validation.
- [ ] I can explain global/context variables, collections and named formulas.
- [ ] I can explain delegation and identify the correct remediation.
- [ ] I can use `IfError`, App Checker and Monitor conceptually.
- [ ] I can select automated, instant and scheduled triggers.
- [ ] I can design approvals, conditions, loops and failure paths.
- [ ] I can troubleshoot from flow run history.
- [ ] I can distinguish prompt inputs, knowledge and model settings.
- [ ] I can explain safe app/flow consumption of AI output.
- [ ] I can choose among business rules, BPFs, formula/calculated/rollup columns and flows.
- [ ] I reviewed current licensing, limits and Preview labels immediately before the exam.
- [ ] I practised the official exam sandbox.

### 🎯 Exam-Day Strategy

1. **Read the final sentence first.** Identify exactly what must be recommended, configured or troubleshot.
2. **Extract constraints.** Look for external/internal users, relational data, real-time versus scheduled, deterministic versus generative, security boundary, licensing, ALM and human review.
3. **Eliminate category errors.** A view is not security, a BPF is not automation, and an agent is not a formula.
4. **Prefer native supported capability.** Select the least complex option that fully satisfies functional and nonfunctional requirements.
5. **Respect explicit qualifiers.** “Only,” “minimum administrative effort,” “without code,” “real time,” and “across environments” usually change the answer.
6. **For case studies, build a requirement matrix.** Record actor, data, trigger, experience, security and lifecycle before answering.
7. **For multi-select, evaluate each option independently.** Do not stop after finding one plausible choice.
8. **Flag uncertain numeric questions.** Revisit after conceptual questions; do not let one obscure limit consume time.
9. **Reserve review time.** Recheck questions involving negatives, multiple requirements and Preview/GA wording.
10. **Use Microsoft Learn access according to the current exam policy/interface.** Do not assume every website or portal is available during the exam.

## 9. REACT Scenario-Question Framework

Use **REACT** to turn long scenarios into a defensible architecture decision.

1. **R, Requirements:** Identify personas, channel, data, event, AI outcome, scale, latency, compliance and budget.
2. **E, Exclusions:** Mark restrictions such as no code, external users, offline support, least privilege, no premium connectors or GA-only production use.
3. **A, Architecture:** Select the smallest complete combination of experience, data, automation, intelligence and lifecycle components.
4. **C, Constraints:** Test licensing, environment, data policy, connector, delegation, identity, capacity, regional availability and ALM constraints.
5. **T, Test the options:** Eliminate answers that satisfy the visible UI but violate security, data integrity, supportability or lifecycle requirements.

**Decision order:** Security and compliance → functional fit → supportability and ALM → performance → cost → maker convenience.

### Language clues

| Wording in a scenario | Likely direction |
|---|---|
| Immediately after a Dataverse row changes | Automated cloud flow with a narrow Dataverse trigger |
| At a fixed time every weekday | Scheduled cloud flow |
| User selects a button | Instant flow, app-triggered flow or direct Power Fx, based on orchestration need |
| Guide users through stages | Business process flow |
| Validate/default data consistently | Business rule or data-layer logic |
| Aggregate child records | Rollup column if its recalculation characteristics are acceptable |
| Pixel-level task experience | Canvas app |
| Data-dense process experience | Model-driven app |
| External website | Power Pages with identity, web roles and table permissions |
| Multi-turn conversation plus actions | Copilot Studio agent |
| Exact calculation | Deterministic formula or process logic, not generative AI |

## 10. Environment, Security and ALM Quick References

### Environment selection

| Environment type | Best fit | Main caution |
|---|---|---|
| Default | Governed personal productivity and limited experimentation | Do not make it the planned home of a governed enterprise production solution |
| Developer | Individual maker/developer work | Not shared production |
| Sandbox | Development, test, training, reset/copy scenarios | Protect production data and credentials |
| Production | Live business workload | Apply controlled access, managed deployment, monitoring and change control |
| Trial | Time-limited evaluation | Not a durable production architecture |
| Dataverse for Teams | Teams-scoped solutions | Account for capability, capacity and lifecycle differences |

### Dataverse security matrix

| Control | Secures/controls | Does not replace |
|---|---|---|
| Environment role | Environment administration and maker capabilities | Dataverse row/table privileges |
| Security role | Table privileges and applicable access depth | Licensing, app sharing or column security |
| Team membership | Group ownership and cumulative role access | Deliberate least-privilege design |
| Row ownership/sharing | Access to specific rows according to model | Table privileges |
| Column security profile | Eligible sensitive column values | Table and row access |
| App sharing | Ability to launch/use the app | Underlying data privileges |
| Form role assignment | Form availability by persona | Data authorization |
| View filter | Record presentation | Row security |
| Power Pages table permission | Site-user access to Dataverse rows | Web role assignment and identity configuration |

### ALM control map

| Need | Use |
|---|---|
| Package and transport assets | Solution |
| Environment-specific configuration | Environment variable |
| Bind solution-aware components to target connections | Connection reference |
| Editable source assets | Unmanaged solution in development |
| Controlled downstream deployment | Managed solution |
| Repeatable promotion | Power Platform pipelines or governed CI/CD |
| Quality checking | Solution checker, app checker, tests and deployment validation |
| Secrets | Approved identity/secrets mechanism, never formulas or source control |

## 11. Power Fx Quick Reference

### State and reuse

- `Set(name, value)`: creates or updates app-wide mutable state.
- `UpdateContext({name: value})`: creates or updates screen-scoped state.
- `Navigate(Screen, Transition, {parameter: value})`: navigates and can pass target-screen context.
- `Collect` and `ClearCollect`: manage in-memory tabular data. Collections are not durable databases.
- Named formulas: declarative, reusable and automatically recalculated values.
- User-defined functions: parameterized reusable logic where supported.
- Components: reuse inside an app. Component libraries: governed reuse across apps.

### Safe formula patterns

```powerfx
If(
    IsBlank(Trim(txtTitle.Text)),
    Notify("Enter a title.", NotificationType.Error),
    IfError(
        Patch(
            Requests,
            Defaults(Requests),
            { Title: Trim(txtTitle.Text) }
        ),
        Notify("The request could not be saved.", NotificationType.Error),
        Notify("Request saved.", NotificationType.Success)
    )
)
```

```powerfx
Filter(
    Requests,
    Status = 'Request Status'.Active &&
    StartsWith(Title, txtSearch.Text)
)
```

Delegation depends on the connector, operation and column type. Always inspect delegation warnings against the actual data source.

### Performance review

- Filter and select only required data.
- Avoid repeated lookups inside galleries.
- Do not call a flow once per gallery row when batching is possible.
- Use responsive containers and relative sizing.
- Use `Concurrent` only for independent operations and account for connector throttling.
- Use App Checker before publishing and Monitor for runtime diagnosis.

## 12. Business Logic Decision Tree

```text
Is the requirement conversational and multi-turn?
  Yes -> Copilot Studio agent, with governed actions where needed.
  No  -> Continue.

Is the output probabilistic generation, classification or summarization?
  Yes -> AI Hub prompt/model, grounded and validated.
  No  -> Continue.

Is it stage-based guidance for a human process?
  Yes -> Business process flow.
  No  -> Continue.

Is it a supported declarative validation/default/field behavior?
  Yes -> Business rule.
  No  -> Continue.

Is it a derived current-row value?
  Yes -> Formula or calculated column, based on supported behavior.
  No  -> Continue.

Is it an aggregate over related rows with acceptable recalculation delay?
  Yes -> Rollup column.
  No  -> Continue.

Is it event-driven, scheduled, approval-based or cross-service?
  Yes -> Cloud flow.
  No  -> Continue.

Does it require immediate complex server-side transaction behavior?
  Yes -> Evaluate plug-in/custom server logic.
```

## 13. Prompt Engineering and Copilot Studio Cheat Sheets

### Prompt contract

1. Define the business task and success criteria.
2. Separate stable instructions from runtime inputs.
3. Supply only approved, minimal grounding.
4. State allowed evidence, constraints and missing-evidence behavior.
5. Request a defined output structure when automation consumes the result.
6. Test normal, empty, ambiguous, adversarial, multilingual and oversized input.
7. Validate schema, content and authorization before downstream use.
8. Monitor quality, latency, failures, human overrides and consumption.

```text
Role: Classify incoming service requests.
Task: Select exactly one approved category and give a short rationale.
Allowed categories: Access, Hardware, Software, Other.
Evidence: Use only the supplied request text and approved knowledge.
Missing evidence: Select Other and explain what is missing.
Output: JSON containing category and rationale.
Input: <RequestText>
```

### Copilot Studio selection and delivery

- Use an agent for multi-turn conversation, knowledge grounding and action orchestration.
- Define instructions, knowledge, topics/tools/actions, authentication and channels.
- Use least-privileged actions and do not let the agent bypass the caller's authorization.
- Keep high-impact writes deterministic, validate inputs and request confirmation/human review where appropriate.
- Test prompt injection, unauthorized knowledge access, ambiguous intent, tool failure and escalation.
- Publish through governed environments and solutions, then monitor analytics and action failures.

### AI Hub versus agent

| Requirement | Choose |
|---|---|
| A reusable generate/summarize/classify operation in an app or flow | AI Hub prompt |
| Document extraction, prediction or another supported AI model task | AI model |
| Multi-turn conversation using knowledge and actions | Copilot Studio agent |
| Exact rule/calculation/authorization | Deterministic logic |

## 14. ALM Deployment Checklist

### Before build

- [ ] Correct development environment selected.
- [ ] Publisher, prefix and solution naming agreed.
- [ ] Ownership, environments and release path documented.
- [ ] Data classification, identity and data-policy constraints reviewed.

### During build

- [ ] Components created or added inside the solution.
- [ ] Environment-specific values moved to environment variables.
- [ ] Solution-aware connectors use connection references.
- [ ] No secrets, fixed tenant IDs or production URLs embedded in formulas/scripts.
- [ ] Apps, flows, tables, prompts, agents and dependencies included.
- [ ] Security roles, sharing steps and deployment identities documented.
- [ ] Solution checker, App Checker and relevant tests completed.

### Before promotion

- [ ] Unmanaged source retained in development.
- [ ] Managed package prepared for controlled downstream environments.
- [ ] Target connection owners and permissions are ready.
- [ ] Environment-variable deployment values reviewed.
- [ ] Data migration/reference-data plan validated.
- [ ] Rollback/forward-fix and support plan agreed.

### After deployment

- [ ] Connection references bound and flows enabled.
- [ ] Apps, forms, views, dashboards, prompts and agents published.
- [ ] Users/groups assigned app access and correct data roles.
- [ ] Least-privileged persona tests passed.
- [ ] Flow runs, Monitor traces, agent actions and AI outputs validated.
- [ ] Monitoring, capacity, cost and service health ownership confirmed.

## 15. Seven-Day Revision Plan

| Day | Focus | Hands-on outcome | Self-check |
|---:|---|---|---|
| 1 | Blueprint, architecture, environments and ALM | Design Dev/Test/Prod promotion with variables and references | Explain each architecture choice in 60 seconds |
| 2 | Dataverse | Build tables, relationship types, form, views, security, formula and rollup | Test as two personas |
| 3 | Model-driven apps | Compose app, role-specific forms/views, chart and dashboard | Diagnose three access failures |
| 4 | Canvas apps | Responsive app, component library, named formulas, errors and Monitor | Find delegation and performance issues |
| 5 | Cloud flows | Event, scheduled and approval flows with trigger conditions/scopes | Trace success, failure, timeout and throttling paths |
| 6 | AI Hub and agents | Grounded prompt, structured output, app/flow use and safe agent action | Run an adversarial test set |
| 7 | Business logic and mock review | Business rule/BPF/formula/rollup lab plus practice set | Explain every wrong answer by violated constraint |

**Daily cadence:** 60 minutes concepts, 90 minutes lab, 30 minutes scenario questions, 20 minutes error log and 10 minutes closed-book recall.

## 16. Official Skills Coverage Matrix

| Domain | Objective group | Official bullets covered | Guide section | Status |
|---|---|---:|---|---|
| Foundation | Design Microsoft Power Platform solutions using AI-enabled tools | 5 | 4.1, 9, 10, 14 | Complete |
| Foundation | Build data models | 10 | 4.2, 10 | Complete |
| Intelligent applications | Create model-driven apps | 7 | 4.3 | Complete |
| Intelligent applications | Create canvas apps | 8 | 4.4, 11 | Complete |
| Logic and automation | Create cloud flows | 6 | 4.5 | Complete |
| Logic and automation | Create prompts and models in AI Hub | 8 | 4.6, 13 | Complete |
| Logic and automation | Implement business and process logic | 4 | 4.7, 12 | Complete |
| **Total** | **All objective groups** | **48** | **Mapped throughout** | **Complete** |

> The current study guide contains 48 bullet-level tasks when counted directly under the seven objective groups. Some secondary guides report 49 by splitting a combined bullet. This guide preserves every official bullet without altering the blueprint wording.

## 17. Extended 100-Question Practice Bank

The 15 fully explained questions in Section 7 are followed by 85 rapid scenario drills below, creating a total bank of 100 original questions. Use the rapid drills for recall, then explain why the rejected options would fail.

### Question 16

**Scenario:** A maker needs an editable source package in development.

**Answer:** Use an unmanaged solution.

### Question 17

**Scenario:** Production components must be protected from direct maker edits.

**Answer:** Deploy a managed solution through controlled ALM.

### Question 18

**Scenario:** A target API URL changes by environment.

**Answer:** Use an environment variable.

### Question 19

**Scenario:** A solution-aware flow uses a different connection in test.

**Answer:** Use a connection reference bound to the target connection.

### Question 20

**Scenario:** A team wants production in the default environment.

**Answer:** Reject as the planned governed architecture; use a controlled production environment.

### Question 21

**Scenario:** One developer needs an isolated personal build environment.

**Answer:** Use a developer environment.

### Question 22

**Scenario:** A temporary reset/copy test environment is required.

**Answer:** Use a sandbox environment.

### Question 23

**Scenario:** A relationship needs start date and allocation percentage.

**Answer:** Use an explicit intersection table with two lookups.

### Question 24

**Scenario:** One customer has many orders.

**Answer:** Place a customer lookup on the Order child table.

### Question 25

**Scenario:** Sensitive salary data is hidden on the form but still readable by API.

**Answer:** Use column security plus appropriate table/row privileges.

### Question 26

**Scenario:** Users should read only owned records.

**Answer:** Use user/team ownership with user-level role depth, subject to complete role design.

### Question 27

**Scenario:** A reference table should be broadly shared without per-row ownership.

**Answer:** Evaluate an organization-owned table.

### Question 28

**Scenario:** Integration needs upsert by a stable business identifier.

**Answer:** Evaluate an alternate key.

### Question 29

**Scenario:** A finite status set must be consistent across tables.

**Answer:** Use an appropriate reusable choice.

### Question 30

**Scenario:** Deleting a parent must not unexpectedly remove children.

**Answer:** Review and configure relationship cascade behavior.

### Question 31

**Scenario:** A user can launch an app but cannot read rows.

**Answer:** Fix Dataverse privileges/access depth, not app navigation.

### Question 32

**Scenario:** A role needs a different main form.

**Answer:** Assign form access/order by security role.

### Question 33

**Scenario:** Managers need an operational visual over accessible records.

**Answer:** Use model-driven chart/dashboard if its operational analytics are sufficient.

### Question 34

**Scenario:** Rich semantic analytics are required.

**Answer:** Evaluate Power BI rather than forcing model-driven charts.

### Question 35

**Scenario:** A natural-language generated page is produced.

**Answer:** Review security, bindings, accessibility, responsiveness and dependencies before release.

### Question 36

**Scenario:** A canvas app must work on phone and desktop.

**Answer:** Use responsive containers and relative sizing.

### Question 37

**Scenario:** The same header is needed within one canvas app.

**Answer:** Use a component.

### Question 38

**Scenario:** The same header is centrally maintained across apps.

**Answer:** Use a component library.

### Question 39

**Scenario:** A value is derived and should recalculate declaratively.

**Answer:** Prefer a named formula over unnecessary mutable state.

### Question 40

**Scenario:** A small value must be shared across screens.

**Answer:** Use Set for app-wide state if mutable state is justified.

### Question 41

**Scenario:** A dialog-open flag is required only on one screen.

**Answer:** Use UpdateContext.

### Question 42

**Scenario:** The app needs a temporary tabular working set.

**Answer:** Use a collection, then persist final data to a durable source.

### Question 43

**Scenario:** A search over a large source shows a delegation warning.

**Answer:** Rewrite with delegable operations or server-side search.

### Question 44

**Scenario:** An app calls a connector repeatedly inside a gallery.

**Answer:** Reduce repeated calls through query redesign, precomputation or appropriate caching.

### Question 45

**Scenario:** Independent connector calls can run in parallel.

**Answer:** Consider Concurrent, accounting for throttling and dependencies.

### Question 46

**Scenario:** A save can fail and users need feedback.

**Answer:** Use IfError/Errors and Notify with actionable messaging.

### Question 47

**Scenario:** The exact runtime connector call must be inspected.

**Answer:** Use Power Apps Monitor.

### Question 48

**Scenario:** Static authoring issues need review.

**Answer:** Use App Checker.

### Question 49

**Scenario:** A canvas app starts a multi-system approval process.

**Answer:** Call a governed cloud flow with minimal typed inputs.

### Question 50

**Scenario:** A flow should react to a Dataverse create event.

**Answer:** Use an automated cloud flow with the Dataverse row trigger.

### Question 51

**Scenario:** A process starts from a user button.

**Answer:** Use an instant/app-triggered flow when server orchestration is needed.

### Question 52

**Scenario:** A reminder runs every Monday.

**Answer:** Use a scheduled cloud flow.

### Question 53

**Scenario:** A flow starts for irrelevant updates.

**Answer:** Narrow trigger configuration and use trigger conditions/filtering.

### Question 54

**Scenario:** A flow updates its own triggering row and loops.

**Answer:** Restrict changed columns/conditions and add an origin/state guard.

### Question 55

**Scenario:** An action receives an array.

**Answer:** Use Apply to each when iteration is required.

### Question 56

**Scenario:** Processing repeats until a condition or limit.

**Answer:** Use Do until with safe limits and failure handling.

### Question 57

**Scenario:** There are several discrete status branches.

**Answer:** Use Switch when clearer than nested conditions.

### Question 58

**Scenario:** Several flows need the same reusable sequence.

**Answer:** Evaluate a solution-aware child flow.

### Question 59

**Scenario:** A create action is retried and produces duplicates.

**Answer:** Add idempotency/duplicate protection before retrying.

### Question 60

**Scenario:** Order-dependent updates are processed concurrently.

**Answer:** Disable or bound concurrency to preserve required ordering.

### Question 61

**Scenario:** A target API throttles under load.

**Answer:** Batch/filter, bound concurrency and honor retry/backoff.

### Question 62

**Scenario:** A support engineer needs action inputs and outputs.

**Answer:** Inspect flow run history, protecting sensitive data.

### Question 63

**Scenario:** Sensitive values appear in run history.

**Answer:** Use secure inputs/outputs where appropriate and maintain broader access controls.

### Question 64

**Scenario:** The sole flow owner is leaving.

**Answer:** Move to governed ownership/service identity strategy and validate connections.

### Question 65

**Scenario:** An approval requires all approvers.

**Answer:** Choose the approval type requiring everyone and handle rejection/timeout.

### Question 66

**Scenario:** The first valid approver response is enough.

**Answer:** Choose first-to-respond approval.

### Question 67

**Scenario:** The requester must not self-approve a high-risk request.

**Answer:** Enforce approver identity and separation-of-duties logic.

### Question 68

**Scenario:** A prompt performs an exact financial calculation.

**Answer:** Replace it with deterministic formula/process logic.

### Question 69

**Scenario:** A prompt summarizes approved case notes.

**Answer:** Ground it with minimal authorized notes and constrain the output.

### Question 70

**Scenario:** A prompt invents missing details.

**Answer:** Require missing-evidence behavior and validate the result.

### Question 71

**Scenario:** Downstream automation expects fields.

**Answer:** Request structured output and validate the schema/content.

### Question 72

**Scenario:** Untrusted text may contain instructions.

**Answer:** Separate privileged instructions from inputs, minimize tools and test prompt injection.

### Question 73

**Scenario:** Restricted notes must never reach users.

**Answer:** Enforce source authorization and least-privileged execution; prompt wording is not security.

### Question 74

**Scenario:** A generated classification controls a consequential decision.

**Answer:** Use deterministic eligibility controls and human review as appropriate.

### Question 75

**Scenario:** Users need a multi-turn assistant with actions.

**Answer:** Use a Copilot Studio agent with governed knowledge/actions.

### Question 76

**Scenario:** An app needs a single reusable summarization call.

**Answer:** Use an AI Hub prompt rather than a full agent.

### Question 77

**Scenario:** A document needs supported extraction.

**Answer:** Evaluate an appropriate AI model and validate its output.

### Question 78

**Scenario:** AI calls are slow and expensive.

**Answer:** Minimize context, choose a fit-for-purpose model and avoid unnecessary invocations.

### Question 79

**Scenario:** AI quality drops after release.

**Answer:** Monitor test-set accuracy, latency, failures, overrides and grounding quality.

### Question 80

**Scenario:** A field should become required when Priority is High.

**Answer:** Use a supported business rule when its scope meets all channels.

### Question 81

**Scenario:** Users must follow Qualify, Review and Approve stages.

**Answer:** Use a business process flow for guidance.

### Question 82

**Scenario:** A process must send notifications across services.

**Answer:** Use a cloud flow, even if a BPF guides the stages.

### Question 83

**Scenario:** A current-row value is derived from other columns.

**Answer:** Evaluate formula or calculated column based on supported functions/behavior.

### Question 84

**Scenario:** A parent needs an eventually consistent total of child rows.

**Answer:** Use a rollup column if its recalculation behavior meets the requirement.

### Question 85

**Scenario:** A total must be transactionally current immediately.

**Answer:** Do not rely on rollup alone; evaluate an appropriate synchronous design.

### Question 86

**Scenario:** The same threshold exists in app, flow and table logic with different values.

**Answer:** Centralize the authoritative rule and remove conflicting duplication.

### Question 87

**Scenario:** A field is hidden in the UI to enforce policy.

**Answer:** Reject the design; UI hiding is not authorization.

### Question 88

**Scenario:** A view is filtered to a region.

**Answer:** Treat it as presentation, not row security.

### Question 89

**Scenario:** Dataverse access appears broader than one assigned role.

**Answer:** Remember privileges are cumulative across roles, teams, ownership and sharing.

### Question 90

**Scenario:** A user needs to associate a child row with a parent.

**Answer:** Verify both Append and Append To privileges on the relevant sides.

### Question 91

**Scenario:** An external customer edits only their own rows on a site.

**Answer:** Use authenticated Power Pages identity, web roles and table permissions.

### Question 92

**Scenario:** A Power Pages site is proposed for an internal-only task app.

**Answer:** Prefer canvas/model-driven if they better fit the audience and process.

### Question 93

**Scenario:** A connector is premium.

**Answer:** Validate licensing and data policy before committing to the design.

### Question 94

**Scenario:** A custom API has no suitable certified connector.

**Answer:** Evaluate a custom connector with governed authentication and API design.

### Question 95

**Scenario:** A pro-code extension is proposed despite adequate standard capability.

**Answer:** Prefer the supported standard/low-code option unless nonfunctional needs disqualify it.

### Question 96

**Scenario:** A solution imports but flows are disabled.

**Answer:** Validate connection references, owners, permissions and post-deployment activation.

### Question 97

**Scenario:** A component is missing after import.

**Answer:** Review solution dependencies and add the required asset.

### Question 98

**Scenario:** A preview feature is the only production-critical option.

**Answer:** Confirm scenario allowance, current status and risk; prefer GA where required.

### Question 99

**Scenario:** A question gives an old numerical quota.

**Answer:** Use current official service documentation and focus on the design consequence.

### Question 100

**Scenario:** A scenario asks for minimum administration.

**Answer:** Choose the simplest native supported option that meets every constraint.

## 18. Five-Page Exam Cram

### Page 1: Architecture and ALM

- Canvas app: tailored task UX. Model-driven app: Dataverse/process-centric UX. Power Pages: external web.
- Cloud flow: event/schedule/approval orchestration. Agent: multi-turn conversation/actions. Prompt: reusable generative operation.
- Separate experience, data, automation, intelligence, security and lifecycle decisions.
- Build unmanaged in development; normally deploy managed downstream.
- Environment variable stores configuration; connection reference binds a solution-aware component to a target connection.
- App sharing and solution import do not grant all data permissions.
- Prefer standard capability, then low-code extension, then pro-code when justified.

### Page 2: Dataverse and Model-Driven Apps

- Reuse standard tables when semantics fit. Choose ownership before designing row security.
- Lookup sits on the child/many side. Use an explicit intersection table when a many-to-many relationship has attributes.
- Security is cumulative. Know create/read/write/delete/append/append-to/assign/share and access depth.
- Hidden field and filtered view are not security. Use roles, ownership/sharing and eligible column security.
- Forms, views, charts and dashboards shape UX. App/form/view access remains separate from data authorization.
- Rollup aggregates related rows but is not assumed immediate.

### Page 3: Canvas Apps

- `Set` is global; `UpdateContext` is screen scoped; collection is an in-memory table.
- Prefer named formulas for declarative reusable values. Use components/libraries for UI reuse.
- Delegation affects completeness and scale. Rewrite nondelegable large-source queries.
- Responsive containers, accessible labels, keyboard/focus, contrast and non-color cues.
- Use `IfError`, `Errors`, `Notify`, App Checker and Monitor.
- Minimize connector calls and do not store secrets in formulas/state.

### Page 4: Cloud Flows

- Automated = event, instant = on demand, scheduled = time.
- Filter at trigger. A later Condition does not prevent the run.
- Condition = binary, Switch = discrete branches, Apply to each = arrays, Do until = repeat.
- Scopes plus run-after provide structured error paths.
- Retry only with idempotency/duplicate protection. Bound concurrency according to ordering and throttling.
- Use solution-aware flows, connection references, environment variables, governed ownership and run history.

### Page 5: AI and Business Logic

- Grounding improves relevance, not certainty or authorization.
- Separate instructions from untrusted input. Minimize context/tools. Validate structured output.
- Human review for consequential AI-assisted decisions. Deterministic logic for exact calculations and authorization.
- Agent = conversation/actions; prompt = one reusable generative skill; model = supported AI task.
- Business rule = declarative field/data behavior. BPF = guided stages. Formula/calculated = derived value. Rollup = related aggregate. Flow = asynchronous/cross-service process.

## 19. One-Page Revision Poster

```text
AB-410 LAST-HOUR POSTER

WEIGHTS
Foundation 25-30% | Intelligent apps 25-30% | Logic/automation 40-45%

SELECT
Canvas = bespoke task UX
Model-driven = Dataverse + process UX
Power Pages = external web
Flow = event/schedule/approval
Agent = multi-turn knowledge + actions
Prompt = reusable generation/classification/summarization

ALM
Unmanaged Dev -> Managed downstream
Environment variable = configuration
Connection reference = connector binding
Solution transport != user permission

SECURITY
App access != data access
Form/view hiding != security
Privileges are cumulative
Append + Append To matter
Least privilege, DLP, governed identity

DATAVERSE
Lookup on child/many side
Intersection table if relationship has attributes
Rollup aggregate is not guaranteed immediate
Views present; roles/ownership secure

CANVAS
Set global | UpdateContext screen | Collection temporary table
Delegation warning can mean missing results
Responsive containers + accessibility
IfError + Monitor

FLOWS
Automated event | Instant on demand | Scheduled time
Filter at trigger
Apply to each array | Do until repeat
Retry only when duplicate-safe
Run history for diagnosis

AI
Grounding != truth or authorization
Validate output and structured schema
Exact/high-impact decisions stay deterministic or human-reviewed
Minimize inputs, tools, cost and data exposure

LOGIC
Business rule = declarative behavior
BPF = guided stages
Formula/calculated = derived value
Rollup = related aggregate
Flow = orchestration

EXAM
REACT: Requirements, Exclusions, Architecture, Constraints, Test options
Security -> fit -> ALM -> performance -> cost -> convenience
```

## 20. References

All sources below are official Microsoft sources. **Accessed 2 September 2026.**

### Exam and certification

1. Microsoft, **Microsoft Certified: Intelligent Applications Builder Associate**  
   https://learn.microsoft.com/en-us/credentials/certifications/intelligent-applications-builder-associate
2. Microsoft, **Study guide for Exam AB-410: Building Intelligent Applications**  
   https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-410
3. Microsoft, **Course AB-410T00-A: Build intelligent applications**  
   https://learn.microsoft.com/en-us/training/courses/ab-410t00
4. Microsoft, **Exam scoring and score reports**  
   https://learn.microsoft.com/en-us/credentials/certifications/exam-scoring-reports
5. Microsoft, **Exam sandbox**  
   https://aka.ms/examdemo

### Official course learning paths and all linked modules reviewed

6. **Get started with AI-first solutions in Microsoft Power Platform**  
   https://learn.microsoft.com/en-us/training/paths/design-model-solutions-power-platform/
   - Design AI-powered business solutions with Microsoft Power Platform: https://learn.microsoft.com/en-us/training/modules/design-ai-powered-solutions-power-platform/
   - Create effective prompts for generative AI training tools: https://learn.microsoft.com/en-us/training/modules/create-prompts-for-generative-ai-training-tools/
   - Turn business ideas into Power Platform solutions with Plans: https://learn.microsoft.com/en-us/training/modules/turn-business-ideas-power-platform-solutions-plans/
7. **Build your data model with Microsoft Dataverse**  
   https://learn.microsoft.com/en-us/training/paths/build-data-model-microsoft-dataverse/
   - Create tables in Dataverse: https://learn.microsoft.com/en-us/training/modules/get-started-with-powerapps-common-data-service/
   - Create and manage columns within a table in Dataverse: https://learn.microsoft.com/en-us/training/modules/create-manage-fields-within-entity/
   - Get started with security roles in Dataverse: https://learn.microsoft.com/en-us/training/modules/get-started-security-roles/
8. **Build intelligent apps and portals with Microsoft Power Apps**  
   https://learn.microsoft.com/en-us/training/paths/build-apps-portals-power-apps/
   - Get started with Power Apps canvas apps: https://learn.microsoft.com/en-us/training/modules/get-started-with-powerapps/
   - Customize a canvas app in Power Apps: https://learn.microsoft.com/en-us/training/modules/customize-apps-in-powerapps/
   - Publish, share, and maintain a canvas app: https://learn.microsoft.com/en-us/training/modules/publish-share-maintain-app/
   - Get started with model-driven apps: https://learn.microsoft.com/en-us/training/modules/get-started-with-model-driven-apps-in-powerapps/
   - Configure forms, charts and dashboards: https://learn.microsoft.com/en-us/training/modules/configure-model-driven-apps-customer-engagement-apps/
   - Core components of Power Pages: https://learn.microsoft.com/en-us/training/modules/power-pages-intro/
   - Explore Power Pages design studio: https://learn.microsoft.com/en-us/training/modules/power-pages-studio/
9. **Automate and extend your solutions with AI in Microsoft Power Automate**  
   https://learn.microsoft.com/en-us/training/paths/automate-business-processes-power-automate/
   - Get started with Power Automate: https://learn.microsoft.com/en-us/training/modules/get-started-flows/
   - Use Dataverse triggers and actions: https://learn.microsoft.com/en-us/training/modules/use-dataverse-triggers-actions/
   - Build approval flows: https://learn.microsoft.com/en-us/training/modules/build-approval-flows/
   - Create AI Builder prompts using your own Dataverse data: https://learn.microsoft.com/en-us/training/modules/ai-builder-grounded-prompts/

### Current product documentation used for validation/further verification

10. Microsoft Power Platform documentation: https://learn.microsoft.com/en-us/power-platform/
11. Power Apps documentation: https://learn.microsoft.com/en-us/power-apps/
12. Microsoft Dataverse documentation: https://learn.microsoft.com/en-us/power-apps/maker/data-platform/
13. Canvas delegation overview: https://learn.microsoft.com/en-us/power-apps/maker/canvas-apps/delegation-overview
14. Power Automate documentation: https://learn.microsoft.com/en-us/power-automate/
15. Power Automate limits and configuration: https://learn.microsoft.com/en-us/power-automate/limits-and-config
16. Dataverse API limits: https://learn.microsoft.com/en-us/power-apps/developer/data-platform/api-limits
17. Microsoft Copilot Studio documentation: https://learn.microsoft.com/en-us/microsoft-copilot-studio/
18. AI Builder documentation: https://learn.microsoft.com/en-us/ai-builder/
19. AI Builder licensing: https://learn.microsoft.com/en-us/ai-builder/administer-licensing
20. Power Platform CLI: https://learn.microsoft.com/en-us/power-platform/developer/cli/introduction
21. Power Apps and Power Automate licensing FAQ: https://learn.microsoft.com/en-us/power-platform/admin/powerapps-flow-licensing-faq

---

> **Final currency warning:** Microsoft Power Platform features, model availability, Preview/GA status, licensing, quotas and maker experiences change frequently. Re-open the official study guide and linked product documentation during the final week before the exam. Where this guide deliberately avoids a number, it is because no stable AB-410-specific value was verified in the authoritative blueprint.
