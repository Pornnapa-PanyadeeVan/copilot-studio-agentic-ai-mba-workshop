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
| เครื่องมือหลัก | Google AI Studio, Make, Gemini API, Google Sheets, Google Docs/Drive และ Gmail |
| ข้อมูล | ใช้ข้อมูลจำลองเท่านั้น ห้ามใช้ข้อมูลจริงหรือข้อมูลลับ |
| ค่าใช้จ่าย | ออกแบบให้ใช้ free/free-tier; ไม่ต้องเปิด billing หรือซื้อ API credits เพื่อผ่าน Workshop |

## เป้าหมายการเรียนรู้

เมื่อจบ Workshop ผู้เรียนจะสามารถ:

1. แยกความแตกต่างระหว่าง Generative AI, AI Agent, Agent + Tools, Workflow และ Agentic AI
2. อธิบายว่า autonomy (ระดับความเป็นอิสระ) เป็นสเปกตรัม ไม่ใช่มีหรือไม่มีเพียงสองสถานะ
3. สร้าง `Business Request Assistant` ด้วย System Instructions ใน Google AI Studio
4. ใช้ Business Rules เพื่อจัดลำดับ `HIGH`, `MEDIUM`, `LOW` จากผลกระทบจริง
5. เชื่อม Trigger → Gemini → Decision Router → Action → Google Sheets ใน Make
6. เปลี่ยน Request History ให้เป็น Management Insight และส่งรายงาน PDF
7. กำหนด Human-in-the-loop, permission, audit trail และ fallback ที่เหมาะสม
8. ออกแบบ Agentic AI use case ที่วัด Business Value ได้

## เส้นทางการเรียนรู้

```text
Generative AI
↓
AI Agent
↓
Agent + Business Rules
↓
Workflow
↓
Decision
↓
Action
↓
Data / Memory
↓
Management Report
↓
Insight
↓
Human Decision
↓
Agentic AI
```

| แนวคิด | ทำอะไร |
|---|---|
| Generative AI | สร้างเนื้อหาจาก Prompt |
| AI Agent | ทำงานสู่ Goal โดยใช้อินสตรักชันและการให้เหตุผล |
| Agent + Tools | ติดต่อหรือสั่งงานระบบภายนอกได้ |
| Workflow | เชื่อมขั้นตอนของกระบวนการธุรกิจ |
| Decision | ผล AI กำหนดสิ่งที่จะเกิดขึ้นถัดไป |
| Action | ระบบลงมือทำงาน เช่น บันทึก ส่ง หรือแจ้งเตือน |
| Agentic AI | รวม Goal, Reasoning, Tools, Decisions, Actions, Workflow, Data, Feedback และ Human Oversight |

> Workflow อัตโนมัติทุกชนิดไม่ใช่ Agentic AI เสมอไป หากไม่มี Goal, AI reasoning หรือ decision ที่มีความหมาย ระบบนั้นอาจเป็นเพียง automation แบบกำหนดกฎล่วงหน้า

## สถาปัตยกรรมหลัก

```text
Business Request
↓
AI Agent
↓
Reason
↓
Priority Decision
↓
Workflow
↓
Action
↓
Google Sheets
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

## ตารางเวลา 3 ชั่วโมง

| เวลา | กิจกรรม | ผลลัพธ์ |
|---|---|---|
| 00:00–00:25 | [Introduction](01-introduction/README.md) | เข้าใจ Generative AI → AI Agent → Agentic AI |
| 00:25–01:05 | [Lab 1: Build a Business Request AI Agent](02-build-ai-agent/README.md) | Agent วิเคราะห์และจัด Priority |
| 01:05–01:15 | Break | พัก 10 นาที |
| 01:15–02:05 | [Lab 2: Build an Agentic Workflow](03-build-agentic-workflow/README.md) | Make เปลี่ยน AI decision เป็น Action และเก็บข้อมูล |
| 02:05–02:35 | [Lab 3: Generate a Management Report](04-generate-management-report/README.md) | รายงาน PDF บน Drive และส่ง Gmail |
| 02:35–02:50 | [MBA Agentic AI Challenge](05-mba-challenge/README.md) | แบบร่าง Agentic AI use case ของทีม |
| 02:50–03:00 | [Responsible Agentic AI](06-responsible-agentic-ai/README.md) + Wrap-up | Human oversight และ Exit Ticket |

กิจกรรมเสริมสำหรับผู้สอน: [LINE OA Instructor Demo](07-instructor-demo-line-oa/README.md)

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

- Google Account ที่เข้า Google AI Studio, Sheets, Drive, Docs และ Gmail ได้
- Make account แบบ Free
- Browser รุ่นปัจจุบัน และอินเทอร์เน็ต
- Gemini API key เฉพาะบุคคลสำหรับ Lab 2–3 หากบัญชีสร้างได้
- ไม่ต้องมี API key ใน Lab 1
- ไม่ต้องมีบัตรเครดิตและไม่ต้องเปิด paid tier

### ผู้สอน

- ทดสอบทุก connection ด้วยบัญชีประเภทเดียวกับผู้เรียน
- เตรียม [sample requests](templates/sample-requests.md) และ scenario/report fallback
- จำกัดการทดสอบคนละ 3 คำร้องใน Lab 2 เพื่อลด quota และ credit usage
- ใช้ [Instructor Checklist](templates/instructor-checklist.md) ก่อนสอน

## เครื่องมือ

| เครื่องมือ | ใช้ทำอะไร | หมายเหตุ |
|---|---|---|
| [Google AI Studio](https://aistudio.google.com/) | ทดลอง Prompt และ System Instructions | Lab 1 ใช้โดยไม่ต้องคัดลอก API key |
| [Gemini API](https://ai.google.dev/gemini-api/docs) | วิเคราะห์คำร้องและสร้างรายงานจาก Make | ใช้ key ของผู้เรียน; free tier มี rate limits |
| [Make](https://www.make.com/) | Workflow Orchestrator (ตัวประสานขั้นตอนงาน) | Free plan มี credit/feature limits และอาจเปลี่ยนได้ |
| Google Sheets | Request Log และข้อมูลสะสม | ใช้ข้อมูลจำลอง |
| Google Docs / Drive | สร้างและเก็บรายงาน | Permission ต้องอนุญาตให้ Make ตามที่ใช้จริง |
| Gmail | ส่งรายงานถึงอีเมลของผู้เรียนเอง | ใช้ `[Your Email]` ในคู่มือเสมอ |
| LINE OA | Channel สำหรับ instructor demo | ไม่ใช่ requirement ของผู้เรียน |
| Manus Free Tier | เปรียบเทียบ goal-based agent (ถ้ามีเวลา) | Optional และไม่กระทบการผ่าน Workshop |

## Free-tier และความเป็นส่วนตัว

> **FREE-TIER DISCLAIMER:** Free tier ไม่ได้หมายถึง unlimited จำนวน model, request rate, daily quota, Make credits, interval, connector หรือ eligibility อาจเปลี่ยนตามบัญชี ประเทศ และเวลาที่ใช้งาน ตรวจหน้าราคา/โควตาทางการก่อนสอนเสมอ

- Workshop นี้ไม่บังคับเปิด Cloud Billing หรือซื้อ credits
- หากหน้าจอเสนอ paid upgrade ให้หยุดและใช้ fallback
- Google ระบุว่า free tier อาจใช้ข้อมูลที่ส่งเพื่อปรับปรุงผลิตภัณฑ์ จึงใช้เฉพาะ simulated data
- ห้ามแชร์ API key, ใส่ key ใน screenshot, chat, Sheet หรือ GitHub
- Make นับการทำงานของ module เป็น credits; ทดสอบสั้นและปิด schedule หลังจบ
- ดูข้อมูลล่าสุด: [Gemini API Pricing](https://ai.google.dev/gemini-api/docs/pricing), [Gemini Rate Limits](https://ai.google.dev/gemini-api/docs/rate-limits), [Make Pricing](https://www.make.com/en/pricing)

## เริ่ม Workshop

1. [Introduction — แนวคิดและ Autonomy Spectrum](01-introduction/README.md)
2. [Lab 1 — Google AI Studio Agent](02-build-ai-agent/README.md) · [Prompts](02-build-ai-agent/prompts.md)
3. [Lab 2 — Make Agentic Workflow](03-build-agentic-workflow/README.md) · [Prompts](03-build-agentic-workflow/prompts.md)
4. [Lab 3 — Management Report, PDF และ Email](04-generate-management-report/README.md) · [Prompts](04-generate-management-report/prompts.md)
5. [MBA Challenge](05-mba-challenge/README.md) · [Worksheet](05-mba-challenge/worksheet.md)
6. [Responsible Agentic AI](06-responsible-agentic-ai/README.md)
7. [LINE OA Instructor Demo](07-instructor-demo-line-oa/README.md)
8. [Troubleshooting](troubleshooting/README.md)

## Final Deliverables

ผู้เรียนควรมี:

- AI Agent ที่ใช้ System Instructions และทดสอบ Business Rules แล้ว
- Make scenario ที่รับ input, เรียก Gemini, route ตาม Priority และบันทึก Sheet
- Request Log ที่มี HIGH, MEDIUM และ LOW อย่างน้อยประเภทละหนึ่งรายการ
- Weekly Management Report ที่มองหารูปแบบข้ามหลายคำร้อง
- PDF บน Google Drive และอีเมลทดสอบถึงตนเอง หรือ fallback artifact ที่เทียบเท่า
- MBA Agentic AI Canvas พร้อม Human-in-the-loop และ KPI

## คำถามสรุป

> **Operational AI asks:** “What should we do with this request?”
>
> **Managerial AI asks:** “What are all these requests telling us about the business?”

---

[เริ่มบทนำ →](01-introduction/README.md)
