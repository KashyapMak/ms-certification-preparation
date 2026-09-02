# AB-620 Complete Exam Study Guide

> **Microsoft Certified: AI Agent Builder Associate**  
> **Research date:** 2 September 2026  
> **Authority rule:** The current AB-620 study guide defines the assessed scope. Course material is supporting preparation content, not a substitute for the blueprint. Features and interfaces can change, so re-check the official study guide before booking or sitting the exam.

## 1. Exam Snapshot

| Item | Verified detail |
|---|---|
| Exam | AB-620: Designing and Building Integrated AI Agent Solutions in Copilot Studio |
| Certification | Microsoft Certified: AI Agent Builder Associate |
| Level / roles | Intermediate; App Maker and Developer |
| Exam duration | 120 minutes |
| Passing score | 700 or greater |
| Current blueprint | Plan and configure agent solutions; Integrate and extend agents; Test and manage agents |
| Practice assessment | Not currently available on the certification page at research time |
| Official course | AB-620T00-A, three days; Microsoft Learn says availability is 18 September 2026 |
| Study-guide update shown | 21 April 2026 |

Microsoft describes the candidate as a professional developer or advanced builder who creates, extends, and integrates enterprise-grade agents, with familiarity in Power Fx, Dataverse, Power Platform environments, Microsoft 365 Copilot, Microsoft Foundry, Adaptive Cards, RAG, MCP, A2A, prompt engineering, REST APIs, and Copilot Studio fundamentals. view1view6

**Direct official sources**

- [AB-620 Study Guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-620)
- [AB-620T00-A Official Course](https://learn.microsoft.com/en-us/training/courses/ab-620t00)
- [Microsoft Certified: AI Agent Builder Associate](https://learn.microsoft.com/en-us/credentials/certifications/ai-agent-builder-associate/)
- [Copilot Studio documentation](https://learn.microsoft.com/en-us/microsoft-copilot-studio/)
- [Microsoft Foundry documentation](https://learn.microsoft.com/en-us/azure/foundry/)

The passing score comes from Microsoft's exam scoring guidance linked by the study guide. The certification page states a 120-minute assessment. view1view6

## 2. Domain Coverage Matrix

| Domain | Weight | Related learning paths | Priority |
|---|---:|---|---|
| Plan and configure agent solutions | 30–35% | Design conversations and responses; Integrate enterprise systems | 🔥 High Priority |
| Integrate and extend agents in Copilot Studio | 40–45% | Multi-agent solutions; Integrate enterprise systems; Design conversations and responses | 🔥 High Priority |
| Test and manage agents | 20–25% | No dedicated AB-620 course learning path listed at research time | ✅ Medium Priority |

The weights and objectives above are the current official blueprint. view1 The official course currently lists three paths containing 11 modules: three conversation modules, four multi-agent modules, and four enterprise-integration modules. view2view3view4view5

## 3. Blueprint Changes and Course Gap Analysis

### Verified alignment

- **Strong course coverage:** topics, Adaptive Cards, tools, agent flows, HTTP requests, generative answers, custom knowledge, custom prompts, connectors, REST APIs, Azure AI Search, MCP, child agents, connected agents, Foundry agents, Fabric Data agents, and A2A. view3view4view5
- **Classic UI warning:** every listed course module states that it is based on the classic experience while Copilot Studio has introduced a new experience. Learn concepts and outcomes rather than memorising only click paths. view7view10view17
- **Course timing:** at research time, the course page says the instructor-led course becomes available on 18 September 2026. Treat the published self-directed paths as preparatory material, but use the blueprint as final authority. 

### Blueprint objectives not represented by a dedicated listed course module

The following are explicit blueprint items but are not clearly covered by a dedicated module among the 11 modules listed on the course page:

- Full solution planning: identity, channels, deployment, responsible AI, reusable components, internal versus external audiences.
- Agent-flow monitoring and human-in-the-loop flows.
- Computer use configuration and monitoring.
- Application Insights monitoring.
- Formal test sets, evaluation-method selection, and test-result analysis.
- ALM: solutions, environment variables, and Power Platform Pipelines. view1

**Exam implication:** these are first-class objectives. Do not down-rank them merely because the course syllabus has no dedicated path.

### New, retired, preview, deprecated

- **Current/emphasised topics:** MCP, A2A, computer use, connected agents, Microsoft Foundry, Fabric Data agents, Azure AI Search, and Power Platform Pipelines are explicit in the blueprint. view1
- **Preview:** Microsoft states that most questions concern GA features, but commonly used Preview features may appear. The blueprint itself does not label individual objectives GA or Preview. Verify status in the product documentation immediately before the exam. view1
- **Deprecated/retired:** no deprecated or retired features are identified in the supplied study guide or listed course syllabus. It would be incorrect to invent a retirement list.
- **Historical change log:** the current study-guide page does not expose a detailed prior-blueprint comparison. Therefore, precise “added since version X” or “removed since version Y” claims cannot be verified from the reviewed sources.

## 4. Objective-by-Objective Study Notes

# Domain 1: Plan and configure agent solutions (30–35%)

## 4.1 Plan an agent solution

### What You Need to Know

Plan around **audience, desired outcomes, data, actions, identity, channels, lifecycle, safety, ownership, and operations**. Decide whether a single agent is sufficient before adding multiple agents. Separate:

- **Knowledge**: information used to ground answers.
- **Tools/actions**: operations that read or change external state.
- **Topics**: deterministic conversational logic and orchestration.
- **Other agents**: delegated expertise or cross-platform capabilities.
- **Agent flows**: automation designed for agent invocation.

### Mental Model & Decision Rules

| Need | Preferred pattern | Why |
|---|---|---|
| Answer from governed enterprise content | Knowledge source | Grounds generated answers |
| Perform a transaction | Tool, connector, flow, or REST API | Explicit action contract and authentication |
| Fixed conversational control | Topic | Predictable nodes, variables, branching, and responses |
| Separate domain ownership inside one solution | Child agent | Focused internal decomposition |
| Reuse an independently published agent | Connected agent | Independent ownership and lifecycle |
| Integrate a standards-based external agent | A2A | Agent-to-agent delegation across platforms |
| Discover standardised tools/resources from a server | MCP | Standardised tool integration |

The course explicitly distinguishes tools, knowledge sources, and other agents, and asks candidates to select authentication models by integration type. view14

### Implementation Approach

1. Define measurable business outcomes and unacceptable outcomes.
2. Classify users as internal, partner, customer, or anonymous/external.
3. Inventory data sources, actions, sensitivity, residency, and owners.
4. Select identity: user-delegated where the action must honour each user's permissions; maker/service identity only where a controlled shared identity is justified.
5. Select channels and test channel-specific capabilities.
6. Define responsible-AI controls, escalation, audit, data-loss prevention, content boundaries, and human approval.
7. Package assets in a solution and define environment variables before promotion.
8. Define monitoring, evaluation, support, rollback, and cost ownership.

### Security, Governance & Operations

- Apply least privilege to environment roles, connections, data, APIs, and Azure resources.
- Avoid placing secrets in topic text, prompts, variables, source control, or environment-variable values that are not designed as secret stores.
- Use DLP policies to control connector combinations.
- Distinguish user-provided from maker-provided credentials. The connector/REST module explicitly includes these authentication choices. view15
- Design for traceability and human escalation when actions are consequential or ambiguous.
- Review licensing and consumption for Copilot Studio, premium connectors, Azure AI Search, Foundry models, Fabric, Application Insights, and Power Platform Pipelines in the tenant's current plans. No single universal licence combination is verified by the blueprint.

### Exam Gotchas ⚠️

- Multi-agent is not automatically better. It introduces orchestration, latency, testing, security, and ownership complexity.
- Knowledge answers are not transaction tools.
- A connection that works for the maker may fail for end users if authentication or sharing is wrong.
- Channel support can differ, especially for Adaptive Cards.
- “Most secure” usually means least privilege, user-context enforcement where required, governed connections, and explicit approval for high-impact actions.

### Scenario Patterns

- **HR self-service:** use enterprise knowledge for policy answers, a connector/flow for leave submission, user authentication to enforce employee permissions, and human approval where policy requires it.
- **Public support agent:** minimise exposed data and actions, use anonymous-safe knowledge only, add escalation, and do not assume an internal user's delegated identity.
- **Multiple separately owned business agents:** use a connected-agent architecture when publication and lifecycle independence matter.

### Quick Revision Summary

- Start with business outcome and audience.
- Separate knowledge, deterministic logic, actions, and delegation.
- Make identity and data boundaries explicit.
- Prefer least privilege and governed reusable components.
- Design channels, monitoring, evaluation, ALM, cost, and escalation up front.

## 4.2 Create and monitor agent flows in Copilot Studio

### What You Need to Know

The blueprint requires creating agent flows, human-in-the-loop flows, configuring actions/connectors, monitoring, input/output parameters, and error handling. view1 Agent flows can be called from topics to automate business processes. view8

### Mental Model & Decision Rules

- Use an **agent flow** for multi-step automation and connector orchestration.
- Use **human-in-the-loop** when judgement, approval, policy exception, or consequential action demands oversight.
- Use direct **HTTP** for a specific API operation when a suitable connector does not exist and the API contract is stable.
- Keep parameters small, typed, well named, and semantically clear so orchestration can select and call the flow correctly.

### Implementation Example

1. Create the flow from Copilot Studio or add an existing eligible flow.
2. Define required inputs and outputs.
3. Add connector actions and validation.
4. Add approval or human review if needed.
5. Configure success, known-error, timeout, and unexpected-error paths.
6. Save, test with valid and invalid inputs, then add the flow to the agent/topic.
7. Monitor runs, failures, latency, connection issues, and downstream throttling.

Example response contract:

```json
{
  "status": "Succeeded",
  "referenceId": "REQ-1048",
  "userMessage": "Your request was submitted.",
  "retryable": false
}
```

### Security, Governance & Operations

- Do not return internal exception details or secrets to a user.
- Make write operations idempotent where possible.
- Correlate agent conversation, flow run, and downstream request IDs.
- Use approvals for sensitive writes, not merely a confirmation phrase in free text.

### Exam Gotchas ⚠️

- Inputs and outputs are part of the agent-tool contract.
- Successful invocation does not guarantee the downstream business transaction succeeded.
- Handle connector authentication, null data, business-rule failure, throttling, and transient faults separately.
- No universal timeout or retry number was verified in the reviewed blueprint, so memorised numbers should be checked against current product documentation.

### Scenario Pattern

For a purchase request that needs manager approval, an agent flow with structured inputs, an approval step, explicit output status, and failure handling is better than a direct unaudited HTTP write.

### Quick Revision Summary

- Agent flow equals orchestrated automation.
- Human review is a design control.
- Define typed inputs and useful outputs.
- Monitor both technical and business outcomes.
- Return safe error messages and correlation data.

## 4.3 Configure topics

### What You Need to Know

The blueprint covers flows and tools in topics, response formatting, custom prompts, custom knowledge, APIs/HTTP, generative answers, Adaptive Cards, and variables. view1 The conversation learning path covers Adaptive Cards, tools/flows/HTTP, generative answers, custom knowledge, instructions, and Foundry model selection. view3view7view8view9

### Mental Model & Decision Rules

| Requirement | Use |
|---|---|
| Deterministic sequence and branching | Topic nodes and variables |
| Rich information display | Message with Adaptive Card |
| Structured user input | Ask with Adaptive Card |
| Grounded natural-language answer | Generative answers node |
| Special transformation or generation | Custom prompt |
| External state read/write | Tool, flow, connector, or HTTP request |

### Implementation Examples

**Minimal Adaptive Card pattern**

```json
{
  "type": "AdaptiveCard",
  "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.5",
  "body": [
    { "type": "TextBlock", "text": "Request details", "weight": "Bolder" },
    { "type": "Input.Text", "id": "reason", "label": "Reason", "isRequired": true }
  ],
  "actions": [
    { "type": "Action.Submit", "title": "Continue" }
  ]
}
```

Validate the schema version and element support for every target channel. The module explicitly calls out channel-specific rendering for Teams, web, and other surfaces. view7

**HTTP request pattern**

```http
GET https://api.example.com/v1/orders/{orderId}
Authorization: Bearer <token supplied by configured authentication>
Accept: application/json
```

Map the status code and JSON response into variables; branch for not found, unauthorised, throttled, server error, and malformed response. Never hard-code tokens.

### Security, Governance & Operations

- Scope variables correctly and avoid retaining sensitive content unnecessarily.
- Validate user inputs before action calls.
- Constrain prompts with explicit task, allowed sources, expected format, and refusal/escalation behaviour.
- Treat model output as untrusted when feeding downstream actions.
- Log safely and avoid personal/sensitive data leakage.

### Exam Gotchas ⚠️

- An informational card and an Ask with Adaptive Card solve different needs.
- Adaptive Card rendering is channel dependent.
- Generative answers should be grounded and scoped; they do not guarantee correctness.
- Prompt instructions do not replace data permissions or DLP.
- HTTP 200 can still contain a business-level failure payload.

### Scenario Pattern

For “show a policy summary, collect a category, then open a case,” use generative answers for the grounded summary, an Ask Adaptive Card for structured category input, and a connector/flow for case creation.

### Quick Revision Summary

- Use topics for controlled conversation.
- Use cards for rich display and structured input.
- Use generative answers for grounded responses.
- Use tools for actions.
- Validate inputs, outputs, channels, and failures.

# Domain 2: Integrate and extend agents (40–45%)

## 4.4 Connect to enterprise knowledge sources

### What You Need to Know

The objective includes Copilot connectors, Power Platform connectors, and Azure AI Search. view1 The official module distinguishes index-based Copilot connector knowledge, real-time Power Platform connector knowledge, and Azure AI Search vector indexes. view16

### Mental Model & Decision Rules

| Source | Best fit | Trade-off |
|---|---|---|
| Copilot connector | Enterprise content indexed for discovery and grounding | Index freshness and connector governance matter |
| Power Platform connector as knowledge | Real-time access to supported enterprise systems | Runtime latency, connection, permissions, and throttling |
| Azure AI Search | Controlled search index, vector retrieval, Azure architecture | Requires Azure search/index design and operations |

### Implementation Approach

1. Confirm source ownership, sensitivity, and allowed audience.
2. Choose index-based versus real-time access.
3. Configure the source and authentication.
4. Restrict content and honour source permissions.
5. Add meaningful descriptions/instructions.
6. Test direct questions, paraphrases, ambiguous questions, unauthorised content, stale content, and no-answer cases.
7. Publish only after validating end-user authentication.

### Security, Governance & Operations

- Security trimming and identity design are more important than answer fluency.
- Monitor freshness, ingestion/index failures, runtime connector failures, retrieval relevance, citations, and latency.
- Azure services can add consumption cost; real-time connectors can add runtime dependency and throttling risk.

### Exam Gotchas ⚠️

- “Latest data” favours real-time access when supported, not a stale index.
- Large or semantically rich corpora needing controlled vector search can favour Azure AI Search.
- The blueprint does not publish a universal quota, index size, or retention figure.

### Scenario Pattern

A frequently changing service record should use a supported real-time connector when immediate freshness is mandatory. A curated document corpus requiring vector retrieval and Azure operational control can use Azure AI Search.

### Quick Revision Summary

- Decide index versus real-time first.
- Match identity to source permissions.
- Test retrieval quality and unauthorised cases.
- Plan freshness, latency, failures, and cost.

## 4.5 Add tools to agents

### What You Need to Know

The objective covers computer use, MCP, existing custom connectors, and REST APIs. view1 The course covers prebuilt/custom connectors, OpenAPI-based REST tools, API key/OAuth MCP authentication, and selective MCP tool enablement. view15view17

### Mental Model & Decision Rules

| Requirement | Use |
|---|---|
| Supported SaaS operation | Prebuilt connector |
| Governed organisation-specific API reused across Power Platform | Custom connector |
| Direct API contract from OpenAPI | REST API tool |
| Standardised server exposing multiple agent tools/resources | MCP |
| Legacy UI with no suitable API | Computer use, with strong controls |

### OpenAPI Example

```yaml
openapi: 3.0.1
info:
  title: Order Status API
  version: '1.0'
servers:
  - url: https://api.example.com
paths:
  /orders/{orderId}:
    get:
      operationId: getOrderStatus
      summary: Get an order's current status
      parameters:
        - name: orderId
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                type: object
                properties:
                  status:
                    type: string
        '404':
          description: Order not found
```

### Security, Governance & Operations

- Prefer OAuth/user delegation when actions must respect user permissions.
- Use API keys only through supported secret/connection configuration.
- For computer use, isolate the runtime, use least-privileged accounts, constrain applications/sites, and monitor executions.
- Enable only needed MCP tools to reduce ambiguity and exposure.

### Exam Gotchas ⚠️

- MCP is for standardised tool/resource integration; A2A is for agent delegation.
- A connector is preferable to UI automation when a stable supported API exists.
- Computer use is sensitive to UI changes and requires operational monitoring.
- The reviewed sources do not verify universal limits for tool count, runtime, or retries.

### Scenario Pattern

If an ERP exposes a stable supported connector, use it instead of computer use. If an external platform publishes an MCP server with several discoverable tools, MCP can reduce bespoke tool integration. If the target is another autonomous agent, consider A2A instead.

### Quick Revision Summary

- Stable API beats UI automation.
- Connector gives Power Platform governance and reuse.
- REST tool uses an explicit API contract.
- MCP exposes standardised tools; A2A connects agents.
- Secure credentials and minimise enabled capabilities.

## 4.6 Configure multi-agent collaboration

### What You Need to Know

The objective includes multi-agent design, Foundry agents, existing Copilot Studio agents, Fabric Data agents, and A2A. view1 The course separates child agents, connected agents, and external A2A-enabled agents. view10view11view12view13

### Mental Model & Decision Rules

| Pattern | Choose when |
|---|---|
| Child agent | Decompose one Copilot Studio agent into focused internal capabilities with structured input/output |
| Connected Copilot Studio agent | Reuse an independently published Copilot Studio agent |
| Foundry agent | Delegate to an agent built/managed in Microsoft Foundry |
| Fabric Data agent | Natural-language queries over governed Fabric data sources |
| A2A agent | Cross-platform agent delegation through the A2A protocol |

Use an **orchestrator/subagent** pattern when the orchestrator interprets intent and delegates. Use a **workflow-oriented** pattern when sequencing is explicit and predictable. The design module asks candidates to compare these patterns. view10

### Implementation Approach

1. Define each agent's narrow capability, description, inputs, outputs, owner, and failure contract.
2. Select child versus connected based on lifecycle and ownership.
3. Configure the connection and authentication.
4. Make descriptions discriminative so orchestration selects correctly.
5. Test task delegation, conflicting capabilities, unavailable subagents, malformed outputs, latency, and permissions.

### Security, Governance & Operations

- Apply trust boundaries at every agent connection.
- Do not assume the parent agent's identity automatically applies to the child/external system.
- Minimise data passed between agents.
- Monitor end-to-end traces and identify which agent produced each decision or answer.

### Exam Gotchas ⚠️

- Child and connected agents are not synonyms.
- Fabric Data agent is the specific choice for natural-language access over Fabric data.
- A2A is not a replacement for every REST API or MCP integration.
- Multi-agent architecture can reduce maintainability if boundaries overlap.

### Scenario Pattern

A central employee agent delegates analytics questions to a Fabric Data agent, specialised reasoning to a Foundry agent, and HR transactions to an independently owned Copilot Studio agent. Use connected agents because ownership and deployment are independent.

### Quick Revision Summary

- Select by capability, ownership, and lifecycle.
- Child agent is internal decomposition.
- Connected agent is independent reuse.
- Fabric is for governed data questioning.
- A2A enables cross-platform agent delegation.

## 4.7 Integrate agents with Azure

### What You Need to Know

The blueprint names Azure AI Search with Foundry, Foundry model-catalog custom prompts, and Application Insights monitoring. view1 The generative-answers module covers custom prompts using models from the Microsoft Foundry model catalog. view9

### Mental Model & Decision Rules

- Use **Azure AI Search** for controlled retrieval/indexing, including vector-based enterprise grounding.
- Use a **Foundry model-catalog model** when a custom prompt needs an appropriately selected model.
- Use **Application Insights** for operational telemetry and investigation where the supported integration applies.

### Operations

Track latency, failures, dependency calls, retrieval quality, token/consumption trends, user outcomes, and correlation IDs. Avoid recording sensitive prompt content unless policy explicitly permits it. Define alerts and ownership.

### Exam Gotchas ⚠️

- Monitoring is not the same as formal answer-quality evaluation.
- Selecting a model should consider capability, safety, latency, region, governance, and cost, not capability alone.
- No universal model, price, quota, or retention value is stated in the blueprint.

### Quick Revision Summary

- Search grounds; Foundry supplies model choices; Application Insights observes operations.
- Correlate calls across services.
- Protect telemetry data.
- Validate region, access, cost, and model availability.

# Domain 3: Test and manage agents (20–25%)

## 4.8 Evaluate agent performance

### What You Need to Know

You must create a test set, choose an evaluation method, and review results. view1 A test set should represent expected use, paraphrases, edge cases, ambiguity, unsafe requests, unauthorised requests, tool failures, and no-answer conditions.

### Mental Model & Decision Rules

- Use repeatable tests for regression and release gates.
- Evaluate the right dimension: groundedness, relevance, completeness, tool selection, task success, policy compliance, latency, and handoff quality.
- Combine automated/scaled evaluation with human review for nuanced business quality and safety.

### Implementation Approach

1. Derive scenarios from requirements and production-like usage.
2. Define expected outcome and acceptance criteria.
3. Include negative and permission-boundary cases.
4. Run a baseline.
5. Change one design variable where practical.
6. Compare results by metric and segment.
7. Investigate failures, remediate, rerun, and retain evidence.

### Exam Gotchas ⚠️

- A fluent answer can be ungrounded or wrong.
- Average scores can hide severe failures in a critical segment.
- Testing only happy paths is inadequate.
- Production monitoring and pre-release evaluation complement each other.

### Scenario Pattern

If an agent answers policy questions well but occasionally leaks restricted content, do not ship based on a high average relevance score. Add permission-boundary tests, fix source/identity controls, and require zero critical leakage in the release gate.

### Quick Revision Summary

- Test representative and adversarial cases.
- Define expected outcomes before judging results.
- Segment results and inspect critical failures.
- Use repeatable regression sets.

## 4.9 Implement ALM for agents in Copilot Studio

### What You Need to Know

The blueprint requires solutions, adding existing agents to solutions, environment variables, and Power Platform Pipelines. view1

### Mental Model & Decision Rules

- **Solutions** package agents and dependent components.
- **Environment variables** externalise environment-specific configuration.
- **Connection references** decouple solution components from individual connections.
- **Pipelines** promote governed solution versions across environments.

### Implementation Approach

1. Build in a development environment within a solution.
2. Add the existing agent and required components.
3. Replace hard-coded endpoints/configuration with environment variables.
4. Use connection references for connector dependencies.
5. Validate dependencies and export/import through the governed path.
6. Use Power Platform Pipelines for controlled promotion.
7. Run smoke, security, integration, and regression tests after deployment.
8. Document rollback and ownership.

### Security, Governance & Operations

- Separate development, test, and production.
- Restrict production maker/admin privileges.
- Do not use a developer's personal connection as the production dependency.
- Audit releases, approvals, configuration, and failures.

### Exam Gotchas ⚠️

- Copying an agent manually is not robust ALM.
- Environment variables hold configuration, not arbitrary hard-coded secrets.
- Adding only the agent but omitting dependencies causes deployment failures.
- A successful import does not prove runtime connections and permissions work.

### Scenario Pattern

For deployment across dev, test, and production with different API base URLs, package the agent in a solution, use an environment variable for the URL, connection references for connectors, and a Power Platform Pipeline for promotion.

### Quick Revision Summary

- Solution first.
- Externalise configuration.
- Govern connections.
- Promote through pipelines.
- Test after deployment and prepare rollback.

## 5. High-Yield Facts Reference

### Verified exam and course facts

| Fact | Verified value |
|---|---|
| Passing score | 700 or greater |
| Assessment duration | 120 minutes |
| Domain 1 | 30–35% |
| Domain 2 | 40–45% |
| Domain 3 | 20–25% |
| Official course duration | 3 days |
| Listed course availability | 18 September 2026 |
| Listed learning paths/modules | 3 paths / 11 modules |
| Practice assessment | Not available at research time |

Sources: official study guide, certification page, and course page. view1view2view6

### Limits, quotas, retention, timeouts, capacity, and licensing

| Category | Exam-safe conclusion |
|---|---|
| Product limits and quotas | No consolidated numeric limits are provided by the current blueprint. Verify current service-specific limits before the exam. |
| Retention periods | No universal retention value is stated in the reviewed blueprint/course pages. Retention depends on the service and tenant configuration. |
| Tool/flow/API timeout values | Not verified in the authoritative blueprint. Do not rely on an unverified memorised number. |
| Azure AI Search capacity | SKU, region, index design, and service limits matter; no AB-620-specific threshold is stated. |
| Licensing | Feature access can depend on Copilot Studio, Power Platform connectors, Azure, Fabric, Foundry, and tenant licensing. Validate current licensing documentation for the scenario. |
| Performance | Real-time connectors add runtime dependency; indexes add freshness considerations; multi-agent calls add orchestration and latency; computer use adds UI fragility. |

## 6. Service Selection Cheat Sheet

| IF the requirement is... | AND the constraint is... | USE... |
|---|---|---|
| Answer from curated enterprise content | Controlled vector retrieval is required | Azure AI Search knowledge source |
| Answer from enterprise system data | Fresh data is mandatory and supported | Power Platform connector as real-time knowledge |
| Ground answers from indexed enterprise content | Copilot connector is available and governed | Copilot connector knowledge source |
| Perform a supported SaaS action | Connector exists | Prebuilt Power Platform connector |
| Reuse an organisation-specific API | Power Platform governance/reuse matters | Custom connector |
| Call a defined external API | OpenAPI contract is available | REST API tool |
| Access standardised tools/resources | An MCP server exists | MCP connection |
| Delegate to another cross-platform agent | It supports A2A | A2A connection |
| Decompose one agent internally | Same solution/lifecycle | Child agent |
| Reuse an independently published agent | Separate owner/lifecycle | Connected agent |
| Query governed Fabric data conversationally | Fabric capability is already built | Fabric Data agent |
| Automate a legacy UI | No suitable API/connector exists | Computer use with strict controls |
| Automate multi-step work with approval | Human judgement is required | Human-in-the-loop agent flow |
| Collect structured conversational input | Channel supports the card | Ask with Adaptive Card |
| Generate a grounded response in a topic | Knowledge sources are configured | Generative answers node |
| Move agents across environments | Governed deployment is required | Solution + environment variables + pipeline |

## 7. Practice Questions

### Question 1

A support agent must answer from an Azure-managed vector index and the organisation needs direct control over indexing and search architecture. What should you configure?

A. Computer use  
B. Azure AI Search knowledge source  
C. A2A connection  
D. Adaptive Card

**Correct answer: B.** Azure AI Search is the blueprint option for enterprise search/vector-index grounding. A is UI automation, C delegates to another agent, and D formats interaction. view1view16

### Question 2

An agent must submit an expense claim and obtain manager approval before posting it. Which design is best?

A. Generative answers only  
B. A human-in-the-loop agent flow  
C. Copilot connector knowledge  
D. A child agent with no flow

**Correct answer: B.** A flow models the transaction and approval. Knowledge does not perform the transaction, and a child agent alone does not provide the required approval workflow.

### Question 3

A company has a published finance agent owned and released by another team. A central employee agent must delegate finance queries to it. What should you use?

A. Child agent  
B. Connected Copilot Studio agent  
C. Adaptive Card  
D. Azure AI Search

**Correct answer: B.** The separate owner and publication lifecycle favour a connected agent. Child agents are suitable for internal decomposition. view11view12

### Question 4

An external vendor exposes several standardised tools through an MCP server. What is the most direct integration?

A. MCP connection  
B. Fabric Data agent  
C. Copilot connector index  
D. Power Platform Pipeline

**Correct answer: A.** MCP is designed for standardised tool/resource integration. Fabric is for data agents, a Copilot connector grounds knowledge, and pipelines provide ALM. view17

### Question 5

A topic must display an order summary and collect a validated reason from the user in a structured payload. Which node is most appropriate?

A. Informational message only  
B. Ask with Adaptive Card  
C. Generative answers only  
D. Application Insights

**Correct answer: B.** Ask with Adaptive Card collects structured inputs. A message card is mainly display, generative answers generate text, and Application Insights is monitoring. view7

### Question 6

An ERP has a stable supported connector, but a maker proposes computer use to click through its web UI. What is the better design?

A. Computer use because it mimics a person  
B. Use the connector  
C. Use A2A  
D. Store credentials in a topic variable

**Correct answer: B.** A supported connector is generally more stable and governable than UI automation. C is agent delegation, and D is insecure.

### Question 7

A REST API tool works for its maker but fails for published users. What should be investigated first?

A. Font size  
B. Authentication model, connection sharing, and end-user permissions  
C. Adaptive Card schema  
D. Test-set wording only

**Correct answer: B.** Maker-provided versus user-provided authentication and connection permissions directly affect runtime access. view15

### Question 8

You need to deploy the same agent to test and production, with different API URLs. Which design is best?

A. Edit the URL manually after each import  
B. Hard-code both URLs in prompt instructions  
C. Solution, environment variable, connection references, and pipeline  
D. Use an Adaptive Card

**Correct answer: C.** This is the blueprint ALM pattern. The alternatives are manual, unsafe, or unrelated. view1

### Question 9

An evaluation reports high average relevance, but restricted documents appear in a small set of answers. What is the correct response?

A. Release because the average is high  
B. Treat leakage as a critical failure, fix access/grounding controls, and rerun permission tests  
C. Increase card version  
D. Add another connected agent

**Correct answer: B.** Security failures must be segmented and treated according to severity. Average quality cannot compensate for access-control leakage.

### Question 10

Which statement best distinguishes MCP and A2A?

A. MCP is for cards; A2A is for variables  
B. MCP integrates standardised tools/resources; A2A delegates work between agents  
C. They are always interchangeable  
D. Both are only ALM mechanisms

**Correct answer: B.** The official modules teach MCP tool integration and A2A cross-platform agent delegation as different choices. view13view17

### Question 11

An agent needs natural-language querying over existing governed Microsoft Fabric data. What should the orchestrator connect to?

A. Fabric Data agent  
B. HTTP message node only  
C. Adaptive Card designer  
D. Copilot connector solely for action execution

**Correct answer: A.** The connected-agent module explicitly identifies Fabric Data agents for natural-language queries over Fabric data. view12

### Question 12

A team wants to monitor operational failures in an Azure-integrated agent and separately measure groundedness against a repeatable test set. Which answer is best?

A. Application Insights alone does both completely  
B. Use Application Insights for telemetry and an evaluation test set for quality measurement  
C. Use environment variables only  
D. Use a child agent only

**Correct answer: B.** Operational monitoring and formal quality evaluation are complementary blueprint objectives. view1

## 8. Final Revision Section

### 🔥 Top Must-Know Facts

1. Integration and extension is the largest domain at **40–45%**.
2. Distinguish **knowledge, tools, topics, flows, and agents**.
3. Know **child agent versus connected agent versus A2A**.
4. Know **MCP versus connector versus REST API**.
5. Choose **index-based versus real-time knowledge** based on freshness, control, latency, and permissions.
6. Use **Fabric Data agent** for conversational access to governed Fabric data.
7. Use **human-in-the-loop flows** for consequential actions needing judgement or approval.
8. Adaptive Cards are **channel dependent**; Ask cards collect structured input.
9. Test groundedness, task success, safety, permissions, failures, and regression.
10. ALM means **solutions, dependencies, environment variables, connection references, pipelines, and post-deployment tests**.
11. Use **Application Insights** for operations, not as a replacement for answer-quality evaluation.
12. Most exam questions cover GA features, but commonly used Preview features may appear. view1

### ⚠️ Common Traps

- Treating a knowledge source as an action mechanism.
- Choosing computer use when a stable connector/API exists.
- Assuming maker authentication represents published-user behaviour.
- Confusing MCP tools with A2A agent delegation.
- Choosing multi-agent without a clear boundary or ownership need.
- Ignoring channel-specific Adaptive Card support.
- Passing unrestricted model output directly into a write action.
- Testing only happy paths.
- Using average evaluation scores while ignoring critical safety failures.
- Importing only the agent and forgetting dependencies.
- Hard-coding endpoints or credentials.
- Memorising unverified limits that are absent from the blueprint.

### ✅ Rapid Revision Checklist

- [ ] Recite all three domains and weights.
- [ ] Explain every blueprint bullet in one sentence.
- [ ] Draw the knowledge/tool/topic/flow/agent decision tree.
- [ ] Compare Copilot connectors, Power Platform connectors, and Azure AI Search.
- [ ] Compare connector, custom connector, REST, MCP, and computer use.
- [ ] Compare child, connected, Foundry, Fabric, and A2A agents.
- [ ] Review HTTP status/error handling and safe authentication.
- [ ] Review Adaptive Card display versus structured input.
- [ ] Review generative answers, custom instructions, custom knowledge, and custom prompts.
- [ ] Review test-set design and evaluation dimensions.
- [ ] Review solution, environment variable, connection reference, and pipeline ALM.
- [ ] Re-check current study guide, feature status, licensing, and limits.

### 🎯 Exam-Day Strategy

1. Read the last sentence first to identify the required outcome.
2. Highlight constraints: real-time, indexed, external agent, approval, least privilege, independent ownership, Fabric, cross-platform, or no API.
3. Classify the need: knowledge, action, conversation, automation, delegation, monitoring, evaluation, or ALM.
4. Eliminate choices that solve the wrong category.
5. Prefer the least complex supported architecture that meets security, governance, and lifecycle requirements.
6. For “best” answers, include identity, permissions, production operations, and maintainability, not only feature capability.
7. Mark uncertain numeric-limit questions for review; avoid inventing values from unrelated products.
8. Reserve time to review case-study constraints and questions with multiple plausible integrations.

## 9. References

All sources below are official Microsoft Learn pages, accessed **2 September 2026**.

1. **Study guide for Exam AB-620: Designing and Building Integrated AI Agent Solutions in Copilot Studio**  
   https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/ab-620 view1
2. **Course AB-620T00-A: Design and build integrated AI agent solutions in Copilot Studio**  
   https://learn.microsoft.com/en-us/training/courses/ab-620t00 
3. **Microsoft Certified: AI Agent Builder Associate**  
   https://learn.microsoft.com/en-us/credentials/certifications/ai-agent-builder-associate/ view6
4. **Design agent conversations and responses using topics in Microsoft Copilot Studio**  
   https://learn.microsoft.com/en-us/training/paths/design-agent-conversations-responses-topics-copilot-studio/ view3
5. **Deliver rich agent responses using Adaptive Cards in Microsoft Copilot Studio**  
   https://learn.microsoft.com/en-us/training/modules/deliver-rich-agent-responses-adaptive-cards-copilot-studio/ view7
6. **Take action from agent conversations using topics and tools in Microsoft Copilot Studio**  
   https://learn.microsoft.com/en-us/training/modules/take-action-agent-topics-tools-flows-copilot-studio/ view8
7. **Generate AI-powered agent responses using generative answers in Microsoft Copilot Studio**  
   https://learn.microsoft.com/en-us/training/modules/generate-ai-powered-responses-generative-answers-copilot-studio/ view9
8. **Design and build multi-agent solutions in Microsoft Copilot Studio**  
   https://learn.microsoft.com/en-us/training/paths/design-build-multi-agent-solutions-copilot-studio/ view4
9. **Design multi-agent solutions in Microsoft Copilot Studio**  
   https://learn.microsoft.com/en-us/training/modules/design-multi-agent-solutions-copilot-studio/ view10
10. **Delegate agent tasks using child agents in Copilot Studio**  
    https://learn.microsoft.com/en-us/training/modules/delegate-agent-tasks-child-agents-copilot-studio/ view11
11. **Build multi-agent solutions using connected agents in Copilot Studio**  
    https://learn.microsoft.com/en-us/training/modules/build-multi-agent-solutions-connected-agents-copilot-studio/ view12
12. **Build cross-platform multi-agent solutions using the Agent2Agent protocol**  
    https://learn.microsoft.com/en-us/training/modules/build-cross-platform-multi-agent-solutions-agent2agent-copilot-studio/ view13
13. **Integrate agents with enterprise systems in Microsoft Copilot Studio**  
    https://learn.microsoft.com/en-us/training/paths/integrate-agents-enterprise-systems-copilot-studio/ view5
14. **Design integration strategies for agents in Microsoft Copilot Studio**  
    https://learn.microsoft.com/en-us/training/modules/design-enterprise-integration-strategies-agents-copilot-studio/ view14
15. **Take action in external systems using connector and REST API agent tools**  
    https://learn.microsoft.com/en-us/training/modules/take-action-external-systems-connector-rest-api-tools-copilot-studio/ view15
16. **Ground agents with enterprise knowledge using connectors and Azure AI Search**  
    https://learn.microsoft.com/en-us/training/modules/ground-agents-enterprise-knowledge-connectors-azure-ai-search-copilot-studio/ view16
17. **Integrate agents with external systems via MCP in Microsoft Copilot Studio**  
    https://learn.microsoft.com/en-us/training/modules/integrate-agents-external-systems-mcp-copilot-studio/ view17

---

> **Final verification note:** Microsoft can update exam objectives, product navigation, Preview/GA status, licensing, and service limits. Re-open the study guide shortly before the exam. Where the authoritative sources reviewed did not provide a numeric limit, retirement history, or licensing entitlement, this guide explicitly avoids inventing one.
