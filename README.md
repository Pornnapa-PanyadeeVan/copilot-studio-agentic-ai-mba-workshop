# Build Your First Agentic AI with Microsoft Copilot Studio

> คู่มือ Workshop แบบลงมือทำสำหรับ MBA: จาก Generative AI ไปสู่ AI Agent และ Agentic Workflow ภายใน 3 ชั่วโมง โดยไม่ต้องเขียนโปรแกรม

## Workshop at a glance

| รายการ | รายละเอียด |
|---|---|
| กลุ่มเป้าหมาย | นักศึกษา MBA ระดับเริ่มต้น ประมาณ 30 คน |
| ระยะเวลา | 3 ชั่วโมง |
| รูปแบบ | Hands-on, business-oriented, ทำตาม repository ได้ด้วยตนเอง |
| กรณีศึกษาหลัก | **Business Request Management** |
| เครื่องมือ | Microsoft Copilot Studio, Microsoft Forms, Power Automate/Power Platform, Microsoft Teams, Excel Online |
| การเขียนโค้ด | ไม่ต้องใช้ |

> [!IMPORTANT]
> Microsoft Copilot Studio มีทั้งประสบการณ์ใหม่และแบบมาตรฐาน และชื่อเมนูอาจต่างกันตาม tenant, environment, license, region และช่วง rollout จุดที่อาจต่างจะระบุว่า **UI MAY VARY** ให้ยึด “หน้าที่ของขั้นตอน” เป็นหลัก ไม่ควรเดาชื่อเมนูที่มองไม่เห็น

## Workshop นี้เหมาะกับใคร

- นักศึกษา MBA ที่ต้องการเข้าใจ Agentic AI ในมุมธุรกิจ
- ผู้เริ่มต้นที่มี Microsoft 365 Copilot แต่ไม่เคยใช้ Copilot Studio
- ผู้บริหารและนักวิเคราะห์ที่ต้องการออกแบบงาน AI โดยไม่เขียนโปรแกรม
- ผู้สอนที่ต้องการกิจกรรม 3 ชั่วโมงสำหรับผู้เรียนประมาณ 30 คน

## Learning outcomes

เมื่อจบ Workshop ผู้เรียนจะสามารถ:

1. อธิบายความต่างระหว่าง **Generative AI, AI Agent, Agentic Workflow และ Agentic AI** ได้
2. สร้าง `Business Request Assistant` ใน Microsoft Copilot Studio
3. เขียน Agent Instructions และทดสอบการจัดลำดับความสำคัญของคำขอ
4. ออกแบบ Workflow ตั้งแต่ Trigger → Input → AI Analysis → Decision → Action
5. เชื่อม Microsoft Forms, AI analysis, Teams และ Excel ในระดับที่ tenant อนุญาต
6. ระบุจุดที่ต้องมี Human-in-the-loop และประเมินคุณค่าทางธุรกิจ
7. อธิบายความเสี่ยงด้านข้อมูล สิทธิ์ การจัดประเภทผิด และ Automation bias ได้

## Prerequisites

### สำหรับผู้เรียน

- บัญชี Microsoft 365 ของสถาบันหรือองค์กร
- สิทธิ์เข้า Microsoft Copilot Studio
- สิทธิ์ใช้ Microsoft Forms, Excel Online และ Microsoft Teams
- Browser รุ่นปัจจุบัน
- ไม่ต้องมีพื้นฐาน Programming

### สำหรับผู้สอน

- ทดสอบ Copilot Studio ใน **environment เดียวกับนักศึกษา** ก่อนสอน
- ตรวจ connector และ permission ของ Microsoft Forms, Teams และ Excel Online (Business)
- ตรวจว่ามีความสามารถ `Run a prompt`, `Run an agent` หรือ AI action ที่เทียบเท่า
- เตรียม Team/Channel สำหรับการแจ้งเตือน และ workbook ที่เก็บใน OneDrive for Business หรือ SharePoint
- เตรียมแผนสำรองจาก [Instructor Checklist](templates/instructor-checklist.md)

> [!WARNING]
> การมี Microsoft 365 Copilot ไม่ได้รับประกันว่าทุกคนจะมี Copilot Studio capacity, AI Builder credits หรือ connector permission เหมือนกัน ผู้สอนต้องทดสอบด้วยบัญชีผู้เรียนตัวอย่างก่อนวันสอน

## Tools

| Tool | ใช้ทำอะไรใน Workshop |
|---|---|
| Microsoft Copilot Studio | สร้างและทดสอบ AI Agent; เปิดการสร้าง flow/workflow ตามสิทธิ์ที่มี |
| Microsoft Forms | รับ Business Request |
| Power Automate / Power Platform | เชื่อม Trigger, AI Analysis, Decision และ Action |
| Microsoft Teams | แจ้งเตือนคำขอที่มี Priority = HIGH |
| Excel Online (Business) | บันทึกคำขอ MEDIUM/LOW และใช้เป็น audit trail เบื้องต้น |

## 3-hour schedule

| เวลา | กิจกรรม | ผลลัพธ์ |
|---|---|---|
| 00:00–00:25 | Introduction: GenAI → AI Agent → Agentic AI | เข้าใจคำศัพท์และกรณีศึกษา |
| 00:25–01:10 | Lab 1: Build Business Request AI Agent | Agent ที่สรุปและจัด Priority |
| 01:10–01:20 | Break | — |
| 01:20–02:30 | Lab 2: Build Agentic Workflow | Forms → AI → Decision → Teams/Excel |
| 02:30–02:50 | MBA Agentic AI Challenge | แบบออกแบบ Agentic Workflow ของทีม |
| 02:50–03:00 | Responsible AI + Wrap-up | Guardrails และ Human-in-the-loop |

## Workshop architecture

```text
Microsoft Forms
      ↓
New Business Request
      ↓
Get Response Details
      ↓
AI Analysis
      ↓
Priority Decision
   ↙      ↓      ↘
 HIGH   MEDIUM    LOW
   ↓       ↓       ↓
Teams    Excel   Excel
```

> ใน Lab 1 มนุษย์เริ่มบทสนทนาและนำคำขอไปถาม Agent ส่วน Lab 2 ใช้ event จาก Forms เป็น Trigger ให้ระบบเดินงานต่อได้โดยอัตโนมัติ

## Student learning path

```text
Generative AI
    ↓
AI Agent
    ↓
Agent + Tools
    ↓
Workflow
    ↓
Decision
    ↓
Action
    ↓
Agentic AI
```

- **Generative AI** สร้างเนื้อหา
- **AI Agent** ทำงานเพื่อเป้าหมาย โดยใช้ instructions, context และ tools
- **Agentic AI** ผสานเป้าหมาย การให้เหตุผล เครื่องมือ การตัดสินใจ การลงมือทำ workflow และ feedback เพื่อทำงานธุรกิจให้สำเร็จ

Agentic AI ไม่ใช่ป้ายที่ติดให้กับ automation ทุกชนิด ความเป็นอิสระหรือ **autonomy เป็น spectrum** ตั้งแต่งานที่มนุษย์กดเริ่มทุกครั้ง ไปจนถึงระบบที่สังเกตเหตุการณ์ ตัดสินใจ ลงมือทำ และเรียนรู้จากผลลัพธ์ภายใต้ guardrails

## Continuous business scenario: Business Request Management

องค์กรรับคำขอจากพนักงาน ระบบต้อง:

1. อ่านคำขอ
2. สรุป
3. ระบุ Priority
4. อธิบายเหตุผล
5. แนะนำ Action

ผลลัพธ์มาตรฐาน:

```text
Summary:
Priority:
Reason:
Recommended Action:
```

| Priority | หลักเกณฑ์ |
|---|---|
| **HIGH** | กระทบลูกค้าทันที, กระทบรายได้/การเงิน, เหตุขัดข้องสำคัญ, deadline ภายใน 24 ชั่วโมง, ความเสี่ยง compliance/reputation ร้ายแรง |
| **MEDIUM** | สำคัญแต่ยังไม่วิกฤต, deadline ภายในหลายวัน, ต้องการการพิจารณาจากผู้บริหาร |
| **LOW** | งานธุรการทั่วไป, ขอข้อมูลทั่วไป, ไม่มีผลกระทบทางธุรกิจทันที |
| **NEEDS CLARIFICATION** | ข้อมูลไม่พอที่จะตัดสินอย่างรับผิดชอบ ต้องถามเพิ่มหรือส่งให้มนุษย์ตรวจ |

## Start here

1. [Introduction: จาก GenAI สู่ Agentic AI](01-introduction/README.md)
2. [Lab 1: Build an AI Agent](02-build-ai-agent/README.md)
3. [Lab 1 Prompts](02-build-ai-agent/prompts.md)
4. [Lab 2: Build an Agentic Workflow](03-build-agentic-workflow/README.md)
5. [Lab 2 Prompts](03-build-agentic-workflow/prompts.md)
6. [MBA Challenge](04-mba-challenge/README.md)
7. [Challenge Worksheet](04-mba-challenge/worksheet.md)
8. [Responsible Agentic AI](05-responsible-agentic-ai/README.md)
9. [Sample Requests](templates/sample-requests.md)
10. [Troubleshooting](troubleshooting/README.md)

## Student success checklist

- [ ] Agent ชื่อ `Business Request Assistant` ถูกสร้างและบันทึก
- [ ] Agent ตอบครบ 4 บรรทัดตามรูปแบบที่กำหนด
- [ ] ทดสอบ HIGH, MEDIUM, LOW, ambiguous และ debate case
- [ ] Form มี 4 fields ครบ
- [ ] Workflow แสดง Trigger → Input → AI Analysis → Decision → Action
- [ ] HIGH ไป Teams; MEDIUM/LOW ไป Excel หรือมี conceptual fallback
- [ ] ทีมส่ง MBA Challenge worksheet และระบุ Human-in-the-loop
- [ ] ผู้เรียนอธิบายได้ว่าทำไม automation ไม่ได้เท่ากับ Agentic AI เสมอไป

## Final deliverables

ผู้เรียนควรมีอย่างน้อย:

1. AI Agent ที่ทดสอบได้ใน Copilot Studio
2. Workflow ที่ทำงานได้ หรือแผนผัง Workflow ที่ตรวจสอบได้หาก connector ถูกจำกัด
3. ผลทดสอบอย่างน้อย 3 ระดับ Priority และ 1 ambiguous case
4. MBA Challenge worksheet ของทีม
5. รายการ guardrails และ Human-in-the-loop ที่เหมาะกับกรณีศึกษา

## Official references

- [Microsoft Copilot Studio documentation](https://learn.microsoft.com/microsoft-copilot-studio)
- [Create a form with Microsoft Forms](https://support.microsoft.com/en-us/forms/create-a-form-with-microsoft-forms)
- [Microsoft Forms in Power Automate](https://learn.microsoft.com/en-us/power-automate/forms/popular-scenarios)
- [Send a Teams message with Power Automate](https://learn.microsoft.com/en-us/power-automate/teams/send-a-message-in-teams)
- [Connect Forms to Excel with Power Automate](https://support.microsoft.com/en-us/forms/setting-up-an-automated-workflow-between-microsoft-forms-and-excel-through-power-automate)

---

**Next:** [01 — Introduction](01-introduction/README.md)
