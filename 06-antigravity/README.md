# 06 — Lab 4: Google Antigravity — Solve Lab 2 + Lab 3 without Building a Workflow

[← Previous: LINE OA Demo](../05-line-oa-demo/README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)

🎯 **Goal**  ให้ Google Antigravity รับ Goal และไฟล์คำร้องจำลอง วางแผนเอง แล้วสร้าง Request Triage กับ DRAFT Situation & Follow-up Report สำหรับทุก HIGH case โดยผู้เรียนไม่ประกอบ Make Workflow ทีละ module

⏱ **Estimated Time**  30 นาที

👥 **Team**  3–4 คน ใช้หนึ่ง local project และหนึ่ง conversation ต่อทีม

🧰 **Tool**  [Google Antigravity 2.0](https://antigravity.google/) แบบ standalone desktop; Antigravity IDE/CLI/SDK ไม่จำเป็นสำหรับ Lab นี้

ผู้เรียนไม่ต้องเขียน code เอง Core lab ใช้ conversation, project settings, plan review และ file artifacts

## Antigravity ใน Lab นี้เป็น Agentic AI แบบใด

Lab นี้ใช้ **Bounded Goal-based Workspace Agent for Analysis and Artifact Creation** หรือ Agent แบบรับเป้าหมายที่ทำงานหลายขั้นภายใน project scope ที่จำกัด

```text
Human defines Goal + Rules + Project Boundary
↓
Antigravity creates Plan + Task List
↓
Human reviews and presses Proceed
↓
Agent reads local dataset → reasons → decides → writes files
↓
Agent validates deliverables and creates Walkthrough
↓
Human reviews evidence and accepts/rejects changes
```

ระดับ autonomy เป็น **ปานกลางและมีขอบเขตชัดเจน**: Agent เลือกลำดับการทำงานและใช้ local file tools เอง แต่คนกำหนด input, allowed outputs, permissions, approval gate และ acceptance criteria

## สิ่งที่ Lab นี้ทำ — และไม่ทำ

### Agent ทำภายใน project เดียว

- อ่านคำร้องจำลอง 4 รายการจากไฟล์ local
- สร้าง implementation plan และ task list
- รอ Human Review ก่อนแก้หรือสร้างไฟล์
- จัด Priority ตาม business impact
- สร้าง report เฉพาะ HIGH cases
- สร้าง follow-up index และ validation summary
- สรุปสิ่งที่ทำใน walkthrough/artifacts

### Lab นี้ไม่ทำ

- ไม่สร้าง Make Scenario, automation หรือ application
- ไม่เปิด browser, web research หรือ URL ภายนอก
- ไม่ใช้ scheduled task หรือ background automation
- ไม่เชื่อม Google Sheets, Drive, Gmail, LINE หรือ production system
- ไม่เปิด Connector หรือ MCP Server
- ไม่ติดตั้ง package และไม่ใช้ paid-only multi-agent/teamwork feature
- ไม่ส่ง email, alert, message หรือเปลี่ยนข้อมูลภายนอก
- ไม่ใช้ข้อมูลจริงหรือ confidential data

> จุดประสงค์คือเปรียบเทียบ **Human-designed deterministic Workflow** กับ **Agent-planned bounded execution** ไม่ใช่ให้ Agent แทน Workflow ในทุกสถานการณ์

## Agent, Tool, Skill, Connector, MCP และ Guardrail

| แนวคิด | ใช้อย่างไรใน Lab 4 |
|---|---|
| Agent | Antigravity รับ Goal วาง plan ตัดสิน Priority สร้างและตรวจ artifacts |
| Tool | อ่าน/เขียนไฟล์ภายใน project; ใช้ local terminal เฉพาะเมื่อผู้ใช้อนุมัติและจำเป็นต่อ PDF |
| Skill | Core lab ไม่สร้าง Skill; Prompt + rules + dataset เป็น task specification ก่อน |
| Connector | ไม่ใช้ เพราะไม่มีการเชื่อม application/account ภายนอก |
| MCP | ปิด/ไม่เพิ่ม MCP Server หรือ MCP Tool ใน project นี้ |
| Guardrail | Project scope, Review-driven approval, simulated data, output allowlist, no web/external action, validation และ Human Review |

หากองค์กรทำงานนี้ซ้ำ จึงค่อยเปลี่ยน rules/checklist ที่ผ่านการทดสอบเป็น workspace **Skill**; การทำเป็น Skill ไม่ได้อนุญาตให้เปิด Connector หรือ MCP โดยอัตโนมัติ

ดูนิยามกลางที่ [Skill](../01-introduction/glossary.md#skill), [Connector](../01-introduction/glossary.md#connector), [MCP](../01-introduction/glossary.md#mcp-model-context-protocol) และ [Guardrail](../01-introduction/glossary.md#guardrail)

## เปรียบเทียบโจทย์เดียวกัน

| Lab 2–3: Make + Gemini | Lab 4: Antigravity |
|---|---|
| ผู้เรียนกำหนด Form, Trigger, AI step, Parser, Router และ Actions | ผู้เรียนกำหนด Goal, Project Boundary, Rules, Inputs และ Deliverables |
| เส้นทางถูกออกแบบล่วงหน้าและทำซ้ำได้ | Agent สร้าง plan/task list และเลือกวิธีทำภายในขอบเขต |
| ทำ Action กับ Sheet/Drive/Gmail ตาม module ที่กำหนด | Core lab สร้างไฟล์ local เท่านั้น |
| เหมาะกับ event-driven recurring process | เหมาะกับ bounded one-off analysis และ artifact creation |
| Audit ผ่าน run history, mappings และ route | Audit ผ่าน plan, task list, file changes, source IDs, validation และ walkthrough |

## Free-plan และ Installation Guardrail

Antigravity มี individual tier ราคา $0 พร้อม basic weekly rate limits แต่ model/limits และ UI เปลี่ยนได้ ตรวจ [Pricing](https://antigravity.google/pricing), [Download](https://antigravity.google/download), [Docs](https://antigravity.google/docs/home) และ [Official Getting Started Codelab](https://codelabs.developers.google.com/getting-started-google-antigravity) ก่อนสอน

- ติดตั้ง Antigravity 2.0 ล่วงหน้า ไม่ใช้เวลาห้องเรียน download พร้อมกัน 50 คน
- ใช้หนึ่งเครื่อง/หนึ่ง project/หนึ่ง conversation ต่อทีม
- ใช้ model ที่ individual tier เปิดให้และไม่ซื้อ plan เพื่อผ่าน Workshop
- ไม่เปิด multi-agent teamwork, subagents, browser หรือ schedule
- หาก quota, installation หรือ account ไม่พร้อม ใช้ [Fallback](#fallback) ทันที

> **UI MAY VARY:** ชื่อ Security Preset, Agent Behaviour, Review Policy, Project Settings, Artifacts และ Proceed/Review controls อาจเปลี่ยน ให้เลือก function ที่จำกัด project และให้คน review ก่อน execution ตาม UI ที่เห็นจริง

## Timebox

| นาที | งาน |
|---:|---|
| 0–4 | เปรียบเทียบ Make Workflow กับ Antigravity Agent |
| 4–8 | เตรียม local project folder และ dataset |
| 8–13 | เปิด Antigravity สร้าง Project และตั้ง Guardrails |
| 13–18 | ส่ง bounded task และ review plan |
| 18–24 | Agent สร้าง artifacts ภายใน project |
| 24–28 | Validate triage, HIGH report และ files |
| 28–30 | Compare architecture และสรุป |

## ก่อนเริ่ม

- [ ] รวมทีม 3–4 คนและเลือก Operator หนึ่งคน
- [ ] ติดตั้ง Antigravity 2.0 และ Sign in เรียบร้อยก่อน Workshop
- [ ] ดาวน์โหลด/เปิด [Antigravity Lab Input](../templates/antigravity-lab-input.md)
- [ ] เปิด [Lab 4 Prompts](prompts.md)
- [ ] สร้างโฟลเดอร์ใหม่ที่ไม่มีไฟล์ธุรกิจจริง
- [ ] ยืนยันว่าจะไม่เปิด browser, schedule, MCP, Connector หรือ external action

## 📌 Step 1 — Frame the Business Goal

ให้ทีมเขียน Goal หนึ่งประโยคก่อนเปิด Agent:

```text
ช่วยผู้จัดการจัดลำดับคำร้องทางธุรกิจอย่างสม่ำเสมอ
และสร้างร่างรายงานสถานการณ์พร้อมรายการติดตามสำหรับทุก HIGH case
โดยใช้เฉพาะข้อมูลจำลองใน project และยังคง Human Review
```

💡 **Why This Matters**  Workflow เริ่มจาก Trigger และ route ที่คนออกแบบ ส่วน Workspace Agent เริ่มจาก Goal + context + constraints + acceptance criteria

✅ **Checkpoint**  Goal ระบุ stakeholder, outcome, project boundary และ Human Review

## 📌 Step 2 — Prepare a Dedicated Local Project

1. สร้างโฟลเดอร์ใหม่ชื่อ:

```text
lab4-antigravity-business-triage/
├── input/
└── outputs/
```

2. Copy [antigravity-lab-input.md](../templates/antigravity-lab-input.md) ไปไว้เป็น:

```text
input/business-requests.md
```

3. อย่าวาง repository, Downloads, Desktop ทั้งหมด หรือโฟลเดอร์งานจริงเป็น project scope
4. ตรวจว่า `outputs/` ยังว่าง

💡 **Why This Matters**  Project folder คือ permission boundary และ context boundary ของ Agent ไม่ใช่เพียงที่เก็บไฟล์

✅ **Checkpoint**  Project มี input file หนึ่งไฟล์ จำนวน 4 records และไม่มีข้อมูลจริง

⚠️ **Common Problem**  หากเลือกโฟลเดอร์กว้างเกินไป ให้หยุดและสร้าง dedicated folder ใหม่ก่อนเริ่ม Agent

## 📌 Step 3 — Create a Review-driven Antigravity Project

1. เปิด [Google Antigravity](https://antigravity.google/)
2. เลือก `Select Project` → `New Project` หรือ function เทียบเท่าตาม UI
3. Add เฉพาะโฟลเดอร์ `lab4-antigravity-business-triage`
4. ตั้งชื่อ Project เช่น `MBA Lab 4 — Business Triage`
5. เปิด Project Settings แล้วกำหนด:
   - review/approval ก่อน Agent execute implementation plan;
   - file access เฉพาะ project folder;
   - terminal command ต้องขออนุมัติ;
   - ไม่อนุญาต browser, external URLs, schedule หรือ MCP tools สำหรับ Lab นี้
6. เริ่ม conversation ใหม่ใน project

> Antigravity project สามารถมี settings และ permissions แยกจาก global settings ได้ ผู้เรียนต้องตรวจ project-specific settings ไม่พึ่ง default โดยไม่อ่าน

💡 **Why This Matters**  Guardrail ที่มีผลจริงต้องอยู่ทั้ง Prompt และ Tool/Permission layer

✅ **Checkpoint**  Agent เห็นเฉพาะ dedicated folder และทีมรู้ว่าจุดใดต้องกดอนุมัติ

⚠️ **Common Problem**  หาก UI ไม่มีชื่อ `Review-driven` ให้เลือก preset/policy ที่ต้อง review plan, file changes และ terminal actions มากที่สุดที่บัญชีแสดง

## 📌 Step 4 — Submit the Bounded Goal and Review the Plan

ใช้ [Primary Agent Task Prompt](prompts.md#primary-agent-task-prompt)

### 📋 Copy This Prompt

```text
You are a bounded Business Request Management Agent working inside one local project.

Use only input/business-requests.md.
Do not browse the web, open external URLs, use MCP or connectors,
schedule tasks, send messages, install packages, or modify files outside this project.

First create a concise implementation plan and task list with no more than 5 steps.
Do not create or modify output files until a human approves the plan.

After approval, triage all requests using business impact rather than urgency words.
Create these required deliverables under outputs/:
1. 01-request-triage.md
2. one DRAFT-HIGH-Situation-Report-[Request-ID].md per HIGH case
3. 03-high-follow-up-index.md
4. 04-validation-summary.md

Do not create a HIGH report for MEDIUM or LOW cases.
Do not invent facts, amounts, root causes, owners, deadlines, policies, SLAs,
actions already taken, or resolution status.
Unknown owner = Manager to assign.
Unknown target time = Manager to confirm.
Follow-up status = OPEN or PENDING VALIDATION; never RESOLVED.

Optional: create DRAFT-HIGH-Situation-Report-[Request-ID].pdf only if an
existing local capability can do so without
installing packages. Ask for approval before any terminal command.
Otherwise create DRAFT-HIGH-Situation-Report-[Request-ID].html as a
print-ready fallback and state why PDF was not created.

End by validating file names, row counts, HIGH-report counts, evidence,
and confirming that no external action was performed.
```

เมื่อ Agent แสดง plan/task list:

- ตรวจว่าใช้เฉพาะ `input/business-requests.md`
- ตรวจว่าเขียนเฉพาะ `outputs/`
- ต้องไม่มี app, workflow, browser, schedule, MCP, external action หรือ package install
- ตรวจว่า report count ผูกกับ HIGH count
- ถ้าถูกต้องจึงกด `Proceed` หรือ approve ตาม UI
- ถ้าไม่ถูกต้องให้ comment/edit plan หรือใช้ [Boundary Correction Prompt](prompts.md#boundary-correction-prompt)

💡 **Why This Matters**  Human Approval อยู่ก่อน Tool execution ไม่ใช่ตรวจเฉพาะผลลัพธ์หลัง Agent ทำเสร็จ

✅ **Checkpoint**  Plan ผ่าน review และยังไม่พบการเปลี่ยนไฟล์ก่อน approval

⚠️ **Common Problem**  หาก Agent เริ่มเขียนไฟล์ทันที ให้กด Stop, ปรับ project review policy และเริ่มจาก plan เดิมโดยไม่เพิ่ม permission

## 📌 Step 5 — Observe Agent Execution and Artifacts

ระหว่าง Agent ทำงาน ให้สังเกตเฉพาะ evidence ที่ UI แสดง ไม่ขอ hidden chain-of-thought:

- implementation plan และ task list
- ไฟล์ที่ Agent อ่าน/สร้าง
- permission request สำหรับ terminal หรือ file access
- progress/status ของ tasks
- file diffs หรือ artifact review
- validation result และ walkthrough

อนุมัติเฉพาะ command ที่อ่าน/สร้างไฟล์ใน project และสอดคล้องกับ plan หาก Agent ขอ network, package install, URL, schedule หรือ access นอก project ให้ reject

💡 **Why This Matters**  ความเป็น Agentic อยู่ที่ Goal → Plan → Tool Use → Artifact → Validation ภายในขอบเขต ไม่ได้วัดจากข้อความที่ดูฉลาดเพียงอย่างเดียว

✅ **Checkpoint**  มีไฟล์ใน `outputs/` โดย input file ไม่ถูกแก้และไม่มี external action

## 📌 Step 6 — Validate the Deliverables

### 🧪 Test A — Request Triage

- [ ] `01-request-triage.md` มี 4 rows และ Request IDs ไม่หาย/ซ้ำ
- [ ] Priority มีเพียง `HIGH`, `MEDIUM`, `LOW`
- [ ] `BR-004` ไม่เป็น HIGH เพียงเพราะมี urgent/ASAP
- [ ] Recommended Action เป็นข้อเสนอ ไม่ใช่ Action ที่อ้างว่าทำแล้ว
- [ ] Missing Information และ Human Review แสดงเมื่อเหมาะสม

### 🧪 Test B — HIGH Reports and Index

- [ ] ตาม Business Rules มี HIGH report สำหรับ `BR-001` เพียงรายการเดียว
- [ ] จำนวน HIGH reports เท่ากับจำนวน HIGH rows
- [ ] ไม่มี MEDIUM/LOW Request ID ถูกสร้างเป็น HIGH report
- [ ] Report มี DRAFT/Human Review banner และ source Request ID
- [ ] Impact claims อ้างหลักฐาน; ช่องที่ขาดใช้ `ไม่พบในข้อมูลต้นทาง`
- [ ] Unknown owner/time ใช้ `Manager to assign` / `Manager to confirm`
- [ ] Follow-up Status เป็น `OPEN` หรือ `PENDING VALIDATION` ไม่ใช่ `RESOLVED`
- [ ] `03-high-follow-up-index.md` อ้าง report file ถูกต้อง
- [ ] `04-validation-summary.md` ยืนยัน row count, report count และ no external action

### 🧪 Test C — File and Permission Boundary

- [ ] Input file ไม่ถูกแก้
- [ ] ไม่มีไฟล์นอก `outputs/` ถูกสร้างหรือแก้
- [ ] ไม่มี browser, network, Connector, MCP หรือ schedule execution
- [ ] ไม่มี package ถูกติดตั้ง
- [ ] PDF มีเฉพาะเมื่อทีมอนุมัติ local command; ไม่เช่นนั้นมี Markdown/HTML fallback

ใช้ [Validation Prompt](prompts.md#validation-prompt) เมื่อจำเป็น หรือให้ Reviewer ตรวจด้วยมือเพื่อประหยัด quota

✅ **Checkpoint**  ทีมย้อนจาก HIGH report ไปยัง source Request ID และ evidence ได้ทุก claim

## 📌 Step 7 — Compare Architecture

| Criteria | Make Workflow — Lab 2+3 | Antigravity Agent — Lab 4 |
|---|---|---|
| ใครกำหนดลำดับขั้น | Human ออกแบบ modules/routes | Agent เสนอ plan; Human review |
| Trigger | Google Form/Watch New Rows | Human starts bounded conversation |
| Tool use | Connectors/actions ที่กำหนดล่วงหน้า | Local file tools และ terminal ที่ขออนุมัติ |
| Repeatability | สูงเมื่อ schema/process คงที่ | ขึ้นกับ Goal, context, model และ review |
| External action | Sheet/Drive/Gmail ตาม workflow | ปิดใน core lab |
| Audit evidence | Run history, mappings, routes | Plan, task list, diffs, files, validation, walkthrough |
| Best fit | Recurring event-driven process | One-off multi-step analysis/artifact creation |

### 💬 Discussion

1. ถ้าต้องประมวลผลคำร้องทุก 5 นาที เหตุใด Make จึงเหมาะกว่า Antigravity conversation?
2. ส่วนใดของ Lab 4 แสดง Agentic behavior มากกว่าการใช้ Chatbot?
3. Project scope กับ Prompt prohibition ต่างกันอย่างไรในฐานะ Guardrail?
4. ถ้าเปิด MCP ให้ Agent เขียน Google Sheets ความเสี่ยงและ approval gate ต้องเพิ่มอะไร?
5. Architecture แบบ Hybrid จะให้ Make คุม Trigger/Action และให้ Antigravity ทำ bounded analysis อย่างไร?

## Fallback

### Fallback A — Instructor Completed Project

ผู้สอนเปิด project ที่ทำสำเร็จล่วงหน้า ให้ผู้เรียนตรวจ plan, task list, file changes, triage, HIGH report, follow-up index, validation และ walkthrough โดยไม่ใช้ quota ของผู้เรียน

### Fallback B — Antigravity Plan-only

หาก Agent run หรือ quota ไม่พร้อม ให้ผู้เรียนส่ง Prompt แล้วหยุดหลัง implementation plan จากนั้นตรวจว่า plan ใช้ Tools, Files, Guardrails และ approval gate ถูกต้องหรือไม่

### Fallback C — Chat Comparison

ใช้ Prompt เดียวใน Chat Mode/AI Studio และเปรียบเทียบว่าไม่มี project permission, file change review, task list หรือ walkthrough แบบเดียวกับ Workspace Agent

### Fallback D — Manual Team Simulation

ทีมแบ่งบทบาท Goal Owner, Planner, Triage Analyst, HIGH Report Analyst และ Reviewer แล้วจำลอง plan → approval → files → validation บน dataset เดียวกัน

> Fallback ต้องรักษา Learning Objective เรื่อง Goal-based planning, bounded tool use, artifacts, approval และ validation ไม่จำเป็นต้องบังคับให้ installation สำเร็จในห้อง

## 🏁 Completed

- [ ] สร้าง dedicated Antigravity project แบบ review-driven
- [ ] ใช้ dataset จำลอง 4 records
- [ ] Review plan ก่อน Agent เขียนไฟล์
- [ ] ได้ Request Triage และ HIGH report เฉพาะ `BR-001`
- [ ] ได้ Follow-up Index และ Validation Summary
- [ ] ไม่มี external action, MCP, browser, schedule หรือ package install
- [ ] อธิบายได้ว่า Antigravity ใน Lab นี้คือ bounded goal-based workspace agent
- [ ] เลือกได้ว่า use case ใดเหมาะกับ Make, Antigravity หรือ Hybrid

---

[← Previous: LINE OA Demo](../05-line-oa-demo/README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)
