# Build Your First Agentic AI for Business

**From Generative AI to AI Agent, Workflow, Decision, Action, and Management Report**

Workshop เชิงปฏิบัติการ 3 ชั่วโมงสำหรับนักศึกษา MBA เพื่อเข้าใจและออกแบบ **Agentic AI (ระบบ AI ที่ทำงานสู่เป้าหมายผ่านการให้เหตุผล เครื่องมือ การตัดสินใจ และการลงมือทำ)** โดยไม่ต้องเขียนโปรแกรมและไม่พึ่ง Microsoft Copilot Studio

> **Generative AI creates content.**
>
> **AI Agents work toward goals.**
>
> **Agentic AI connects reasoning, decisions, tools, actions, workflows, data, and feedback to accomplish business goals.**

> **Agentic AI is not a product name. It is a way of designing AI-enabled business systems.**

## ภาพรวม Workshop

| รายการ | รายละเอียด |
|---|---|
| กลุ่มเป้าหมาย | นักศึกษา MBA ประมาณ 50 คน ผู้เริ่มต้น ไม่ต้องมีพื้นฐานเขียนโปรแกรม |
| ระยะเวลา | 3 ชั่วโมง รวมพัก 10 นาที |
| รูปแบบ | Hands-on, business-oriented และเรียนตามคู่มือใน repository ได้ด้วยตนเอง |
| กรณีศึกษา | Business Request Management |
| เครื่องมือหลัก | Google AI Studio, Make, Gemini API, Google Workspace และ Manus AI |
| ข้อมูล | ใช้ข้อมูลจำลองเท่านั้น ห้ามใช้ข้อมูลจริงหรือข้อมูลลับ |
| ค่าใช้จ่าย | ออกแบบให้ใช้ free/free-tier; ไม่ต้องเปิด billing หรือซื้อ API credits เพื่อผ่าน Workshop |

## เป้าหมายการเรียนรู้

เมื่อจบ Workshop ผู้เรียนจะสามารถ:

1. แยกความแตกต่างระหว่าง Generative AI, AI Agent, Workflow และ Agentic AI
2. อธิบาย Agent, Skill, Tool, Connector, MCP, Workflow และ Guardrail ด้วยตัวอย่างธุรกิจได้
3. อธิบายว่า autonomy (ระดับความเป็นอิสระ) เป็นสเปกตรัม ไม่ใช่มีหรือไม่มีเพียงสองสถานะ
4. สร้าง `Business Request Assistant` ด้วย System Instructions ใน Google AI Studio
5. ใช้ Business Rules เพื่อจัดลำดับ `HIGH`, `MEDIUM`, `LOW` จากผลกระทบจริง
6. เชื่อม Google Form → Google Sheets → Gemini → Decision Router → Update Row/Alert ใน Make
7. เปลี่ยน Request History ให้เป็น Management Insight และส่งรายงาน PDF
8. ให้ Manus Agent รับ Goal เดียวกับ Lab 2–3 แล้ววางแผน วิเคราะห์ และสร้าง deliverables โดยไม่ประกอบ Workflow
9. เปรียบเทียบ Human-designed Workflow กับ Goal-based Autonomous Agent
10. กำหนด Guardrails, Human-in-the-loop, permission, audit trail และ fallback ที่เหมาะสม

## จาก Generative AI → AI Agent → Agentic AI

### 1. Generative AI

```text
Prompt → Generate → Response
```

สร้างเนื้อหาแล้วหยุด เช่นสรุปข้อความหรือร่างคำตอบ

### 2. AI Agent

```text
Business Goal
↓
Instructions + Skill + Context
↓
Observe → Reason → Decide
↓
Recommend OR Use Tool
```

AI Agent ทำงานสู่ Goal และเลือกสิ่งที่จะเกิดขึ้นถัดไป โดยไม่จำเป็นต้องเชื่อมระบบภายนอกเสมอไป

### 3. Agentic AI

```text
AI Agent
↓
Workflow OR Agent-planned Execution
↓
Capability Access
├─ Tool → Connector / API → External System
└─ MCP → Resources / Prompts / Tools
↓
Action / Artifact → Data / Memory → Feedback
```

Agentic AI เชื่อม Agent เข้ากับ execution, capabilities, actions, data และ feedback ส่วน Guardrails ครอบทุกช่วงตั้งแต่ input และ permissions ไปจนถึง validation, approval, audit และ stop/recovery

> Workflow ตามกฎคงที่อาจเป็น Automation แต่ยังไม่จำเป็นต้องเป็น Agentic AI และ AI Agent ไม่จำเป็นต้องมี Connector หรือ MCP เสมอไป

## สถาปัตยกรรมหลัก

```text
Google Form / Business Request
↓
Google Sheets — Form Response
↓
Make Workflow / Orchestrator
├─ AI Agent / Gemini Reasoning
├─ Priority Decision / Router
├─ Tool + Connector
└─ Action → Update Google Sheets / HIGH Alert
↓
Request History
↓
Management Analysis
↓
PDF Report
↓
Google Drive
↓
Email
↓
Human Decision
```

## สองวิธีแก้โจทย์เดียวกัน

```text
Business Request Data + Business Goal
                 │
        ┌────────┴────────┐
        │                 │
Lab 2–3: Make       Lab 4: Manus Agent
Human designs       Human defines Goal,
every module        Rules and Deliverables
        │                 │
Gemini → Router     Agent plans and executes
→ Sheet → Report    analysis in its workspace
        │                 │
Real Workflow       Triage + Insight + Report
and Actions         without building Workflow
```

Lab 4 ไม่ได้แทน Make ในทุกกรณี แต่ใช้เปรียบเทียบ control, repeatability, autonomy, auditability และ effort ของสองแนวทาง

## ตารางเวลา 3 ชั่วโมง

| เวลา | กิจกรรม | ผลลัพธ์ |
|---|---|---|
| 00:00–00:20 | [Introduction](01-introduction/README.md) | เข้าใจ end-to-end Agentic AI Path และคำศัพท์พื้นฐาน |
| 00:20–00:50 | [Lab 1: AI Agent](02-build-ai-agent/README.md) | Agent วิเคราะห์และจัด Priority |
| 00:50–01:30 | [Lab 2: Agentic Workflow](03-build-agentic-workflow/README.md) | Form → Sheet → AI decision → Update Row/Alert |
| 01:30–01:40 | Break | พัก 10 นาที |
| 01:40–02:05 | [Lab 3: Managerial AI](04-generate-management-report/README.md) | Request History → Insight → PDF/Email |
| 02:05–02:15 | [LINE OA Demo](05-line-oa-demo/README.md) | เห็น Channel → Agentic Workflow |
| 02:15–02:45 | [Lab 4: Manus AI](06-manus-ai/README.md) | ทำโจทย์ Lab 2+3 แบบ Goal-based Agent โดยไม่สร้าง Workflow |
| 02:45–03:00 | [Responsible Agentic AI](07-responsible-agentic-ai/README.md) + Compare + Wrap-up | Human oversight และเลือก architecture ให้เหมาะกับงาน |

กิจกรรมหลังชั้นเรียน: [Optional MBA Agentic AI Challenge](08-optional-mba-challenge/README.md)

## กรณีศึกษาต่อเนื่อง: Business Request Management

องค์กรรับคำร้องจากพนักงานหรือลูกค้า เช่น ปัญหาระบบ คำร้องฝ่ายขาย การเงิน HR หรือข้อร้องเรียนลูกค้า Agent ต้อง:

1. อ่านคำร้อง
2. สรุปหนึ่งประโยค
3. ตัดสิน Priority
4. อธิบายเหตุผล
5. แนะนำ Next Action

### Business Rules

| Priority | เกณฑ์จากผลกระทบจริง |
|---|---|
| HIGH | กระทบลูกค้าทันที รายได้/การเงินอย่างมีนัยสำคัญ ระบบงานหลักหยุดชะงัก ความเสี่ยง compliance/reputation รุนแรง หรือ deadline ที่พลาดแล้วเกิดผลกระทบสำคัญ |
| MEDIUM | สำคัญและต้องให้ผู้บริหารสนใจ มี deadline ภายในหลายวัน แต่ธุรกิจยังดำเนินต่อได้ |
| LOW | งานประจำ ขอข้อมูลทั่วไป ไม่มีผลกระทบทันทีและไม่มี deadline เร่งด่วน |

> ห้ามจัดเป็น `HIGH` เพียงเพราะพบคำว่า “ด่วน”, “ASAP”, “ทันที” หรือ “โดยเร็วที่สุด” ต้องพิจารณา customer, financial, operational, compliance, reputation และ time impact จริง

## สิ่งที่ต้องเตรียม

### ผู้เรียน

- Google Account ที่เข้า Google AI Studio, Forms, Sheets, Drive, Docs และ Gmail ได้
- Make account แบบ Free
- Manus account แบบ Free หนึ่งบัญชีต่อทีมสำหรับ Lab 4 หรือใช้ Instructor run fallback
- Browser รุ่นปัจจุบัน และอินเทอร์เน็ต
- Gemini API key เฉพาะบุคคลสำหรับ Lab 2–3 หากบัญชีสร้างได้
- ไม่ต้องมี API key ใน Lab 1
- ไม่ต้องมีบัตรเครดิตและไม่ต้องเปิด paid tier

### ผู้สอน

- ทดสอบทุก connection ด้วยบัญชีประเภทเดียวกับผู้เรียน
- เตรียม [sample requests](templates/sample-requests.md) และ scenario/report fallback
- จำกัดการทดสอบคนละ 3 คำร้องใน Lab 2 เพื่อลด quota และ credit usage
- ให้ Lab 4 ทำเป็นทีม 3–4 คนและรัน Agent task เพียงหนึ่งครั้งต่อทีม
- ใช้ [Instructor Checklist](templates/instructor-checklist.md) ก่อนสอน

## เครื่องมือ

| เครื่องมือ | ใช้ทำอะไร | หมายเหตุ |
|---|---|---|
| [Google AI Studio](https://aistudio.google.com/) | ทดลอง Prompt และ System Instructions | Lab 1 ใช้โดยไม่ต้องคัดลอก API key |
| [Gemini API](https://ai.google.dev/gemini-api/docs) | วิเคราะห์คำร้องและสร้างรายงานจาก Make | ใช้ key ของผู้เรียน; free tier มี rate limits |
| [Make](https://www.make.com/) | Workflow Orchestrator (ตัวประสานขั้นตอนงาน) | Free plan มี credit/feature limits และอาจเปลี่ยนได้ |
| Google Forms | ช่องทางรับ Business Request ใน Lab 2 | ไม่เก็บ email หากไม่จำเป็น และใช้ข้อมูลจำลอง |
| Google Sheets | Form response log, ผล AI และข้อมูลสะสม | ใช้ข้อมูลจำลอง |
| Google Docs / Drive | สร้างและเก็บรายงาน | Permission ต้องอนุญาตให้ Make ตามที่ใช้จริง |
| Gmail | ส่งรายงานถึงอีเมลของผู้เรียนเอง | ใช้ `[Your Email]` ในคู่มือเสมอ |
| LINE OA | Channel สำหรับ instructor demo | ผู้สอนเตรียมล่วงหน้า; ผู้เรียนไม่ต้องสร้างบัญชี |
| [Manus](https://manus.im/) | Goal-based Agent สำหรับทำ triage + management report โดยไม่ประกอบ Workflow | Lab 4 ใช้ Agent Mode Lite เท่าที่ Free plan/credits เปิดให้ |

## Free-tier และความเป็นส่วนตัว

> **FREE-TIER DISCLAIMER:** Free tier ไม่ได้หมายถึง unlimited จำนวน model, request rate, daily quota, Make credits, interval, connector หรือ eligibility อาจเปลี่ยนตามบัญชี ประเทศ และเวลาที่ใช้งาน ตรวจหน้าราคา/โควตาทางการก่อนสอนเสมอ

- Workshop นี้ไม่บังคับเปิด Cloud Billing หรือซื้อ credits
- หากหน้าจอเสนอ paid upgrade ให้หยุดและใช้ fallback
- Google ระบุว่า free tier อาจใช้ข้อมูลที่ส่งเพื่อปรับปรุงผลิตภัณฑ์ จึงใช้เฉพาะ simulated data
- ห้ามแชร์ API key, ใส่ key ใน screenshot, chat, Sheet หรือ GitHub
- Make นับการทำงานของ module เป็น credits; ทดสอบสั้นและปิด schedule หลังจบ
- Manus Agent Mode ใช้ credits ตามความซับซ้อนและระยะเวลาของ task; Free plan, model access และ queue เปลี่ยนได้ ให้ทำเป็นทีมและเตรียม recorded run
- ดูข้อมูลล่าสุด: [Gemini API Pricing](https://ai.google.dev/gemini-api/docs/pricing), [Gemini Rate Limits](https://ai.google.dev/gemini-api/docs/rate-limits), [Make Pricing](https://www.make.com/en/pricing), [Manus Pricing](https://manus.im/pricing), [Manus Credit Rules](https://help.manus.im/en/articles/11711097-what-are-the-rules-for-credits-consumption-and-how-can-i-obtain-them)

## เริ่ม Workshop

อ่านก่อนหรือเปิดเป็น reference: [คำศัพท์พื้นฐาน Agentic AI — Agent, Skill, Tool, Connector, MCP, Workflow และ Guardrail](01-introduction/glossary.md)

1. [Introduction — แนวคิด คำศัพท์พื้นฐาน และ Autonomy Spectrum](01-introduction/README.md)
2. [Lab 1 — Google AI Studio Agent](02-build-ai-agent/README.md) · [Prompts](02-build-ai-agent/prompts.md)
3. [Lab 2 — Make Agentic Workflow](03-build-agentic-workflow/README.md) · [Prompts](03-build-agentic-workflow/prompts.md)
4. [Lab 3 — Managerial AI: Report, PDF และ Email](04-generate-management-report/README.md) · [Prompts](04-generate-management-report/prompts.md)
5. [LINE OA Instructor Demo](05-line-oa-demo/README.md)
6. [Lab 4 — Manus AI: Lab 2+3 without Workflow](06-manus-ai/README.md) · [Prompts](06-manus-ai/prompts.md)
7. [Responsible Agentic AI + Architecture Comparison](07-responsible-agentic-ai/README.md)
8. [Optional MBA Challenge](08-optional-mba-challenge/README.md) · [Worksheet](08-optional-mba-challenge/worksheet.md)
9. [Troubleshooting](troubleshooting/README.md)

## Final Deliverables

ผู้เรียนควรมี:

- AI Agent ที่ใช้ System Instructions และทดสอบ Business Rules แล้ว
- Google Form ที่เชื่อมกับ response sheet
- Make scenario ที่ Watch New Rows, เรียก Gemini, route ตาม Priority และอัปเดตแถวเดิม
- Request Log ที่มี HIGH, MEDIUM และ LOW อย่างน้อยประเภทละหนึ่งรายการโดยไม่มีแถวซ้ำ
- Weekly Management Report ที่มองหารูปแบบข้ามหลายคำร้อง
- PDF บน Google Drive และอีเมลทดสอบถึงตนเอง หรือ fallback artifact ที่เทียบเท่า
- Manus task ที่สร้าง Request Triage และ Management Report จาก Goal เดียว โดยไม่สร้าง Workflow
- ตารางเปรียบเทียบ Make Workflow กับ Manus Agent พร้อมข้อเสนอว่าเมื่อใดควรใช้แบบใด

## คำถามสรุป

> **Operational AI asks:** “What should we do with this request?”
>
> **Managerial AI asks:** “What are all these requests telling us about the business?”

---

[เริ่มบทนำ →](01-introduction/README.md)
