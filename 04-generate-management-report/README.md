# 04 — Lab 3: Managerial AI — HIGH Priority Situation & Follow-up PDF

[← Previous: Lab 2](../03-build-agentic-workflow/README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)

🎯 **Goal**  นำคำร้องที่ Lab 2 ตัดสินเป็น `HIGH` มาสร้างร่างรายงานสถานการณ์เร่งด่วนและรายการติดตามสำหรับ Manager แล้วแปลงเป็น PDF โดยยังคง Human Review

⏱ **Estimated Time**  25 นาที

🧰 **Tools**  Make + Google Sheets + Gemini + Google Docs/Drive; Gmail เป็น optional delivery

## Continuity from Lab 2

```text
Lab 2
Business Request → Gemini → Priority = HIGH → HIGH Route → Business Request Log
                                                        ↓
Lab 3
HIGH Case → Situation Report Draft → Validate → PDF → Follow-up Status → Human Review
```

Lab 3 ไม่สรุปยอดรายสัปดาห์และไม่วิเคราะห์หลายคำร้อง แต่ขยาย **HIGH case หนึ่งรายการ** ให้เป็น management artifact ที่ตอบว่า:

1. เกิดสถานการณ์อะไร?
2. มีหลักฐานของผลกระทบอะไร?
3. เหตุใดจึงเป็น HIGH?
4. เรื่องใดต้องได้รับ attention ทันที?
5. ใครต้องรับไปติดตาม และต้องยืนยันอะไร?
6. ข้อมูลใดยังขาด?

> รายงานคือ **Decision Support + Follow-up Artifact** ไม่ใช่คำสั่งอนุมัติ ไม่ใช่หลักฐานว่าสาเหตุได้รับการยืนยัน และไม่ใช่การแก้สถานการณ์อัตโนมัติ

## Architecture

```text
HIGH Row from Lab 2
↓
Prepare Case Payload
↓
Gemini Drafts Situation & Follow-up Report
↓
Validate Evidence + Required Sections
↓
Create Document → Export PDF → Restricted Drive Folder
↓
Update Report Link + Follow-up Status = OPEN
↓
Optional Email to Self
↓
Human Review / Assign Owner / Confirm Target Time
```

## Timebox

| นาที | งาน |
|---:|---|
| 0–3 | เลือก HIGH case จาก Lab 2 |
| 3–7 | เตรียม Case Payload |
| 7–12 | ให้ Gemini สร้างร่างรายงาน |
| 12–16 | Validate evidence และ required sections |
| 16–21 | สร้าง Document/PDF และบันทึก Drive |
| 21–23 | อัปเดต Report Link + Follow-up Status |
| 23–25 | ส่งถึงตนเองหรือใช้ fallback แล้วสรุป |

> **UI MAY VARY:** ชื่อ action สำหรับค้นหา row, สร้าง document, export PDF, upload Drive, update row และ Gmail อาจต่างตาม Make version/connection ให้เลือกตาม function ที่ต้องการ ไม่ต้องอัปเกรด paid plan เพื่อจบ Lab

## ก่อนเริ่ม

- [ ] มี `Business Request Log` จาก Lab 2
- [ ] มีคำร้องอย่างน้อยหนึ่งรายการที่ `Priority = HIGH`
- [ ] HIGH row มี `Request ID`, `Request`, `Summary`, `Reason` และ `Recommended Action`
- [ ] Google Drive เป็นบัญชีของตนเองและ folder ตั้งเป็น private/restricted
- [ ] เปิด [Lab 3 Prompts](prompts.md)
- [ ] ใช้ข้อมูลจำลองเท่านั้น

## 📌 Step 1 — Select One HIGH Case

เลือก HIGH row ที่ผ่าน HIGH route ใน Lab 2 โดยแนะนำ test case ที่มีผลกระทบชัด เช่น:

```text
Request ID: BR-001
Department: Sales
Request: ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้และอาจยกเลิกคำสั่งซื้อ
Context: ต้องแก้ภายในวันนี้; order มีมูลค่าสำคัญ
Priority: HIGH
```

ตรวจว่า `HIGH` มาจาก business impact ไม่ใช่เพียงคำว่า “ด่วน”, “ASAP” หรือ “ทันที”

💡 **Why This Matters**  Lab 3 ต้องเริ่มจาก Decision ที่ Lab 2 สร้างไว้ จึงเห็นว่า AI classification เปลี่ยนเส้นทางและสร้าง artifact สำหรับการจัดการอย่างไร

✅ **Checkpoint**  เลือกหนึ่ง row ที่ `Priority = HIGH` และมี evidence ของ customer, financial, operational, compliance, reputation หรือ time impact

⚠️ **Common Problem**  หากไม่มี HIGH row ให้ใช้ [Fallback HIGH Case](prompts.md#fallback-high-case) หรือ run HIGH test จาก Lab 2 อีกครั้ง ห้ามเปลี่ยน MEDIUM เป็น HIGH เพียงเพื่อให้ผ่าน Lab

## 📌 Step 2 — Prepare the Case Payload

ใน HIGH route หรือ Scenario แยกแบบ run-on-demand ให้ map ข้อมูลเป็นข้อความที่มี labels ชัดเจน:

```text
Report Generated At: {{TIMESTAMP}}
Request ID: {{REQUEST_ID}}
Requester: {{REQUESTER}}
Department: {{DEPARTMENT}}
Original Request: {{REQUEST}}
AI Summary: {{SUMMARY}}
Priority: {{PRIORITY}}
Priority Reason: {{REASON}}
Recommended Action: {{RECOMMENDED_ACTION}}
Current Follow-up Status: {{FOLLOW_UP_STATUS_OR_OPEN}}
```

ข้อมูลที่ไม่มีให้ส่งคำว่า `NOT PROVIDED` อย่าให้ AI เดาชื่อ owner, จำนวนเงิน, จำนวนลูกค้า, root cause หรือเวลาที่จะแก้เสร็จ

💡 **Why This Matters**  Structured payload ทำให้รายงานอ้างกลับไปยัง source row ได้และลด hallucination

✅ **Checkpoint**  Payload มี Request ID และ `Priority: HIGH`; ไม่มี API key, email จริง หรือข้อมูลลับ

⚠️ **Common Problem**  หาก field ว่าง ให้ map จาก trigger/Sheet ใหม่หรือใช้ `NOT PROVIDED` อย่ากรอกข้อมูลสมมติเพิ่มเอง

## 📌 Step 3 — Generate the HIGH Situation Report

เพิ่ม Gemini step แล้ว map payload ไปยัง `{{HIGH_CASE_DATA}}` ใช้ Prompt ฉบับเต็มจาก [prompts.md](prompts.md#high-priority-situation-report-prompt)

### 📋 Copy This Prompt

```text
You are a managerial incident-reporting assistant.

Create a concise Thai draft report for ONE simulated business request
that has already been classified as HIGH.

If the supplied Priority is not exactly HIGH, stop and return:
"STOP — Source Priority is not HIGH; no report created."

Use only the supplied case data. Do not invent facts, counts, monetary values,
root causes, owner names, deadlines, resolution status, policies, or SLAs.
If information is unavailable, write "ไม่พบในข้อมูลต้นทาง".

Do not approve, authorize, compensate, discipline, contact external parties,
or claim that any corrective action has already occurred.

Title:
# ร่างรายงานสถานการณ์เร่งด่วนและรายการติดตาม

Required sections:

## สถานะรายงาน
- DRAFT — HIGH PRIORITY — HUMAN REVIEW REQUIRED

## ข้อมูลอ้างอิง
- Report Generated At
- Request ID
- Department
- Source Priority

## ภาพรวมสถานการณ์
- What happened
- What is affected
- What is known now

## ผลกระทบที่มีหลักฐาน
- Customer
- Financial / Revenue
- Operations
- Compliance / Reputation
- Time Sensitivity
Mark unsupported dimensions as "ไม่พบในข้อมูลต้นทาง".

## เหตุผลที่จัดเป็น HIGH
- Explain using evidence from the source only

## สิ่งที่ต้องได้รับ Attention ทันที
- Provide proposed checks, containment, or escalation steps
- Label every item as a recommendation pending human confirmation

## รายการติดตาม
Create a table with:
Follow-up Item | Proposed Owner | Target Time | Status | Evidence / Source
Use "Manager to assign" and "Manager to confirm" when not provided.
Use OPEN or PENDING VALIDATION as status; never write RESOLVED.

## การตัดสินใจหรือการอนุมัติที่ต้องการ

## ข้อมูลที่ยังขาด

## Human Review Sign-off
- Reviewer
- Decision / Changes
- Owner Confirmed
- Target Time Confirmed
- Review Date

End with:
"รายงานนี้สร้างจากข้อมูลจำลองเพื่อการเรียนรู้ ต้องตรวจสอบข้อเท็จจริง
และได้รับการยืนยันจากผู้รับผิดชอบก่อนดำเนินการหรือเผยแพร่"

HIGH Case Data:
{{HIGH_CASE_DATA}}
```

💡 **Why This Matters**  Managerial AI ใน Lab นี้เปลี่ยน operational decision หนึ่งรายการให้เป็นสถานการณ์ที่ติดตามได้ ไม่ได้สร้างสถิติรายสัปดาห์

🧪 **Test**  ค้นหาคำว่า `ไม่พบในข้อมูลต้นทาง`, `Manager to assign`, `Manager to confirm` และตรวจว่า AI ไม่แต่งข้อเท็จจริงแทนช่องว่าง

✅ **Checkpoint**  รายงานมี Request ID, evidence, HIGH reason, immediate attention, follow-up table, missing information และ Human Review Sign-off

⚠️ **Common Problem**  หากรายงานเขียนว่า “แก้ไขแล้ว” หรือสร้าง owner/deadline เอง ให้ใช้ [Correction Prompt](prompts.md#correction-prompt) และคงสถานะเป็น DRAFT

## 📌 Step 4 — Validate Before Creating the PDF

ตรวจอย่างน้อย:

- [ ] ใช้ข้อมูลเพียงหนึ่ง Request ID
- [ ] Source Priority เป็น `HIGH`
- [ ] เหตุผล HIGH มี evidence ไม่อาศัย urgent keyword อย่างเดียว
- [ ] ไม่มี root cause, count, amount, SLA, owner หรือ deadline ที่ไม่มี source
- [ ] ทุก proposed action ระบุว่า pending human confirmation
- [ ] Follow-up status เป็น `OPEN` หรือ `PENDING VALIDATION`
- [ ] มี missing information และ Human Review Sign-off
- [ ] ไม่มีข้อมูลจริงหรือ confidential data

หากข้อใดไม่ผ่าน ให้หยุดก่อนสร้าง PDF

💡 **Why This Matters**  PDF ดูเป็นทางการและอาจเพิ่ม automation bias จึงต้อง validate เนื้อหาก่อนสร้าง artifact

✅ **Checkpoint**  Reviewer ในทีมยืนยัน checklist ครบและยังเห็นคำว่า `DRAFT — HUMAN REVIEW REQUIRED`

## 📌 Step 5 — Create the Document and PDF

1. ใช้ Google Docs หรือ document action ที่บัญชี Make รองรับ
2. สร้าง document จาก report text
3. ตั้งชื่อ:

```text
DRAFT HIGH Situation Report — {{REQUEST_ID}} — YYYY-MM-DD
```

4. Export/convert เป็น PDF ชื่อ:

```text
DRAFT-HIGH-Situation-Report-{{REQUEST_ID}}-YYYY-MM-DD.pdf
```

5. ตรวจว่าเปิด PDF ได้และขนาดมากกว่า 0 bytes

> หาก Make ไม่มี document/PDF action ให้ใช้ [Manual Document Fallback](#manual-document-fallback) ไม่ต้องซื้อ feature เพิ่ม

💡 **Why This Matters**  PDF เป็น artifact สำหรับ review และติดตาม แต่ยังไม่ใช่ final approval

✅ **Checkpoint**  PDF เปิดได้ ชื่อไฟล์มี Request ID และทุกหน้าระบุว่าเป็น DRAFT/Human Review

⚠️ **Common Problem**  หากได้ URL หรือ text แทน PDF ให้เพิ่มขั้นตอน export/download binary ก่อน upload หรือใช้ manual fallback

## 📌 Step 6 — Save to Google Drive

สร้าง folder แบบ restricted:

```text
Agentic-AI-Reports/
└── HIGH-Follow-up/
```

บันทึก PDF ใน `HIGH-Follow-up` และห้ามเปิด `Anyone with the link`

✅ **Checkpoint**  เห็นไฟล์ PDF ใน folder ของตนเองและ permission เป็น private/restricted

⚠️ **Common Problem**  หาก Make หา folder ไม่พบ ให้ตรวจ account/ownership หรือเก็บ PDF local แล้วบันทึก intended path ใน Sheet

## 📌 Step 7 — Update the Follow-up Tracker

อัปเดต HIGH row เดิมใน `Business Request Log`:

| Column | Value |
|---|---|
| Report Status | `DRAFT — HUMAN REVIEW REQUIRED` |
| Report Link | Restricted Drive link หรือ local filename |
| Follow-up Status | `OPEN` |

ห้ามสร้าง row ใหม่สำหรับคำร้องเดิม เพราะจะทำให้ audit trail ซ้ำ ให้ค้นหาด้วย `Request ID`

💡 **Why This Matters**  วงจรไม่ได้จบที่ PDF; Manager ต้องเห็นว่างานยัง OPEN และต้อง assign owner/confirm target time

✅ **Checkpoint**  HIGH row เดิมมี report link และ `Follow-up Status = OPEN`

⚠️ **Common Problem**  หาก update row ไม่สำเร็จ ให้กรอกสาม field ด้วยตนเองและอภิปราย idempotency/Request ID

## 📌 Step 8 — Optional Email to Self

ส่งถึงอีเมลของผู้เรียนเองเท่านั้น

**Subject**

```text
[DRAFT][HIGH][Human Review] {{REQUEST_ID}} — โปรดติดตามสถานการณ์เร่งด่วน
```

**Body**

```text
พบคำร้องจำลองที่ถูกจัดเป็น HIGH และสร้างร่างรายงานเพื่อ Human Review แล้ว

Request ID: {{REQUEST_ID}}
Department: {{DEPARTMENT}}
Situation: {{SUMMARY}}
Follow-up Status: OPEN

สิ่งที่ต้องทำต่อ:
1. ตรวจสอบข้อเท็จจริงและผลกระทบ
2. ยืนยันหรือแก้ไข Priority
3. มอบหมาย Owner
4. ยืนยัน Target Time
5. บันทึกการตัดสินใจและสถานะล่าสุด

ไฟล์แนบเป็น DRAFT และไม่ใช่การอนุมัติให้ดำเนินการ
```

Attach PDF หรือใส่ restricted Drive link หาก attachment path ไม่พร้อม

✅ **Checkpoint**  ได้รับ email ที่ inbox ของตนเอง หรือบันทึก draft text เป็น fallback

⚠️ **Common Problem**  หาก Gmail authorization ไม่ผ่าน ให้ข้าม email; PDF + updated follow-up tracker ถือว่าผ่าน Lab

## Manual Document Fallback

1. ใช้ [Fallback HIGH Case](prompts.md#fallback-high-case) กับ Prompt ใน Google AI Studio
2. ตรวจ report ด้วย Step 4 checklist
3. Copy ไป Google Docs ด้วยตนเอง
4. Download/export เป็น PDF
5. เก็บใน Drive folder ของตนเองหรือ local folder
6. อัปเดต `Report Status`, `Report Link`, `Follow-up Status` ด้วยตนเอง
7. อธิบายว่า Make จะ automate จุดใด

Fallback ยังคง Learning Path:

```text
HIGH Decision → Situation Report → Validate → PDF → OPEN Follow-up → Human Review
```

## 💬 Discussion

1. เหตุใด PDF ของ HIGH case ต้องติดป้าย DRAFT?
2. หาก AI แต่ง owner หรือ deadline เอง จะเกิดความเสี่ยงอะไร?
3. เมื่อใด `OPEN` จึงเปลี่ยนเป็น `RESOLVED` และใครมีสิทธิ์เปลี่ยน?
4. รายงานควรส่งอัตโนมัติถึงใครบ้าง หรือควรรอ approval ก่อน?

## Bridge to LINE Demo and Lab 4

- LINE Demo เปลี่ยน Channel ที่รับคำร้อง แต่ HIGH decision ยังต้องเข้า report/follow-up control เดียวกัน
- Lab 4 ให้ Antigravity Workspace Agent triage dataset แล้วสร้าง draft report files สำหรับ **ทุก case ที่จัดเป็น HIGH** ภายใน project scope โดยไม่ประกอบ Make Workflow และไม่ทำ external action

ให้จดว่า Lab 2–3 ต้องกำหนด Router, document, PDF, Drive และ tracker update เอง เพื่อนำไปเปรียบเทียบ control, repeatability และ setup effort กับ Lab 4

## 🏁 Completed

- [ ] รับ HIGH case ต่อจาก Lab 2
- [ ] สร้าง Situation & Follow-up Report จาก source evidence เท่านั้น
- [ ] Validate ก่อนสร้าง PDF
- [ ] สร้าง PDF แบบ DRAFT หรือใช้ manual fallback
- [ ] เก็บไฟล์แบบ restricted
- [ ] อัปเดต HIGH row เป็น `Follow-up Status = OPEN`
- [ ] ระบุ Human Review, Owner และ Target Time ที่ยังต้องยืนยัน

---

[← Previous: Lab 2](../03-build-agentic-workflow/README.md) · [Home](../README.md) · [Next: LINE OA Demo →](../05-line-oa-demo/README.md)
