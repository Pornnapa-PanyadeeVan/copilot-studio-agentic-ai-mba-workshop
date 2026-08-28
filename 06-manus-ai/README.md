# 06 — Lab 4: Manus AI — Solve Lab 2 + Lab 3 without Building a Workflow

[← Previous: LINE OA Demo](../05-line-oa-demo/README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)

🎯 **Goal**  ให้ Manus Agent triage dataset แล้วสร้าง DRAFT Situation & Follow-up Report สำหรับทุก HIGH case แบบ end-to-end โดยผู้เรียนไม่ประกอบ Workflow ทีละ module

⏱ **Estimated Time**  30 นาที

👥 **Team**  3–4 คน ใช้หนึ่ง Manus task ต่อทีมเพื่อลด credits และ queue

🧰 **Tool**  [Manus](https://manus.im/) Free plan / Agent Mode Lite เท่าที่บัญชีเปิดให้

## สิ่งที่ Lab นี้ทำ — และไม่ทำ

### Manus ทำใน task เดียว

```text
Read Dataset
↓
Understand Goal and Rules
↓
Plan the Work
↓
Classify Requests
↓
Validate Counts
↓
Select HIGH Cases
↓
Create HIGH Situation Reports + Follow-up Index
↓
Human Review
```

### Lab นี้ไม่ทำ

- ไม่สร้าง Make Scenario หรือ Workflow diagram
- ไม่สร้าง automation, scheduled task, app หรือ integration
- ไม่เชื่อม Google Sheets, Drive, Gmail หรือ LINE
- ไม่ส่ง email, alert หรือข้อความจริง
- ไม่แก้ข้อมูลภายนอก
- ไม่ใช้ข้อมูลจริงหรือ confidential data

> จุดประสงค์คือเปรียบเทียบ **Human-designed Workflow** กับ **Goal-based Agent execution** ไม่ใช่พิสูจน์ว่าเครื่องมือหนึ่งดีกว่าอีกเครื่องมือในทุกกรณี

### Skill, Connector และ Guardrail ใน Lab 4

- ไม่ต้องสร้าง Manus **Skill**: Prompt + business rules + dataset ทำหน้าที่เป็น bounded task instructions ก่อน หากใช้ซ้ำในองค์กรจึงค่อยจัด playbook ที่ผ่านการทดสอบเป็น Skill
- ไม่ใช้ **Connector**: Agent อ่านเฉพาะไฟล์แนบและสร้าง artifacts ใน workspace ไม่เชื่อม Sheet, Gmail, LINE หรือระบบภายนอก
- ไม่ติดตั้ง **MCP Server**: Lab นี้ไม่ต้องเปิด Tools/Resources จากระบบภายนอกผ่าน MCP
- มี **Guardrails** หลายชั้น: ข้อมูลจำลอง, ห้าม browse, ห้าม external action, allowed priorities, HIGH-report count validation, DRAFT labels และ Human Review

คำว่า Skill อาจมีชื่อและรูปแบบต่างกันในแต่ละแพลตฟอร์ม ดูนิยามกลางที่ [Skill](../01-introduction/glossary.md#skill), [Connector](../01-introduction/glossary.md#connector), [MCP](../01-introduction/glossary.md#mcp-model-context-protocol) และ [Guardrail](../01-introduction/glossary.md#guardrail)

## เปรียบเทียบโจทย์เดิม

| Lab 2–3: Make + Gemini | Lab 4: Manus Agent |
|---|---|
| ผู้เรียนกำหนด Trigger, AI step, parser, Router และ Actions | ผู้เรียนกำหนด Goal, Rules, Input, Constraints และ Deliverables |
| เส้นทางถูกออกแบบล่วงหน้า | Agent วางแผนลำดับงานภายใน task |
| เหมาะกับงานซ้ำและ integration ที่ต้องคาดการณ์ได้ | เหมาะกับงานวิเคราะห์หลายขั้นและ deliverable แบบ one-off/bounded |
| ทำ Action จริงกับ Sheet/Drive/Gmail | Lab นี้สร้าง artifacts เท่านั้น ไม่ทำ external action |
| Audit ผ่าน module/run history | Audit ผ่าน task steps, source records และ artifacts |

## Free-plan Guardrail

Manus ระบุว่า Agent Mode ใช้ credits ตาม LLM tokens, virtual-machine resources, third-party APIs, ความซับซ้อน และระยะเวลาของ task ส่วน Free plan/model access/queue เปลี่ยนได้ ตรวจ [Pricing](https://manus.im/pricing) และ [Credit Rules](https://help.manus.im/en/articles/11711097-what-are-the-rules-for-credits-consumption-and-how-can-i-obtain-them) ก่อนสอน

- ใช้ Agent Mode Lite ที่บัญชี Free แสดง
- หนึ่ง task ต่อทีม ไม่ run ซ้ำโดยไม่จำเป็น
- ใช้ dataset 4 records เดียวกับ Lab 2 และห้าม external research
- ไม่กด paid upgrade เพื่อผ่าน Workshop
- หาก credits/queue ไม่พอ ใช้ [Fallback](#fallback) ทันที

> **UI MAY VARY:** Mode names, upload control, task plan, artifact panel และ credit display อาจเปลี่ยน ให้หา function ที่เริ่ม Agent task และแนบไฟล์ตาม UI ปัจจุบัน อย่าคาดเดาชื่อเมนูที่มองไม่เห็น

## Timebox

| นาที | งาน |
|---:|---|
| 0–5 | เปรียบเทียบ Make Workflow กับ Manus Agent |
| 5–9 | เปิด Agent Mode และตรวจ credits |
| 9–12 | Upload dataset และตรวจขอบเขต |
| 12–20 | Run bounded task |
| 20–25 | Validate Request Triage |
| 25–28 | Validate HIGH Reports + Follow-up Index |
| 28–30 | Compare, discuss และเลือก architecture |

## ก่อนเริ่ม

- [ ] รวมทีม 3–4 คนและเลือกหนึ่งคนเป็น Operator
- [ ] Operator เข้า Manus ได้และเห็น Agent Mode ที่ Free plan อนุญาต
- [ ] ดาวน์โหลด/เปิด [Manus Lab Input](../templates/manus-lab-input.md)
- [ ] เปิด [Lab 4 Prompts](prompts.md)
- [ ] ตกลงว่าจะ run เพียงหนึ่ง task
- [ ] ยืนยันว่า dataset เป็นข้อมูลจำลองและไม่มี expected priority ให้ Agent ลอก

## 📌 Step 1 — Frame the Business Goal

ก่อนเปิด Manus ให้ทีมเขียน Goal หนึ่งประโยค:

```text
ช่วยผู้จัดการจัดลำดับคำร้องทางธุรกิจอย่างสม่ำเสมอ
และสร้างร่างรายงานสถานการณ์พร้อมรายการติดตามสำหรับทุก HIGH case
โดยไม่ทำ external action และยังคง Human Review ก่อนมอบหมายหรือดำเนินการ
```

💡 **Why This Matters**  Workflow เริ่มจาก Trigger แต่ Agent task เริ่มจาก Goal + constraints + deliverables หาก Goal คลุมเครือ Agent อาจทำงานมากเกินหรือนอกขอบเขต

✅ **Checkpoint**  Goal ระบุ stakeholder, outcome และ Human Review

## 📌 Step 2 — Open Manus Agent Mode

1. เปิด [Manus](https://manus.im/)
2. Sign in ด้วยบัญชี Operator
3. เลือก Agent Mode Lite หรือ agent mode ที่ Free plan แสดง
4. ตรวจ credit/usage notice ก่อน run
5. อย่าเปิด Max/paid mode เพื่อทำ Lab

💡 **Why This Matters**  Chat Mode อาจตอบคำถามได้ แต่ Lab ต้องการสังเกต Agent ที่วางแผนและทำ multi-step task พร้อม artifacts

✅ **Checkpoint**  ทีมเห็นพื้นที่เริ่ม Agent task และทราบ credit balance/ข้อจำกัดที่หน้า UI แสดง

⚠️ **Common Problem**  หากมีเฉพาะ Chat Mode หรือ Agent queue ยาว ให้ข้ามไป [Fallback](#fallback) ไม่ต้องซื้อ credits

## 📌 Step 3 — Upload the Dataset

แนบไฟล์:

```text
templates/manus-lab-input.md
```

ไฟล์มี 4 คำร้องจำลองชุดเดียวกับ Lab 2: HIGH, MEDIUM, LOW และ anti-keyword โดยไม่มี Expected Priority

หลัง upload ถาม Manus หรือดู file preview ว่าอ่านได้ 4 records หรือไม่ แต่อย่าเริ่ม task แยกเพื่อประหยัด credits หาก UI แสดง preview ได้อยู่แล้ว

💡 **Why This Matters**  ใช้ evidence เดียวกับโจทย์ Lab 2–3 ทำให้เปรียบเทียบวิธี orchestration ได้ยุติธรรม

✅ **Checkpoint**  File name ถูกต้อง จำนวน records = 4 และไม่มีข้อมูลจริง

## 📌 Step 4 — Run One Bounded Agent Task

ใช้ Prompt ฉบับเต็มจาก [prompts.md](prompts.md#primary-agent-task-prompt)

### 📋 Copy This Prompt

```text
You are a Business Request Management Agent.

Your goal is to analyze the attached simulated business-request dataset,
prioritize each request using business-impact rules,
and create a draft Situation & Follow-up Report for every HIGH request.

This is a bounded analysis and artifact-creation task.

Do NOT create a workflow, automation, Make scenario, scheduled task,
application, integration, webhook, email, message, or external action.

Do NOT browse the web or use external sources.
Use only the attached file.

First, present a concise execution plan with no more than 5 steps.
Then execute the plan.

For each request:
1. Preserve the Request ID.
2. Summarize it in one concise Thai sentence.
3. Classify priority as exactly HIGH, MEDIUM, or LOW.
4. Explain the business-impact reason briefly.
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
- Create exactly one DRAFT report for every HIGH Request ID.
- Do not create reports for MEDIUM or LOW requests.
- Use a separate artifact per HIGH case when supported;
  otherwise use clearly separated sections in one artifact.
- Include: DRAFT/Human Review banner, Request ID, Situation Overview,
  evidence-based impact, Why HIGH, Immediate Attention,
  Follow-up table, Decisions/Approvals, Missing Information,
  and Human Review Sign-off.
- Follow-up table columns:
  Item | Proposed Owner | Target Time | Status | Evidence/Source
- Unknown owner = Manager to assign.
- Unknown time = Manager to confirm.
- Status = OPEN or PENDING VALIDATION; never RESOLVED.
- Do not invent facts, amounts, root causes, owners, deadlines, SLAs,
  policies, actions already taken, or resolution status.
- Use "ไม่พบในข้อมูลต้นทาง" for unsupported information.

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
- HIGH report count equals the number of HIGH triage rows;
- every HIGH Request ID has exactly one report and one index row;
- no MEDIUM or LOW Request ID has a HIGH report;
- every report claim is supported by its source record;
- no external action was performed.

End with a short Validation Summary.
```

### ขณะ Agent ทำงาน

สังเกตโดยไม่ขอ hidden chain-of-thought:

- Agent แสดง execution plan หรือไม่?
- อ่านไฟล์และแบ่งงานอย่างไร?
- มีการสร้าง artifact/structured output หรือไม่?
- มีจุดใดที่ขอ clarification?
- Credits/เวลาที่ใช้สะท้อนความซับซ้อนอย่างไร?

💡 **Why This Matters**  Agentic behavior อยู่ที่การรับ Goal, วางแผนหลายขั้น, ใช้ file/tool ภายในขอบเขต, ตรวจผล และส่ง deliverables ไม่ได้อยู่ที่คำว่า “AI Agent” บนหน้าจอเพียงอย่างเดียว

✅ **Checkpoint**  Task เริ่มจาก plan และยังอยู่ในขอบเขต analysis-only

⚠️ **Common Problem**  หาก Agent เสนอสร้าง app/workflow หรือค้นเว็บ ให้หยุด/redirect ด้วย [Boundary Correction Prompt](prompts.md#boundary-correction-prompt)

## 📌 Step 5 — Validate Request Triage

ห้ามเชื่อผลเพียงเพราะตารางดูสวย ตรวจ:

### 🧪 Test

- [ ] มี 4 rows และ Request IDs ไม่หาย/ซ้ำ
- [ ] Priority มีเพียง `HIGH`, `MEDIUM`, `LOW`
- [ ] คำว่า urgent/ASAP ไม่ทำให้ HIGH โดยอัตโนมัติ
- [ ] Payment/system outage cases อ้าง customer/revenue/operations impact
- [ ] กรณีข้อมูลไม่พอมี `Human Review = YES` และ Missing Information
- [ ] Recommended Action เป็นข้อเสนอ ไม่ใช่คำกล่าวว่าได้ทำ Action แล้ว

ใช้ [Validation Prompt](prompts.md#validation-prompt) เฉพาะเมื่อผลไม่ครบและ credits ยังเพียงพอ หรือให้ทีมตรวจด้วยมือเพื่อไม่ run เพิ่ม

💡 **Why This Matters**  Agent autonomy ไม่ลดความจำเป็นของ business validation แต่ย้ายบทบาทคนจาก “ประกอบทุก step” ไปเป็น “กำหนดขอบเขตและตรวจ deliverable”

✅ **Checkpoint**  ทีมระบุอย่างน้อยหนึ่ง decision ที่เห็นด้วยและหนึ่ง decision ที่ต้องทบทวน

## 📌 Step 6 — Validate HIGH Reports and Follow-up Index

### 🧪 Test

- [ ] Total Requests = 4
- [ ] `HIGH + MEDIUM + LOW = 4`
- [ ] ตาม Business Rules มี HIGH report สำหรับ `BR-001` เพียงรายการเดียว
- [ ] จำนวน HIGH reports เท่ากับจำนวน HIGH rows ใน triage
- [ ] HIGH Request ID แต่ละรายการมี report และ index row อย่างละหนึ่ง
- [ ] ไม่มี MEDIUM/LOW request ถูกสร้างเป็น HIGH report
- [ ] ทุก report มี DRAFT/Human Review banner และ source Request ID
- [ ] ทุก impact claim มี source evidence; ช่องที่ขาดใช้ `ไม่พบในข้อมูลต้นทาง`
- [ ] Unknown owner/time ใช้ `Manager to assign` / `Manager to confirm`
- [ ] Follow-up Status เป็น `OPEN` หรือ `PENDING VALIDATION` ไม่ใช่ `RESOLVED`
- [ ] ไม่มีข้อความที่อ้างว่าได้ทำ external action แล้ว

💡 **Why This Matters**  นี่คือโจทย์ Lab 3 ในรูปแบบ Agent task: Agent สร้าง follow-up artifacts ให้ทุก HIGH case โดยไม่ประกอบ report workflow แต่ Human ยังต้องยืนยันข้อเท็จจริง owner และ target time

✅ **Checkpoint**  Manager สามารถย้อนจาก report และ follow-up index ไปยัง HIGH source record ทุกกรณีได้

## 📌 Step 7 — Compare Architecture

ให้ทีมเติมตาราง:

| Criteria | Make Workflow — Lab 2+3 | Manus Agent — Lab 4 |
|---|---|---|
| ใครกำหนดลำดับขั้น | | |
| Setup effort | | |
| Repeatability | | |
| Control/predictability | | |
| Handling ambiguous cases | | |
| External actions | | |
| Audit evidence | | |
| Failure mode | | |
| Cost/quota risk | | |
| Best-fit business work | | |

### 💬 Discussion

1. ถ้าต้องประมวลผลคำร้องทุก 5 นาที ควรใช้ Make หรือ Manus task?
2. ถ้าต้อง triage dataset one-off และสร้าง report ให้ HIGH cases ควรใช้แบบใด?
3. Manus ทำ “งานมากกว่าในคำสั่งเดียว” แต่เราควบคุมและ audit ได้เท่ากับ Workflow หรือไม่?
4. ถ้า Manus สร้าง HIGH reports ได้โดยไม่ทำ external action ระบบนี้เป็น Agentic AI หรือไม่? เพราะอะไร?
5. Architecture แบบ hybrid จะใช้ Manus กับ Make ร่วมกันอย่างไรโดยไม่เพิ่ม risk เกินจำเป็น?

## Fallback

### Fallback A — Instructor Agent Run

ผู้สอนเปิด task ที่ทำสำเร็จล่วงหน้า ให้ผู้เรียนตรวจ plan, triage, HIGH reports, follow-up index และ validation โดยไม่ใช้ credits ของผู้เรียน

### Fallback B — Chat Mode Comparison

หาก Agent Mode unavailable ให้ใช้ Prompt เดียวใน Chat Mode แล้วเปรียบเทียบ:

- ได้คำตอบหรือ artifact อะไร?
- มี multi-step execution/validation evidence หรือไม่?
- เหตุใด Chat response จึงไม่เท่ากับ Agent task โดยอัตโนมัติ?

### Fallback C — Manual Team Simulation

ทีมแบ่งบทบาท Planner, Triage Analyst, HIGH Report Analyst และ Reviewer แล้วทำตาม 5-step plan บน sample data จากนั้นเปรียบเทียบกับ Make

> Fallback ต้องรักษา Learning Objective เรื่อง orchestration choice ไม่จำเป็นต้องซื้อ credits

## 🏁 Completed

- [ ] ระบุความต่างระหว่าง Workflow กับ Goal-based Agent ได้
- [ ] Upload dataset จำลอง 4 records
- [ ] Run หนึ่ง bounded Agent task หรือใช้ Instructor fallback
- [ ] ตรวจ Request Triage, HIGH Situation Reports และ Follow-up Index
- [ ] ยืนยันว่าไม่มี Workflow หรือ external action ถูกสร้าง
- [ ] เติม architecture comparison
- [ ] เลือกได้ว่า use case ใดเหมาะกับ Make, Manus หรือ Hybrid

---

[← Previous: LINE OA Demo](../05-line-oa-demo/README.md) · [Home](../README.md) · [Next: Responsible AI →](../07-responsible-agentic-ai/README.md)
