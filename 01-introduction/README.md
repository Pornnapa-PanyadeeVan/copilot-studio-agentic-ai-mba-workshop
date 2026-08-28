# 01 — Introduction: Generative AI → AI Agent → Agentic AI

[← Home](../README.md) · [Next: Lab 1 →](../02-build-ai-agent/README.md)

🎯 **Goal**  เข้าใจองค์ประกอบของ Agentic AI, autonomy spectrum และกรณีศึกษา Business Request Management

⏱ **Estimated Time**  20 นาที

📖 **Reference**  [คำศัพท์พื้นฐาน Agentic AI: Agent, Skill, Tool, Connector, Workflow และ Guardrail](glossary.md)

## Learning Path

```text
Generative AI → AI Agent → Agent + Rules → Workflow → Decision → Action
→ Data / Memory → Management Report → Insight → Human Decision → Agentic AI
```

## คำศัพท์หลัก 6 คำ

| คำศัพท์ | หน้าที่ในระบบ | เปรียบเทียบกับองค์กร |
|---|---|---|
| **Agent** | ทำงานสู่ Goal และตัดสินใจว่าจะทำอะไรต่อ | ผู้รับผิดชอบงาน |
| **Skill** | วิธีทำงานหรือ Playbook ที่นำกลับมาใช้ซ้ำ | SOP |
| **Tool** | ความสามารถที่ใช้ทำงานหนึ่งอย่าง | เครื่องมือทำงาน |
| **Connector** | เชื่อมระบบพร้อม authentication และ permission | ประตูพร้อมบัตรผ่าน |
| **Workflow** | ประสานลำดับ Trigger → Decision → Action | Process map |
| **Guardrail** | จำกัด ตรวจ อนุมัติ หยุด และเก็บหลักฐาน | Policy + Control |

> **Agent decides. Skill guides. Tool does. Connector grants access. Workflow coordinates. Guardrail limits and checks.**

ดูนิยาม ตัวอย่าง และ Quick Check เพิ่มเติมใน [Glossary](glossary.md)

## Timebox

| นาที | เนื้อหา |
|---:|---|
| 0–4 | Generative AI → AI Agent → Agentic AI |
| 4–9 | Agent, Skill, Tool, Connector, Workflow, Guardrail |
| 9–14 | Autonomy Spectrum และ Make vs Manus |
| 14–18 | Business Request Management + Managerial AI |
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

## 2. AI Agent คืออะไร

AI Agent (ตัวแทน AI ที่ทำงานสู่เป้าหมาย) มี Goal, Instructions, Context และ Reasoning เพื่อเลือกคำตอบหรือข้อเสนอแนะที่สอดคล้องกับเป้าหมาย

```text
Goal
↓
Observe Input
↓
Apply Instructions and Rules
↓
Reason
↓
Decide
↓
Recommend
```

ใน Workshop นี้ Agent จะวิเคราะห์คำร้อง จัด Priority และแนะนำการดำเนินการ แต่ใน Lab 1 ยังไม่สั่งระบบอื่น

## 3. Agent + Tools

Tool (เครื่องมือที่ Agent หรือ Workflow เรียกใช้) ทำให้ผลวิเคราะห์เชื่อมไปยังระบบจริง เช่น:

- Google Sheets เพื่อเก็บ Request History
- Gmail เพื่อส่ง Alert/Report
- Google Drive เพื่อเก็บ PDF
- LINE OA เพื่อรับข้อความจากช่องทางลูกค้า

ความสามารถใช้ Tool เพิ่มประโยชน์และเพิ่มความเสี่ยง จึงต้องจำกัด permission และกำหนด approval

## 4. Workflow, Decision และ Action

| องค์ประกอบ | คำถามธุรกิจ | ตัวอย่าง |
|---|---|---|
| Trigger (เหตุการณ์เริ่มต้น) | งานเริ่มเมื่อใด | มีคำร้องใหม่ |
| Workflow (ลำดับกระบวนการ) | ขั้นตอนเชื่อมกันอย่างไร | รับ → วิเคราะห์ → route → เก็บ |
| Decision (การตัดสินใจ) | อะไรกำหนดขั้นตอนถัดไป | Priority = HIGH |
| Action (การลงมือทำ) | ระบบทำอะไรจริง | เพิ่มแถวและส่ง alert |
| Data / Memory | ระบบจำอะไรไว้ | Request Log |
| Feedback | รู้ได้อย่างไรว่าผลดี | Manager ตรวจและแก้ classification |

> Automation ที่ทำ `ถ้า field = X ให้ส่ง email` ตามกฎคงที่ อาจเป็น Workflow Automation แต่ยังไม่จำเป็นต้องเป็น Agentic AI

## 5. Agentic AI คืออะไร

Agentic AI ผสาน:

```text
Goal + Reasoning + Tools + Decision + Action
+ Workflow + Data + Feedback + Human Oversight
```

เพื่อบรรลุ Business Goal ไม่ใช่เพียงสร้างข้อความ

> **Agentic AI is not a product name. It is a way of designing AI-enabled business systems.**

## 6. Autonomy Spectrum

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

## 7. Business Request Management

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

## 8. Operational AI กับ Managerial AI

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
- [ ] แยก Agent, Skill, Tool, Connector, Workflow และ Guardrail ได้
- [ ] ยกตัวอย่าง Decision และ Action อย่างละหนึ่งตัวอย่าง
- [ ] อธิบายว่า autonomy เป็น spectrum ได้
- [ ] แยก Operational AI กับ Managerial AI ได้

## 🏁 Completed

พร้อมเปลี่ยน Prompt ธรรมดาให้เป็น Business Request Agent ใน Google AI Studio

---

[← Home](../README.md) · [Next: Lab 1 →](../02-build-ai-agent/README.md)
