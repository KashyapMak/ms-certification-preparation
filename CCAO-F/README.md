# Claude Certified Associate – Foundations (CCAO-F)
## Quick Review Exam Guide

> **Purpose:** A domain-by-domain revision guide for the CCAO-F exam, aligned to the published exam blueprint and the Claude Certified Associate Foundations preparation course available on 30 September 2026.
>
> **Use this guide for:** final revision, concept recall, scenario-based decision making, and identifying areas that need hands-on practice.
>
> **Important:** Product capabilities and policies can change. Check the official [certification page](https://anthropic-partners.skilljar.com/claude-certified-associate-foundations-certification), [preparation course](https://anthropic-partners.skilljar.com/path/claude-certified-associate-foundations), [Claude Help Center](https://support.claude.com/), and [Anthropic Usage Policy](https://www.anthropic.com/legal/aup) before your exam.

---

## 1. Exam at a glance

| Item | Detail |
|---|---|
| Exam | Claude Certified Associate – Foundations |
| Code | CCAO-F |
| Audience | Professionals using Claude for everyday business and knowledge-work tasks |
| Technical depth | Foundational; no API or coding expertise expected |
| Questions | 60 |
| Duration | 120 minutes |
| Question types | Multiple choice and multiple response |
| Passing score | 720 on a scaled range of 100–1,000 |
| Delivery | Pearson VUE test centre or online proctored |
| Credential validity | 12 months |

### Domain weighting

| Domain | Weight | Approx. emphasis out of 60 questions |
|---|---:|---:|
| 1. Prompting and Task Execution | 14% | 8–9 |
| 2. Output Evaluation and Validation | 21% | 12–13 |
| 3. Product and Model Selection | 12% | 7–8 |
| 4. Workflow Integration and Solution Design | 16% | 9–10 |
| 5. Configuration and Knowledge Management | 12% | 7–8 |
| 6. Governance, Risk, and Responsible Use | 15% | 9 |
| 7. Troubleshooting and Optimization | 10% | 6 |

> Approximate question counts are calculated from domain percentages. An actual exam form may distribute items differently.

### Exam mindset

The exam is likely to test professional judgment more than feature memorisation. For scenario questions, prefer the option that:

- Fits the stated business need rather than using the most powerful feature by default.
- Protects sensitive information and follows organisational policy.
- Grounds important claims in reliable source material.
- Adds human review where consequences are significant.
- Uses clear success criteria and repeatable evaluation.
- Fixes the root cause rather than repeatedly rewriting an entire prompt.
- Keeps people responsible for decisions, approvals, and accountability.

---

# Domain 1: Prompting and Task Execution (14%)

## 1.1 Create effective prompts for business and technical tasks

### Definition

An effective prompt gives Claude enough information to understand the task, expected result, constraints, and quality standard. A practical structure is:

1. **Role or perspective:** Who Claude should act as, where useful.
2. **Context:** Background needed to understand the task.
3. **Task:** The action Claude must perform.
4. **Input:** Source material or data to use.
5. **Constraints:** Boundaries, exclusions, tone, length, or policy.
6. **Output format:** Bullets, table, report, JSON, email, or another format.
7. **Success criteria:** What a good answer must contain.

### Exam-relevant points

- Be clear, direct, and specific.
- Separate instructions from source material using headings, delimiters, or XML tags.
- State the intended audience and purpose.
- Ask Claude to use only supplied sources when unsupported invention would be risky.
- Specify what Claude should do when information is missing, such as flagging the gap instead of guessing.
- Provide examples when the required pattern, tone, or classification boundary is difficult to describe.
- Avoid unnecessary persona instructions that don't improve the task.

### Example

```text
You are reviewing a project status report for senior management.

Task:
Summarise the attached report in five bullets.

Requirements:
- Cover progress, risks, decisions required, budget status, and next milestone.
- Use only information in the report.
- If a required fact is missing, write "Not stated".
- Keep each bullet below 30 words.

Output:
Five labelled bullets followed by a one-sentence confidence note.
```

### Exam tip

If the initial request is vague, the best improvement usually adds missing context, constraints, source boundaries, output format, and success criteria. A longer prompt isn't automatically better.

---

## 1.2 Apply task decomposition to complex requests

### Definition

Task decomposition divides a complex objective into smaller, verifiable steps. Prompt chaining uses the output of one step as input to the next.

### When to decompose

- Different stages require different reasoning or evidence.
- An intermediate result should be reviewed before continuing.
- The task contains dependencies, such as research before recommendation.
- A single prompt produces incomplete or inconsistent results.
- Different stages require different models, tools, people, or approval controls.

### Common pattern

1. Clarify the objective and assumptions.
2. Extract relevant information.
3. Analyse or classify it.
4. Produce a draft.
5. Evaluate against criteria.
6. Revise and prepare the final output.

### Example

For a vendor recommendation:

1. Extract each requirement from the request for proposal.
2. Build a weighted evaluation matrix.
3. Map vendor evidence to each criterion.
4. Highlight missing evidence.
5. Calculate or explain the comparison.
6. Draft a recommendation for human approval.

### Exam tip

Choose decomposition when traceability and quality matter. Use one prompt for a simple, self-contained task where intermediate review adds little value.

---

## 1.3 Iterate prompts to improve output quality

### Definition

Prompt iteration means changing a prompt deliberately after diagnosing why the result failed. Good iteration changes one or a small number of variables at a time.

### Diagnostic sequence

1. Define the failure precisely.
2. Check whether the source information is sufficient.
3. Check task clarity and conflicting instructions.
4. Add or refine success criteria.
5. Add an example if the desired pattern is ambiguous.
6. Split the task if it is overloaded.
7. Re-run and compare against the same criteria.

### Poor versus better iteration

- **Poor:** “Try again and make it better.”
- **Better:** “Revise the answer so that every recommendation cites evidence from the supplied report, removes unsupported claims, and limits the executive summary to 150 words.”

### Exam tip

Don't jump immediately to another model. First determine whether the problem comes from unclear instructions, weak evidence, excessive context, the wrong feature, or an unsuitable model.

---

## 1.4 Adapt prompting to the task type

### Analysis

- Define the question and evaluation criteria.
- Provide complete, relevant data.
- Ask Claude to distinguish evidence, inference, and uncertainty.
- Request assumptions and gaps.

### Research

- Define scope, date range, geography, and acceptable sources.
- Request citations or source links.
- Verify important claims using primary or authoritative sources.
- Treat generated summaries as a starting point, not final proof.

### Drafting

- Specify audience, purpose, tone, length, structure, and call to action.
- Supply reference examples if house style matters.
- Ask for alternatives only when comparison provides value.

### Brainstorming

- Encourage breadth first, then apply evaluation criteria.
- Separate idea generation from selection.
- Ask for distinct options rather than minor variations.

### Exam tip

Match the prompt to the cognitive task. Research needs grounding and citations; drafting needs audience and tone; analysis needs criteria and evidence; brainstorming needs variety followed by filtering.

---

# Domain 2: Output Evaluation and Validation (21%)

## 2.1 Evaluate accuracy and completeness

### Definitions

- **Accuracy:** Claims agree with reliable evidence.
- **Completeness:** The answer addresses all required parts.
- **Relevance:** Content supports the requested objective.
- **Consistency:** Statements don't contradict each other or the source.
- **Fitness for purpose:** The result suits its audience, risk level, and intended use.

### Practical evaluation checklist

- Were all instructions followed?
- Are factual claims supported?
- Were calculations checked independently?
- Are dates, names, units, totals, and citations correct?
- Are assumptions visible?
- Is any required information missing?
- Does the format match the request?
- Can the intended audience safely act on it?

### Exam tip

Fluent writing isn't evidence of correctness. Evaluate the output against explicit criteria and source material.

---

## 2.2 Identify hallucinations, inconsistencies, and bias

### Hallucination

A plausible-sounding statement that isn't supported by the available evidence or is factually wrong.

### Warning signs

- Citations that don't exist or don't support the claim.
- Precise numbers without a source.
- Unstated assumptions presented as facts.
- Confident interpretation where the input is ambiguous.
- Names, dates, policies, or quotations absent from the source.

### Inconsistency

A conflict within the response or between the response and its source. Check totals, conclusions, terminology, chronology, and recommendations.

### Bias

A systematic skew in framing, assumptions, evidence selection, or treatment of people and alternatives. Mitigation includes representative evidence, neutral criteria, counterexamples, diverse review, and human oversight.

### Exam tip

Asking Claude whether its own answer is correct can help identify issues, but it isn't independent validation. Verify against original or authoritative evidence.

---

## 2.3 Apply fact-checking and validation techniques

### Strong validation methods

- Compare claims with the original supplied document.
- Verify externally using authoritative primary sources.
- Recalculate numbers independently.
- Trace citations to the exact supporting passage.
- Use a checklist or rubric defined before generation.
- Compare multiple outputs to find unstable answers.
- Ask a qualified human to review high-impact content.

### Source hierarchy

Prefer:

1. Primary source or official record.
2. Authoritative regulator, standards body, or product documentation.
3. Trusted secondary source.
4. Community or informal sources only as supporting context.

### Example

If Claude summarises a contract, compare every obligation, amount, deadline, exception, and defined term with the contract. Don't validate one AI-generated interpretation using another AI-generated summary.

### Exam tip

The required validation level should increase with impact, irreversibility, uncertainty, and regulatory exposure.

---

## 2.4 Decide when human review is required

### Human review is especially important when

- The output affects legal rights, safety, employment, finance, healthcare, or regulatory duties.
- The decision has material consequences for a person or organisation.
- Source evidence is incomplete, conflicting, or uncertain.
- Sensitive or confidential data is involved.
- The output will be published externally or sent to senior stakeholders.
- An authorised professional must exercise judgment or approve the result.

### Appropriate human responsibilities

- Validate facts and assumptions.
- Apply domain expertise and organisational context.
- Approve actions and external communication.
- Handle exceptions and appeals.
- Remain accountable for outcomes.

### Exam tip

Human-in-the-loop doesn't mean a person merely clicks “approve.” The reviewer must have enough expertise, evidence, time, and authority to challenge the result.

---

## 2.5 Edit, adapt, refine, and compare outputs

### Key points

- Assess alternatives against the same rubric.
- Adapt detail, tone, terminology, and format to the audience.
- Preserve factual meaning while simplifying language.
- Remove unsupported statements and unnecessary content.
- Keep a clear link between source, draft, review, and final version where traceability matters.

### Exam tip

The “best-written” version may not be the best answer. Select the version that most completely meets the objective, evidence, audience, and risk requirements.

---

## 2.6 Select an appropriate output format

### Common choices

- **Inline response:** Quick explanation or short answer.
- **Table:** Comparison, structured review, or matrix.
- **Artifact:** Substantial content intended for iteration, preview, editing, or reuse.
- **Structured data:** Machine-readable or consistently formatted downstream use.
- **Checklist:** Repeatable control or review activity.

### Exam tip

Choose a format based on how the result will be consumed. Don't choose an Artifact merely because it looks polished, or structured data when a person needs a readable narrative.

---

# Domain 3: Product and Model Selection (12%)

## 3.1 Select the right Claude product feature

### Chat

Best for ad hoc conversation, quick drafting, questions, and iterative exploration where persistent shared configuration isn't required.

### Projects

Best for recurring or team-aligned work that benefits from project instructions, reusable knowledge, and consistent context.

### Research mode

Best for multi-source investigation that requires browsing, synthesis, and citations. Important claims still require verification.

### Artifacts

Best for substantial outputs that users need to view, revise, organise, or reuse separately from the conversation, such as documents, code, or interactive content.

### Connectors

Best when Claude needs authorised access to external services or organisational information. Access, data sensitivity, and policy must be assessed first.

### Exam tip

Select the simplest feature that satisfies the requirement. Projects solve persistent context; Research solves source discovery; Artifacts support creation and iteration; connectors extend access to approved systems.

---

## 3.2 Differentiate model families

### Haiku

- Optimised for speed and lower cost.
- Appropriate for high-volume, straightforward, or latency-sensitive tasks.
- Examples: simple classification, extraction, quick summaries, routine drafting.

### Sonnet

- Balanced capability, speed, and cost.
- Strong default for many professional tasks.
- Examples: analysis, structured drafting, routine problem solving, mixed workloads.

### Opus

- Intended for the most demanding reasoning and quality-sensitive work.
- Usually higher cost and slower than lighter models.
- Examples: complex analysis, difficult synthesis, nuanced strategic work.

> Model names and availability evolve. Focus on the trade-off pattern: **speed/cost versus capability/quality**, then verify currently available models in the product.

### Exam tip

Don't select Opus simply because it is the most capable tier. Choose the least costly and fastest model that reliably meets the defined quality and risk requirement.

---

## 3.3 Align model choice with requirements

Consider:

- Task complexity.
- Required quality and reasoning depth.
- Latency expectations.
- Volume and cost.
- Consequence of an error.
- Need for tool use or specific product features.
- Results from testing on representative examples.

### Exam tip

Benchmark model choices using real use cases and success criteria. General reputation is weaker evidence than task-specific evaluation.

---

## 3.4 Manage context and memory

### Key concepts

- **Context:** Information available to Claude in the current interaction.
- **Project knowledge:** Reusable sources associated with a Project.
- **Project instructions:** Persistent guidance for work within that Project.
- **Memory/personalisation:** Product features that may carry useful preferences or context across conversations, depending on settings and availability.

### When to continue, summarise, restart, or persist

- **Continue:** The conversation remains focused and the existing context is still relevant.
- **Summarise:** The thread is long but key decisions and facts should carry forward.
- **Restart:** Old assumptions, irrelevant content, or conflicting instructions are degrading performance.
- **Persist in a Project:** The information is stable, reusable, authorised, and relevant across many conversations.

### Exam tip

A long conversation isn't automatically better. Excess irrelevant context can distract the model. Keep context current, focused, and authoritative.

---

# Domain 4: Workflow Integration and Solution Design (16%)

## 4.1 Analyse requirements and use cases

### Requirement categories

- Business objective and measurable outcome.
- Users and stakeholders.
- Inputs and data sources.
- Process steps and decisions.
- Output and delivery channel.
- Quality, cost, and timing expectations.
- Privacy, security, regulatory, and policy constraints.
- Human review and escalation.

### Suitability questions

- Is the task language-heavy, repetitive, or pattern-based?
- Is there enough reliable information?
- Can quality be measured?
- Can a person review exceptions?
- Does the benefit justify the risk and effort?

### Exam tip

Start with the business problem, not the Claude feature. A well-designed solution may automate only part of the workflow.

---

## 4.2 Use Claude for research, planning, and process optimisation

### Good uses

- Synthesising approved sources.
- Drafting plans and identifying dependencies.
- Generating options and questions.
- Mapping current processes and bottlenecks.
- Creating first drafts, checklists, or meeting summaries.

### Controls

- Define trusted sources.
- Verify citations and current facts.
- Record assumptions.
- Require human approval for decisions.
- Avoid exposing unauthorised data.

### Exam tip

Claude can accelerate analysis and drafting, but the workflow must still include evidence checks, approvals, and exception handling.

---

## 4.3 Support solution design, development, and iteration

### Iterative lifecycle

1. Define the problem and success criteria.
2. Design the human-plus-Claude workflow.
3. Prototype with representative tasks.
4. Evaluate quality, risk, cost, and usability.
5. Refine prompts, configuration, model, or process.
6. Pilot with controlled users.
7. Monitor and update after release.

### Exam tip

A successful prototype isn't sufficient evidence for production. Test normal cases, difficult cases, edge cases, and failure paths.

---

## 4.4 Augment versus redesign a workflow

### Augmentation

Claude supports an existing step while people retain the process and decision structure. It is often faster and lower risk to introduce.

### Redesign

The workflow is reorganised around new capabilities. It may provide more value but needs stronger change management, controls, role clarity, and testing.

### Example

- **Augment:** Claude drafts a customer response; an employee reviews and sends it.
- **Redesign:** Claude classifies requests, drafts responses, routes exceptions, and creates structured records, with people reviewing high-risk cases.

### Exam tip

Prefer gradual augmentation when risks, requirements, or user behaviour aren't yet well understood.

---

## 4.5 Communicate value and limitations

### Communicate value through

- Faster cycle time.
- Reduced repetitive effort.
- Improved consistency.
- Better access to organisational knowledge.
- More time for professional judgment.

### Communicate limitations honestly

- Outputs can be wrong or unsupported.
- Results depend on prompt, context, source quality, model, and configuration.
- Product access doesn't remove privacy or governance obligations.
- Claude isn't accountable for organisational decisions.

### Exam tip

Avoid absolute promises such as “eliminates errors.” Use measured claims supported by pilot results and quality metrics.

---

# Domain 5: Configuration and Knowledge Management (12%)

## 5.1 Configure Projects with instructions and knowledge

### Project instructions should define

- Purpose and scope.
- Intended users and audience.
- Preferred method or workflow.
- Output standards and style.
- Trusted sources and evidence rules.
- Prohibited actions or content.
- Escalation and human-review conditions.

### Knowledge sources should be

- Relevant and authoritative.
- Current and version-controlled where needed.
- Approved for use.
- Free from unnecessary sensitive data.
- Organised and clearly named.

### Exam tip

Use Project instructions for stable, reusable behaviour. Keep task-specific details in the current prompt.

---

## 5.2 Manage uploaded knowledge and connectors

### Uploaded knowledge

Suitable for controlled reference documents. Confirm that users are authorised to upload the content and that obsolete files are removed or replaced.

### Connectors

Allow Claude to use authorised external services such as workspace tools. Connector access doesn't mean every available item is appropriate for every task.

### Control checklist

- Verify identity and access permissions.
- Use minimum necessary access.
- Understand where data comes from.
- Avoid combining datasets in ways that create new sensitivity.
- Review sharing and retention requirements.
- Remove access when no longer required.

### Exam tip

“Claude can access it” and “Claude should use it” are different judgments.

---

## 5.3 Create effective system-level instructions

### Characteristics

- Clear and non-contradictory.
- Relevant across the Project.
- Specific enough to guide behaviour.
- Explicit about source use, uncertainty, and escalation.
- Tested on varied representative tasks.
- Maintained as requirements change.

### Example

```text
Use the approved policy documents in Project knowledge as the primary source.
If the documents don't answer the question, state that the policy is unclear and
refer the user to the Compliance team. Don't invent policy requirements.
For every answer, cite the document title and section used.
```

### Exam tip

Don't put temporary dates, one-off customer information, or task-specific data into long-lived instructions unless they genuinely apply across the Project.

---

## 5.4 Maintain configurations and sources

### Maintenance activities

- Assign an owner.
- Review instructions and knowledge on a schedule.
- Replace obsolete documents.
- Record important changes.
- Test after policy, source, model, or connector changes.
- Gather user feedback and error examples.
- Remove duplicated or conflicting guidance.

### Exam tip

Configuration is not a one-time setup. Stale knowledge can produce confidently outdated answers.

---

# Domain 6: Governance, Risk, and Responsible Use (15%)

## 6.1 Identify appropriate and inappropriate use cases

### Usually appropriate with suitable controls

- Drafting and summarising non-sensitive material.
- Brainstorming and planning.
- Extracting information from authorised documents.
- Supporting research with source verification.
- Preparing first drafts for expert review.

### Inappropriate or high-risk without stronger controls

- Entering data that policy or law prohibits.
- Allowing Claude to make unreviewed high-impact decisions.
- Presenting generated content as verified when it hasn't been checked.
- Circumventing safety controls, access restrictions, or legal obligations.
- Using content without considering intellectual property and licensing.

### Exam tip

Evaluate the data, purpose, affected people, decision impact, and controls. The same capability can be appropriate in one context and inappropriate in another.

---

## 6.2 Apply privacy, regulatory, and data-sensitivity considerations

### Data questions to ask

- What data is being used?
- Is it personal, confidential, regulated, or commercially sensitive?
- Is there a lawful and organisationally approved purpose?
- Is all the data necessary?
- Who can access the source and output?
- What retention, location, or deletion requirements apply?
- Can data be minimised, anonymised, or redacted?

### Exam tip

Don't assume removing a person's name makes a dataset anonymous. Other attributes may still identify them.

---

## 6.3 Follow organisational policy and governance

### Typical governance controls

- Approved tools, accounts, and models.
- Data classification and acceptable-use rules.
- Access control and least privilege.
- Human review and approval thresholds.
- Testing and release gates.
- Logging, monitoring, incident reporting, and audit records.
- Named ownership and accountability.

### Exam tip

When product capability conflicts with organisational policy, follow policy and use the approved escalation route.

---

## 6.4 Understand ethical implications

### Key areas

- Fairness and discrimination.
- Transparency about AI involvement.
- Accountability for decisions.
- Accessibility and inclusion.
- Avoiding deceptive or manipulative use.
- Respecting intellectual property.
- Providing a route for correction, challenge, or appeal.

### Exam tip

A use case can be technically possible and legally uncertain yet still ethically problematic. Consider impact on affected people, not only efficiency.

---

# Domain 7: Troubleshooting and Optimization (10%)

## 7.1 Diagnose poor prompts and outputs

### Common symptom-to-cause map

| Symptom | Likely cause | Targeted fix |
|---|---|---|
| Generic answer | Insufficient context or criteria | Add audience, purpose, evidence, and success criteria |
| Missing requirements | Too many instructions or unclear structure | Use a checklist, headings, or decomposition |
| Unsupported facts | Weak grounding or request encourages guessing | Supply trusted sources and require uncertainty flags |
| Wrong format | Output specification is absent or ambiguous | Provide an explicit schema or example |
| Inconsistent results | Ambiguous task or weak examples | Tighten boundaries and add representative examples |
| Important source ignored | Excessive, irrelevant, or conflicting context | Curate sources and identify precedence |
| Slow or costly workflow | Model or process is oversized | Test a lighter model and reduce unnecessary steps |
| Stale answer | Old Project knowledge or conversation context | Update sources, summarise, or restart |

### Exam tip

Diagnose before changing. Replacing the model won't correct obsolete source material or contradictory instructions.

---

## 7.2 Adjust based on feedback and results

### Effective feedback loop

1. Collect specific failed examples.
2. Categorise the failures.
3. Identify the root cause.
4. Change one component.
5. Re-test with a representative set.
6. Compare against baseline measures.
7. Document and retain improvements.

### Exam tip

User preference feedback and factual correctness feedback are different. A tone change shouldn't replace factual validation.

---

## 7.3 Optimise efficiency and effectiveness

### Optimisation options

- Use a lighter model for simpler steps.
- Remove duplicated context.
- Reuse stable Project instructions and approved templates.
- Break complex workflows into measurable stages.
- Use connectors only when they add needed information.
- Add human review at risk-based points rather than reviewing everything equally.
- Track quality, time, cost, correction rate, and user outcomes.

### Exam tip

Optimisation means meeting required quality and controls with less time, cost, or effort. A faster workflow that produces unsafe or inaccurate results isn't optimised.

---

# Cross-domain scenario patterns

## Scenario 1: Executive report contains invented figures

**Best response:** Stop publication, trace every figure to the source, remove or label unsupported statements, have the accountable owner review the revised report, and improve the prompt to prohibit guessing.

**Domains:** Evaluation, governance, troubleshooting, prompting.

## Scenario 2: A team repeats the same task every week

**Best response:** Create a Project with approved knowledge and stable instructions, use a standard prompt/template, define an evaluation checklist, and assign ownership for source updates.

**Domains:** Configuration, workflow integration, evaluation.

## Scenario 3: Thousands of simple records need classification

**Best response:** Test Haiku or another suitable lightweight model on representative data, use clear labels and examples, measure precision/recall or agreed business metrics, and route uncertain/high-risk cases to people.

**Domains:** Model selection, prompting, workflow design, evaluation.

## Scenario 4: Complex strategic analysis for leadership

**Best response:** Use a capable model suited to complex reasoning, provide authoritative sources and evaluation criteria, decompose research and synthesis, state uncertainty, and require expert review.

**Domains:** Model selection, prompting, evaluation, workflow design.

## Scenario 5: Claude can access confidential documents through a connector

**Best response:** Confirm approved use, permissions, data classification, minimum necessary access, output audience, and retention requirements before using the information.

**Domains:** Configuration, governance.

## Scenario 6: A long chat starts producing inconsistent answers

**Best response:** Identify and retain the essential current facts, summarise them into clean context, start a fresh conversation when needed, and move stable reusable material into an appropriately governed Project.

**Domains:** Product selection, context management, troubleshooting.

---

# Last-minute memory sheet

## Prompt formula

**Context + task + input + constraints + output format + success criteria**

## Output validation formula

**Accuracy + completeness + consistency + relevance + audience fit + risk review**

## Model selection formula

**Task complexity + quality + speed + cost + risk + tested performance**

## Workflow formula

**Objective → inputs → Claude steps → human steps → controls → measures → feedback**

## Governance formula

**Approved purpose + minimum data + authorised access + human accountability + monitoring**

## Troubleshooting formula

**Symptom → evidence → root cause → targeted change → re-test → retain**

---

# Common exam traps

- Choosing the most capable model for every task.
- Treating fluent wording as factual accuracy.
- Asking Claude to verify itself without checking independent evidence.
- Uploading sensitive data merely because the feature supports uploads.
- Automating an entire process before understanding risk and exceptions.
- Keeping obsolete files in Project knowledge.
- Adding more prompt detail when the real problem is missing or poor-quality data.
- Using a new conversation when stable Project context is the actual need.
- Using a Project when a one-off chat is sufficient.
- Treating human review as a ceremonial approval rather than an informed control.
- Optimising speed or cost below the required quality threshold.
- Applying changes without measuring whether they solved the failure.

---

# 20-question self-check

1. Can I construct a prompt with context, task, constraints, format, and success criteria?
2. Can I explain when examples improve a prompt?
3. Can I recognise when to decompose a task?
4. Can I distinguish accuracy from completeness?
5. Can I identify an unsupported but plausible claim?
6. Can I choose an independent validation method?
7. Can I identify when expert human review is mandatory?
8. Can I select inline, table, Artifact, or structured output appropriately?
9. Can I choose among Chat, Projects, Research, Artifacts, and connectors?
10. Can I explain the Haiku, Sonnet, and Opus trade-off pattern?
11. Can I decide when to continue, summarise, restart, or persist context?
12. Can I map a business workflow into Claude and human steps?
13. Can I distinguish augmentation from workflow redesign?
14. Can I communicate Claude's benefits without overstating reliability?
15. Can I write stable Project instructions?
16. Can I manage knowledge freshness and connector permissions?
17. Can I assess data sensitivity and purpose before use?
18. Can I identify an ethical issue even if a task is technically feasible?
19. Can I diagnose the root cause of a poor output?
20. Can I optimise cost and speed without compromising required quality?

If any answer is “no,” revisit the matching section and practise one realistic scenario in Claude.

---

# Final review strategy

## If you have 60 minutes

- 15 minutes: Domain 2, Output Evaluation and Validation.
- 10 minutes: Domain 4, Workflow Integration and Solution Design.
- 10 minutes: Domain 6, Governance, Risk, and Responsible Use.
- 10 minutes: Domain 1, Prompting and Task Execution.
- 10 minutes: Domains 3 and 5, product/model selection and Projects.
- 5 minutes: Domain 7 and common exam traps.

## During the exam

- Read whether the question asks for the **best**, **first**, or **most appropriate** action.
- For multiple-response items, select exactly the stated number.
- Eliminate options that ignore evidence, policy, permissions, or human accountability.
- Prefer proportionate controls rather than unnecessary complexity.
- Don't assume features, permissions, or facts that the scenario doesn't state.
- Flag difficult questions and return after answering clearer ones.
- Use the full scenario: the audience, risk, source, and intended outcome often determine the answer.

---

# Source references

1. [Claude Certified Associate – Foundations certification page](https://anthropic-partners.skilljar.com/claude-certified-associate-foundations-certification)
2. [Claude Certified Associate – Foundations prep course](https://anthropic-partners.skilljar.com/path/claude-certified-associate-foundations)
3. [Claude Help Center](https://support.claude.com/)
4. [Claude documentation: prompt engineering](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview)
5. [Anthropic Usage Policy](https://www.anthropic.com/legal/aup)
6. [Anthropic Privacy Center](https://privacy.claude.com/)
7. [Claude model overview](https://platform.claude.com/docs/en/about-claude/models/overview)
8. [Independent blueprint cross-check](https://claudecertificationguide.com/ccao-f)
9. [Domain-to-documentation study map](https://ravikirans.com/claude-certified-associate-foundations-study-guide/)

---

*Prepared as an independent study aid. It isn't an official Anthropic publication and doesn't reproduce live course lesson content or exam questions.*
