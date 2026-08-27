# Instructor Preparation Checklist

Checklist สำหรับ Workshop 3 ชั่วโมง ผู้เรียนประมาณ 30 คน

## 1–2 weeks before class

### Access and licenses

- [ ] ผู้เรียนมี Microsoft 365 work/school account
- [ ] ผู้เรียนเข้าถึง Microsoft 365 Copilot ตามที่หลักสูตรกำหนด
- [ ] ผู้เรียนเข้าถึง [Microsoft Copilot Studio](https://copilotstudio.microsoft.com)
- [ ] ตรวจ Copilot Studio license/capacity หรือ trial limitation
- [ ] ผู้เรียนเข้าถึง Microsoft Forms
- [ ] ผู้เรียนเข้าถึง Excel Online (Business)
- [ ] ผู้เรียนเข้าถึง Microsoft Teams
- [ ] ผู้เรียนเข้าถึง Power Automate หรือ flow designer ที่เปิดจาก Copilot Studio

### Environment and governance

- [ ] ระบุ Power Platform environment ที่ทุกคนต้องใช้
- [ ] ตรวจ DLP policy ว่า Forms, Teams, Excel Online (Business) และ AI action ใช้ร่วมกันได้
- [ ] ตรวจว่า student role สร้าง Agent และ flow ได้
- [ ] ตรวจ connector authentication ด้วยบัญชีประเภทเดียวกับผู้เรียน
- [ ] ตรวจ Teams Team/Channel และสิทธิ์ post
- [ ] ตรวจ OneDrive/SharePoint location และสิทธิ์ workbook
- [ ] ตกลงว่าจะ Publish Agent หรือทดสอบใน Preview/Test เท่านั้น
- [ ] ตกลง policy การใช้ AI capacity/credits ระหว่าง class

### Test the exact workshop path

- [ ] สร้าง `Business Request Assistant` ด้วย prompt จาก repository
- [ ] ทดสอบทั้ง HIGH, MEDIUM, LOW และ NEEDS CLARIFICATION
- [ ] สร้าง `New Business Request` Form
- [ ] สร้าง `BusinessRequests.xlsx` และ `BusinessRequestsTable`
- [ ] สร้าง flow ตั้งแต่ Forms trigger ถึง AI Analysis
- [ ] ยืนยันชื่อ AI action ที่ tenant แสดง (`Run a prompt`, `Run an agent` หรือเทียบเท่า)
- [ ] ยืนยัน Structured output/JSON ใช้งานได้
- [ ] ทดสอบ Priority Switch/Condition แบบ exact
- [ ] ทดสอบ Teams notification ใน standard channel
- [ ] ทดสอบ Excel `Add a row into a table`
- [ ] เปิด run history และเตรียมอธิบาย failure details

## 2–3 days before class

### Classroom setup for 30 participants

- [ ] แบ่งผู้เรียนเป็น 8–10 ทีม ทีมละ 3–4 คน
- [ ] กำหนดให้ทำ Agent คนละคน หรือ 1 maker ต่อทีมเพื่อลด connector load
- [ ] แจก repository link และขอให้เปิดก่อนวันเรียน
- [ ] เตรียม Team/Channel กลาง หรือช่องทางแยกสำหรับการทดสอบ HIGH
- [ ] ตั้งชื่อ flow/agent ด้วย team number หากใช้ environment ร่วมกัน
- [ ] เตรียม sample data โดยไม่ใช้ข้อมูลจริง
- [ ] เตรียม QR/link ของ Form ตัวอย่างสำหรับ demo
- [ ] Capture screenshots ตาม [Images Checklist](../images/README.md)
- [ ] เตรียม browser tabs: Copilot Studio, Forms, Power Automate, Teams, Excel, repository
- [ ] เตรียม timer และประกาศจุด fallback ที่ 5 นาที

### Recommended naming convention

```text
Agent: Team-01 Business Request Assistant
Flow: Team-01 Business Request Agentic Workflow
Form: Team-01 New Business Request
Workbook: Team-01 BusinessRequests.xlsx
```

ช่วยลดการเลือก asset ผิดใน environment ที่ใช้ร่วมกัน

## Day-of-class quick check

- [ ] Sign-in ทำงานและไม่มี conditional access prompt ที่ค้าง
- [ ] Copilot Studio เปิด environment ที่ถูกต้อง
- [ ] Agent creation ไม่ถูกปิดโดย admin
- [ ] Forms connector เห็น form ของบัญชีผู้ทดสอบ
- [ ] Teams connector post ได้
- [ ] Excel connector เห็น file และ table
- [ ] AI action test สำเร็จอย่างน้อย 1 ครั้ง
- [ ] Run history พร้อมใช้งาน
- [ ] Repository relative links เปิดได้
- [ ] Backup slides/screenshots/worksheet พร้อม

## Setup risks for a 30-person class

| Risk | Early warning | Mitigation |
|---|---|---|
| Sign-in/conditional access delay | หลายคนเห็น approval/MFA loop | ให้ sign in ก่อนเริ่ม 10 นาที; มี 1 maker ต่อทีม |
| Mixed environments | หา Agent/Form/connection ไม่พบ | แสดง environment name บนจอ; ใช้ naming convention |
| License/capacity limit | Create/Run AI action disabled | ทดสอบ student account; ใช้ Lab 1 + conceptual Lab 2 fallback |
| Connector consent blocked | Forms/Teams/Excel ขอ admin approval | Pre-authorize connectors หรือใช้ instructor demo flow |
| 30 flows ส่ง Teams พร้อมกัน | Channel spam/throttling | ให้แต่ละทีม submit 1 HIGH; แยก channel หรือทำ action disabled demo |
| Excel file lock/table missing | Add row ล้มเหลว | ใช้ workbook ต่อทีม; ปิด desktop Excel; format as table ล่วงหน้า |
| UI rollout differs | นักศึกษาเห็นเมนูไม่ตรง | สอนตาม function; ใช้ป้าย UI MAY VARY และ screenshots 2 variants |
| Slow network | Designer/AI test timeout | ลดจำนวน maker, ใช้ prompt walkthrough และ worksheet |
| Accidental real data use | ผู้เรียน paste email/customer details | ย้ำ synthetic data; monitor shared screens; delete test artifacts ตาม policy |
| Duplicate flow runs | ผู้เรียน submit ซ้ำระหว่างรอ | ตรวจ run history ก่อน submit ใหม่; use unique requester label |

## Recommended backup plan

หาก workflow connectors fail:

1. ทุกคนทำ Lab 1 ให้เสร็จ
2. ผู้สอน demo flow ที่ทดสอบไว้ หรือใช้ screenshots จริงจาก tenant
3. ผู้เรียน copy Form request ไปใส่ Agent ด้วยตนเอง
4. ผู้เรียนบันทึก output ลง worksheet/Excel ด้วยตนเอง
5. ทุกทีมวาด Trigger → Input → AI Analysis → Decision → Action
6. ใช้เวลาที่เหลือกับ Decision boundary, Human-in-the-loop และ MBA Challenge

**Learning outcomes ยังสำเร็จได้** แม้ connector ใช้งานไม่ได้ เพราะเป้าหมายหลักคือ business understanding และการออกแบบ Agentic Workflow ไม่ใช่การแก้ปัญหา tenant ภายในห้อง

## Facilitation checkpoints

| เวลา | ผู้สอนตรวจ |
|---|---|
| 00:25 | ผู้เรียนแยก GenAI/Agent/Agentic AI ได้ |
| 00:40 | Agent name + instructions saved |
| 01:00 | ผ่าน 5 tests หรือรู้สาเหตุที่ไม่ผ่าน |
| 01:40 | Form + Excel table พร้อม |
| 02:00 | Trigger + AI step พร้อม |
| 02:20 | Decision + at least one Action พร้อม |
| 02:30 | เปลี่ยนไป MBA Challenge ไม่ว่า connector status เป็นอย่างไร |
| 02:50 | เริ่ม Responsible AI wrap-up |

## After class

- [ ] ปิด/turn off test flows ที่ไม่ต้องใช้ต่อ
- [ ] ลบข้อมูลจำลองตาม retention plan
- [ ] ตรวจ connection owners และ shared permissions
- [ ] เก็บ feedback: access, timing, difficult steps, business relevance
- [ ] อัปเดต screenshots เมื่อ Copilot Studio UI เปลี่ยน
- [ ] บันทึก tenant-specific differences แยกจาก student guide

---

[← Home](../README.md) · [Troubleshooting](../troubleshooting/README.md) · [Images Checklist](../images/README.md)
