# Lab 4 — Manus AI Prompts

[← Lab 4 Guide](README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)

ใช้ prompts นี้กับ [Manus Lab Input](../templates/manus-lab-input.md) เท่านั้น ห้ามใช้ข้อมูลจริง

## Primary Agent Task Prompt

```text
You are a Business Request Management Agent.

Your goal is to triage the attached simulated business requests
and create a draft Situation & Follow-up Report for every request
that you classify as HIGH.

This is a bounded analysis and artifact-creation task.

Do NOT create a workflow, automation, Make scenario, scheduled task,
application, integration, webhook, email, message, or external action.
Do NOT browse the web or use external sources.
Use only the attached file.

First, present a concise execution plan with no more than 5 steps.
Then execute the plan.

For every request:
1. Preserve the Request ID.
2. Summarize it in one concise Thai sentence.
3. Classify priority as exactly HIGH, MEDIUM, or LOW.
4. Explain the business-impact reason using source evidence.
5. Recommend the next business action.
6. Set Human Review to YES when information is missing,
   the impact is high, or a sensitive decision may be involved.
7. List missing information when applicable.

Priority rules:

HIGH:
- Immediate customer impact
- Significant revenue or financial impact
- Critical operational disruption
- Serious compliance or reputation risk
- A time-sensitive issue where delay causes significant business impact

MEDIUM:
- Important but not immediately critical
- Requires management attention
- Deadline within several days
- Operations can continue

LOW:
- Routine administrative work
- General information request
- No immediate business impact
- No urgent deadline

Do not classify HIGH only because the request contains words such as
urgent, ASAP, immediately, or as soon as possible.

Create three deliverables in Thai:

Deliverable 1: Request Triage
- A table with Request ID, Department, Summary, Priority, Reason,
  Recommended Action, Human Review, and Missing Information.
- Include exactly one row for every input record.

Deliverable 2: HIGH Priority Situation & Follow-up Reports
- Create exactly one draft report for every Request ID classified as HIGH.
- Do not create reports for MEDIUM or LOW requests.
- Use a separate artifact/file per HIGH case when supported.
  Otherwise use clearly separated report sections in one artifact.
- Suggested filename:
  DRAFT-HIGH-Situation-Report-[Request-ID]

Each HIGH report must include:
1. DRAFT — HIGH PRIORITY — HUMAN REVIEW REQUIRED
2. Request ID, Department, Source Priority
3. Situation Overview
4. Evidence-based Business Impact:
   Customer, Financial/Revenue, Operations,
   Compliance/Reputation, Time Sensitivity
5. Why HIGH
6. Immediate Attention Required
   Label all items as recommendations pending human confirmation.
7. Follow-up table:
   Follow-up Item | Proposed Owner | Target Time | Status | Evidence/Source
   Use "Manager to assign" for unknown owners.
   Use "Manager to confirm" for unknown target times.
   Use OPEN or PENDING VALIDATION; never use RESOLVED.
8. Decisions or Approvals Required
9. Missing Information
10. Human Review Sign-off

Do not invent facts, counts, amounts, root causes, owner names,
deadlines, resolution status, policies, or SLAs.
Use "ไม่พบในข้อมูลต้นทาง" for unsupported information.

Deliverable 3: HIGH Follow-up Index
- Request ID
- Report/Artifact Name
- Report Status = DRAFT — HUMAN REVIEW REQUIRED
- Follow-up Status = OPEN
- Owner = Manager to assign
- Target Time = Manager to confirm

Validate that:
- the triage row count equals the input record count;
- HIGH + MEDIUM + LOW equals the total;
- the HIGH report count equals the number of HIGH triage rows;
- every HIGH Request ID has exactly one report and one index row;
- no MEDIUM or LOW Request ID has a HIGH report;
- every report claim is supported by its source record;
- no external action was performed.

End with a short Validation Summary.
```

## Compact Prompt — Low-credit Fallback

```text
Analyze only the attached simulated dataset.

Do not browse, build a workflow, create an app, schedule a task,
connect external services, or perform external actions.

Use the business-impact rules in the file context.

Produce in Thai:
1. One triage table with exactly one row per Request ID:
   ID, Department, Summary, HIGH/MEDIUM/LOW, Reason,
   Recommended Action, Human Review, Missing Information.
2. For each HIGH row only, one concise DRAFT Situation & Follow-up Report:
   Request ID, Situation, Evidence-based Impact, Why HIGH,
   Immediate Attention, Follow-up Items, Missing Information,
   Human Review. Unknown owner = Manager to assign.
   Unknown time = Manager to confirm. Status = OPEN.
3. One HIGH Follow-up Index.

Validate row count and ensure HIGH report count equals HIGH row count.
Do not treat urgent words alone as HIGH. Do not invent missing facts.
```

## Boundary Correction Prompt

```text
Stop the proposed external or automation work.

Return to the original bounded task.

Do not create a workflow, app, integration, scheduled task,
webhook, email, message, or external action.

Use only the attached simulated dataset.

Complete only:
1. Request Triage
2. DRAFT HIGH Priority Situation & Follow-up Reports
3. HIGH Follow-up Index
4. Validation Summary
```

## Validation Prompt

```text
Validate the existing deliverables without starting a new analysis.

Check:
- input record count versus triage row count;
- duplicate or missing Request IDs;
- priorities outside HIGH, MEDIUM, LOW;
- whether urgent words were incorrectly used as the only reason for HIGH;
- HIGH + MEDIUM + LOW versus total;
- HIGH report count versus HIGH triage row count;
- missing or duplicate HIGH reports;
- any HIGH report created for a MEDIUM or LOW row;
- claims without source evidence;
- invented root cause, amount, owner, deadline, SLA, or resolution;
- missing DRAFT/Human Review labels;
- follow-up status other than OPEN/PENDING VALIDATION;
- any statement that implies an external action was performed.

Return only:
1. Validation findings
2. Corrected rows or report sections, if needed
3. Final pass/fail summary

Respond in Thai.
```

## Reflection Prompt — Do Not Run in Manus

ทีมตอบด้วยตนเองเพื่อไม่เพิ่ม credits:

```text
Which parts of triage and HIGH-report creation were planned by humans?
Which parts were planned by the agent?
What evidence supports each HIGH decision?
How would a deterministic workflow create and track the same reports?
What must remain under human approval?
```

---

[← Lab 4 Guide](README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)
