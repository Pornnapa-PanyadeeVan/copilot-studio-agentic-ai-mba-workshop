# 01 — Introduction: Generative AI → AI Agent → Agentic AI

[← Home](../README.md) · [Next: Lab 1 →](../02-build-ai-agent/README.md)

🎯 **Goal**  เข้าใจองค์ประกอบของ Agentic AI, autonomy spectrum และกรณีศึกษา Business Request Management

⏱ **Estimated Time**  20 นาที

📖 **Reference**  [คำศัพท์พื้นฐาน Agentic AI: Agent, Skill, Tool, Connector, MCP, Workflow และ Guardrail](glossary.md)

## Mental Model: AI Agent → Agentic AI System

```text
Business Goal
↓
AI Agent
├─ Guidance: Instructions + Skill + Business Rules
├─ Context: Input + Data / Memory
└─ Agent Loop: Observe → Reason → Decide
                              ↓
Execution Coordination
├─ Human-designed Workflow
└─ Agent-planned Execution
↓
Capability Access
├─ Local Tool
├─ Tool → Connector / API → External System
└─ MCP Client → MCP Server → Resources / Prompts / Tools
↓
Action / Artifact
↓
Validation → Human Review → Feedback → Data / Memory
                                      ↺ New Context
```

**Guardrails ครอบทุกช่วงของเส้นทาง:** Input rules, instructions, permissions, output validation, approval gates, audit trail และ stop/recovery conditions

> **Agent decides. Skill guides. Tool does. Connector grants access. MCP standardizes access. Workflow coordinates. Guardrail limits and checks.**

ดูนิยามและ Quick Check เพิ่มเติมใน [Glossary](glossary.md)

## Timebox

| นาที | เนื้อหา |
|---:|---|
| 0–4 | Generative AI ต่างจาก AI Agent อย่างไร |
| 4–11 | End-to-end Agentic AI Path และคำศัพท์พื้นฐาน |
| 11–15 | Autonomy Spectrum และ Make vs Manus |
| 15–18 | Business Request Management + Managerial AI |
| 18–20 | Discussion และ Checkpoint |

## 1. Generative AI คืออะไร

Generative AI (AI สำหรับสร้างเนื้อหา) รับ Prompt แล้วสร้างคำตอบ ข้อความ ภาพ หรือเนื้อหาอื่น

```text
Prompt
↓
Generate
↓
Response
```

ตัวอย่าง: “ช่วยสรุปข้อร้องเรียนลูกค้านี้” ระบบตอบเป็นข้อความแล้วหยุด

## 2. AI Agent → Agentic AI: เส้นทางเดียวกัน

**AI Agent คือแกนกลาง** ที่รับ Business Goal ใช้ Guidance และ Context เพื่อ Observe → Reason → Decide จากนั้นอาจหยุดที่ Recommendation หรือทำงานต่อผ่าน Tools

**Agentic AI System คือภาพ end-to-end** ที่เชื่อม Agent core เข้ากับ execution coordination, capability access, actions, data, feedback, human oversight และ guardrails เพื่อบรรลุ Business Goal

| ช่วงใน Path | Component | คำถามธุรกิจ | ตัวอย่าง Workshop |
|---:|---|---|---|
| 1 | Goal | ต้องการผลลัพธ์อะไร | จัดลำดับคำร้องอย่างสม่ำเสมอ |
| 2 | Instructions / Skill / Rules | Agent ควรทำงานอย่างไร | Triage playbook และ Priority rules |
| 3 | Context / Data / Memory | ใช้ข้อมูลอะไร | Request text และ Request History |
| 4 | Reasoning | ประเมินหลักฐานอย่างไร | ตรวจ customer, financial, operational impact |
| 5 | Decision | เลือกอะไรต่อ | `Priority = HIGH` |
| 6 | Workflow หรือ Agent Plan | ใครประสานลำดับ execution | Make Scenario หรือ Manus execution plan |
| 7 | Tool | ต้องใช้ความสามารถอะไร | Parse JSON, `Add a row`, create report |
| 8 | Connector / API / MCP | เข้าถึง capability ภายนอกอย่างไร | Make connection หรือ MCP Server |
| 9 | Action / Artifact | เกิดผลลัพธ์จริงอะไร | บันทึก Sheet, alert หรือ PDF report |
| 10 | Validation / Human Review | ผลถูกต้องและอนุมัติได้หรือไม่ | Count check และ Manager approval |
| 11 | Feedback / Audit / Memory | เรียนรู้และตรวจย้อนหลังอย่างไร | Override reason, run log และ Request History |

Tool ไม่จำเป็นต้องเชื่อมระบบภายนอก เช่น calculator หรือ parser ก็เป็น Tool ได้ เมื่อ Tool ต้องเข้าระบบภายนอก Connector จะจัดการ integration, authentication และ permission ส่วน MCP เป็น protocol ที่ AI application ใช้ค้นพบและเรียก Resources, Prompts หรือ Tools จาก MCP Server

Guardrails ไม่ใช่ขั้นตอนสุดท้าย แต่ครอบทุกช่วงของ Path เช่นห้ามข้อมูลจริง จำกัด allowed values, allowlist tools, ใช้ least privilege, บังคับ Human Approval และกำหนด stop/fallback

ใน Workshop นี้:

- **Lab 1:** Agent core จบที่ Decision + Recommendation
- **Lab 2–3:** Make Workflow ประสาน Agent reasoning, native connectors, actions, data และ report
- **Lab 4:** Manus Agent วางแผน execution และสร้าง artifacts โดยไม่ประกอบ Workflow หรือเชื่อมระบบภายนอก

> Workflow ที่ส่ง email ตามกฎคงที่อาจเป็น Automation แต่ยังไม่จำเป็นต้องเป็น Agentic AI และ Agent ที่ไม่มี Connector/MCP ก็ยังเป็น Agent ได้

> **Agentic AI is not a product name. It is a way of designing AI-enabled business systems.**

## 3. Autonomy Spectrum

Autonomy (ระดับความเป็นอิสระ) ควรมองเป็นสเปกตรัม:

| ระดับ | ระบบทำอะไร | ตัวอย่าง Workshop | Human Role |
|---|---|---|---|
| 0: Manual | คนทำทุกขั้นตอน | อ่านและจัด Priority เอง | ตัดสินใจทั้งหมด |
| 1: Assist | AI สร้างคำแนะนำ | Lab 1 | คนตรวจและลงมือทำ |
| 2: Conditional Action | Workflow ทำ Action ที่ความเสี่ยงต่ำ | Lab 2 บันทึก Sheet | คนตรวจ HIGH |
| 3: Bounded Autonomy | ระบบเลือกและทำหลายขั้นตอนภายในขอบเขต | สร้าง/ส่ง weekly report | คนกำหนด policy และ exception |
| 4: Higher Autonomy | ระบบวางแผนและเลือก tools กว้างขึ้น | Optional agent comparison | ต้องมี guardrails และ monitoring เข้มขึ้น |

“อัตโนมัติมากกว่า” ไม่ได้แปลว่า “ดีกว่า” เสมอไป ระดับที่เหมาะสมขึ้นกับ impact, reversibility, data sensitivity และ accountability

### Preview Lab 4 — Make Workflow vs Manus Agent

Workshop จะให้ผู้เรียนแก้โจทย์ Business Request Management สองวิธี:

| Human-designed Workflow | Goal-based Autonomous Agent |
|---|---|
| คนออกแบบ Trigger, route และ action ทีละขั้น | คนกำหนด Goal แล้ว Agent วางแผนขั้นตอนมากขึ้น |
| เส้นทางคาดการณ์และ audit ง่ายกว่า | ยืดหยุ่นกับงานปลายเปิดมากกว่า |
| เปลี่ยน process ต้องแก้ workflow | Agent อาจปรับแผนตาม context |
| เหมาะกับงานซ้ำและ policy ชัด | เหมาะกับงานสำรวจ/วางแผนที่ขอบเขตชัดและตรวจสอบได้ |

ใน Lab 2–3 ผู้เรียนจะประกอบ Workflow เอง ส่วน Lab 4 จะให้ Manus Agent รับ Goal และ dataset เดียวกันแล้ววางแผนทำ triage กับ management report โดยไม่สร้าง Workflow ผู้เรียนต้องสังเกตว่า “ความเป็นอิสระมากขึ้น” ทำให้ต้องกำหนด boundary, approval, evidence และ validation เพิ่มขึ้นอย่างไร

## 4. Business Request Management

องค์กรได้รับคำร้องจากลูกค้าหรือพนักงาน Agent ต้อง:

```text
Read → Summarize → Classify → Explain → Recommend
```

### Priority Rules

**HIGH**

- กระทบลูกค้าทันที
- กระทบรายได้/การเงินอย่างมีนัยสำคัญ
- ระบบงานสำคัญหยุดชะงัก
- ความเสี่ยง compliance หรือ reputation รุนแรง
- deadline สั้นและหากพลาดจะเกิดผลกระทบธุรกิจสำคัญ

**MEDIUM**

- สำคัญแต่ยังไม่ critical
- ต้องการ management attention
- มี deadline ภายในหลายวัน
- Operations ยังทำต่อได้

**LOW**

- Routine administration
- General information
- ไม่มีผลกระทบทันทีและไม่มี urgent deadline

### Anti-keyword Rule

คำว่า “ด่วน” หรือ “ASAP” เป็นเพียงสัญญาณ ไม่ใช่หลักฐานของผลกระทบ

```text
“ขอวิธีเปลี่ยนรูป Profile ด่วนมาก”
```

ควรเป็น LOW หากไม่มี customer, financial, operational, compliance หรือ time impact ที่สำคัญ

## 5. Operational AI กับ Managerial AI

> **Operational AI:** “What should we do with this request?”

> **Managerial AI:** “What are all these requests telling us about the business?”

เชื่อมกับ Management Information Systems (MIS):

```text
Data → Information → Insight → Decision → Action
```

| ชั้น | ตัวอย่าง |
|---|---|
| Data | คำร้องแต่ละรายการ |
| Information | Summary + Priority |
| Insight | รูปแบบซ้ำ ความเสี่ยง และหน่วยงานที่ต้องสนใจ |
| Decision Support | Management recommendation |
| Action | แก้ process, จัดสรรคน, อนุมัติหรือ escalate |

## 💬 Discussion

1. Chatbot ที่ตอบคำถามแต่ไม่ใช้ Tools เป็น Agentic AI หรือไม่?
2. Workflow ที่ส่ง email ตามเวลาโดยไม่มี AI reasoning เป็น Agentic AI หรือไม่?
3. การจัด Priority ผิดอาจสร้างผลกระทบต่อใครบ้าง?
4. Action ใดควรให้ AI ทำอัตโนมัติ และ Action ใดต้องรอคนอนุมัติ?

## ✅ Checkpoint

- [ ] อธิบาย Generative AI, Agent, Workflow และ Agentic AI ด้วยคำของตนเองได้
- [ ] แยก Agent, Skill, Tool, Connector, MCP, Workflow และ Guardrail ได้
- [ ] ยกตัวอย่าง Decision และ Action อย่างละหนึ่งตัวอย่าง
- [ ] อธิบายว่า autonomy เป็น spectrum ได้
- [ ] แยก Operational AI กับ Managerial AI ได้

## 🏁 Completed

พร้อมเปลี่ยน Prompt ธรรมดาให้เป็น Business Request Agent ใน Google AI Studio

---

[← Home](../README.md) · [Next: Lab 1 →](../02-build-ai-agent/README.md)
