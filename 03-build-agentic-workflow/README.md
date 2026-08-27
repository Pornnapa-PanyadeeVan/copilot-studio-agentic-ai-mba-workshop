# 03 — Lab 2: Build an Agentic Workflow

🎯 **Goal**  เปลี่ยน `Business Request Assistant` จาก Agent ที่รอมนุษย์ถาม ให้เป็น workflow ที่เริ่มจาก Microsoft Forms วิเคราะห์ ตัดสินใจ และทำ Business Action

⏱ **Estimated Time**  70 นาที

## Target workflow

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
   ↙       ↓       ↘
HIGH    MEDIUM     LOW
  ↓        ↓        ↓
Teams    Excel    Excel
```

หาก AI ตอบ `NEEDS CLARIFICATION` หรือค่าที่ไม่ตรง ระบบต้องส่งให้มนุษย์ตรวจ ไม่ควรเดา branch

## เวลาแนะนำสำหรับ Lab

| นาที | งาน |
|---:|---|
| 0–12 | สร้าง Form |
| 12–20 | เตรียม Excel table และ Teams channel |
| 20–35 | Trigger + Get Response Details |
| 35–50 | AI Analysis |
| 50–62 | Decision + Teams/Excel Actions |
| 62–70 | Test + Debrief |

> [!IMPORTANT]
> **UI MAY VARY:** Microsoft มีทั้ง `Flows`, `Workflows (preview)`, `Agent flows` และ Power Automate cloud flows ตาม harness, tenant และ rollout ปัจจุบัน Microsoft ระบุว่า Workflows แบบใหม่ยังเป็น preview และ Agent flows แบบมาตรฐานอาจเปิด designer ในอีก tab ดู [Copilot Studio flows overview](https://learn.microsoft.com/en-us/microsoft-copilot-studio/flows-overview) และ [Copilot Studio overview](https://learn.microsoft.com/en-us/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)

## เส้นทางที่แนะนำในห้องเรียน

ใช้ **Power Automate Automated cloud flow** เพราะ Microsoft Forms มี event trigger โดยตรง และแนวคิดที่เรียนเหมือนกันกับ flow designer ที่เปิดจาก Copilot Studio

```text
Copilot Studio environment
        ↕ same Power Platform environment
Power Automate automated cloud flow
```

### เลือกเส้นทางตามสิ่งที่เห็น

| หากเห็น | ให้ทำ |
|---|---|
| Copilot Studio → Workflows/Flows และสร้าง event-triggered flow ได้ | สร้างจากหน้านั้น แล้วใช้ขั้นตอนเชิงหน้าที่ด้านล่าง |
| Copilot Studio เปิด classic designer/Power Automate tab | ทำต่อใน tab ที่เปิด |
| ไม่พบ Forms trigger ใน Copilot Studio | ไปที่ [Power Automate](https://make.powerautomate.com) → Create → Automated cloud flow |
| ไม่มี AI action หรือ connector permission | ใช้ conceptual fallback ท้าย Lab; ห้ามเสียเวลาทั้งชั้นกับ permission |

> 📷 Screenshot needed:
> จุดเข้า Workflows/Flows ใน Copilot Studio และหน้า Create → Automated cloud flow ใน Power Automate

## Part A — Prepare the inputs

### 📌 Step 1 — สร้าง Microsoft Form

1. เปิด [Microsoft Forms](https://forms.office.com)
2. เลือก **New Form**
3. ตั้งชื่อ:

```text
New Business Request
```

4. เลือก **Add new** แล้วสร้างคำถามตามตาราง

| ลำดับ | Field | Question type | Setting |
|---:|---|---|---|
| 1 | Requester Name | Text | Required |
| 2 | Department | Choice หรือ Text | Required |
| 3 | Business Request | Text | Required + Long answer |
| 4 | Required Date | Date | Required |

ตัวเลือก Department ที่แนะนำ:

```text
Sales
Marketing
Finance
HR
Operations
IT
Customer Service
Other
```

5. เลือก **Preview** แล้วกรอกหนึ่งคำขอทดสอบ
6. เลือก **Collect responses** และใช้การจำกัดผู้ตอบตามนโยบายของชั้นเรียน

💡 **Why This Matters**  Form เปลี่ยนคำขอที่หลากหลายให้มี input ขั้นต่ำเหมือนกัน ช่วยให้ AI มี context และช่วยสร้าง audit trail

✅ **Checkpoint**  Form มี 4 fields ครบ และส่ง test response ได้

⚠️ **Common Problem**  หาก Form ไม่ปรากฏใน connector ตรวจว่าเจ้าของ Form และ connection เป็นบัญชีเดียวกัน ดู [Troubleshooting](../troubleshooting/README.md#microsoft-forms-connector-unavailable)

> 📷 Screenshot needed:
> Microsoft Forms → New Business Request พร้อม 4 fields

### 📌 Step 2 — เตรียม Excel table

1. เปิด Excel Online และสร้าง workbook ชื่อ:

```text
BusinessRequests.xlsx
```

2. บันทึกใน **OneDrive for Business** หรือ **SharePoint document library** ที่ connection ของผู้เรียนเข้าถึงได้
3. ใส่ headers ต่อไปนี้ใน row แรก:

```text
SubmittedAt | RequesterName | Department | BusinessRequest | RequiredDate | Summary | Priority | Reason | RecommendedAction | ReviewStatus
```

4. เลือกช่วง header แล้วใช้ **Home → Format as Table** หรือ **Insert → Table**
5. ยืนยันว่า table มี headers
6. ตั้งชื่อ table เป็น:

```text
BusinessRequestsTable
```

💡 **Why This Matters**  Action ของ Excel เขียนข้อมูลลง **table** ไม่ใช่ช่วง cell ธรรมดา Microsoft แนะนำให้เก็บ workbook ใน OneDrive/SharePoint และ format เป็น table ก่อนใช้ Power Automate

✅ **Checkpoint**  เปิด workbook ใหม่อีกครั้งแล้วยังเห็น table name และ headers ครบ

> 📷 Screenshot needed:
> Excel Online → BusinessRequestsTable และชื่อคอลัมน์

### 📌 Step 3 — เตรียม Teams destination

ผู้สอนควรเตรียม Team และ standard channel เช่น:

```text
Team: MBA Agentic AI Workshop
Channel: High Priority Requests
```

หากนักศึกษาไม่มีสิทธิ์สร้าง Team/Channel ให้ใช้ destination กลางของผู้สอน หรือทำ branch ให้เสร็จโดยยังไม่เปิด flow

⚠️ **Common Problem**  Microsoft ระบุว่า action `Post a message in a chat or channel` ไม่รองรับการส่งไป private channel ในบางรูปแบบ ใช้ standard channel สำหรับ Lab

## Part B — Build the flow

### 📌 Step 4 — สร้าง Automated cloud flow

**เส้นทาง Power Automate ที่แนะนำ**

1. เปิด [Power Automate](https://make.powerautomate.com)
2. ตรวจ environment ให้ตรงกับ Copilot Studio
3. เลือก **Create** → **Automated cloud flow**
4. ตั้งชื่อ:

```text
Business Request Agentic Workflow
```

5. ค้นหา trigger ของ Microsoft Forms:

```text
When a new response is submitted
```

6. เลือก **Create**
7. ใน `Form Id` เลือก `New Business Request`

**UI MAY VARY:** ใน new designer อาจเลือก card แล้วตั้งค่าทางซ้าย; classic designer แสดง fields บน card โดยตรง

💡 **Why This Matters**  Trigger ทำให้ flow เริ่มจาก business event แทนการรอให้มนุษย์เปิด chat และพิมพ์คำถาม

✅ **Checkpoint**  Trigger แสดง Form Id ที่ถูกต้อง

### 📌 Step 5 — Get Response Details

1. เลือก `+` หรือ **New step / Add an action**
2. ค้นหา connector **Microsoft Forms**
3. เลือก action:

```text
Get response details
```

4. ตั้งค่า:

| Field | Value |
|---|---|
| Form Id | `New Business Request` |
| Response Id | Dynamic content: `Response Id` จาก trigger |

💡 **Why This Matters**  Trigger แจ้งว่ามี response ใหม่ แต่ `Get response details` ดึงคำตอบจริงของแต่ละ field มาให้ขั้นถัดไปใช้

✅ **Checkpoint**  Dynamic content แสดง Requester Name, Department, Business Request และ Required Date

> 📷 Screenshot needed:
> Trigger และ Get response details พร้อม mapping ของ Response Id

### 📌 Step 6 — เพิ่ม AI Analysis

เลือกวิธีที่ tenant รองรับเพียงหนึ่งวิธี

📋 **Copy This Prompt**  เปิด [Workflow AI Analysis Prompt](prompts.md#workflow-ai-analysis-prompt) แล้ววางทั้งชุดใน AI action จากนั้นแทน placeholder ด้วย dynamic content ของ Form

#### Option A — Run a prompt (แนะนำเมื่อใช้ standard agent flow/AI Builder)

1. เพิ่ม action ใหม่
2. ใน AI capabilities ค้นหา:

```text
Run a prompt
```

3. เลือก prompt ที่เตรียมไว้ หรือเลือก **New custom prompt** หากมี
4. วาง [Workflow AI Analysis Prompt](prompts.md#workflow-ai-analysis-prompt)
5. แทรก dynamic content จาก `Get response details` ในตำแหน่ง Requester Name, Department, Business Request และ Required Date
6. หากเลือก output ได้ ให้ใช้ **JSON/Structured output**

Microsoft ระบุว่าชื่อเดิม `Create text with GPT using a prompt` เปลี่ยนเป็น `Run a prompt` ตั้งแต่ May 2025 แต่ **UI MAY VARY** ตาม rollout และ license

#### Option B — Run an agent (เมื่อใช้ new Workflows experience)

1. Publish `Business Request Assistant` ก่อน หากระบบกำหนด
2. เพิ่ม action ที่ทำหน้าที่ **Run an agent**
3. เลือก existing agent `Business Request Assistant`
4. ใส่ message จาก [Agent Message Template](prompts.md#agent-message-template)
5. เลือก **Structured output** หรือ **Custom structured output** ถ้ามี
6. สร้าง fields: `summary`, `priority`, `reason`, `recommendedAction`

**UI MAY VARY:** หากไม่พบ Prompt node ใน new workflow ไม่ต้องเดา Microsoft ระบุว่า Prompt node มีใน standard harness; new workflow ใช้ Agent action เพื่อได้ผลลัพธ์เทียบเท่า

#### Option C — Classroom fallback

หากไม่มี AI capacity หรือ permission:

1. ให้ผู้เรียนส่ง Form
2. คัดลอก Business Request ไปทดสอบใน Agent จาก Lab 1
3. บันทึก 4 fields ลงใน worksheet หรือ Excel ด้วยตนเอง
4. วาด Decision branches ให้ครบ

นี่คือ fallback ที่ยอมรับได้สำหรับ Workshop เพราะยังสอน Goal, Input, Reasoning, Decision, Action และ Human-in-the-loop ได้

💡 **Why This Matters**  AI Analysis เป็นจุดที่ free-form request ถูกเปลี่ยนเป็นข้อมูลที่ workflow ตัดสินต่อได้

✅ **Checkpoint**  เห็น output แยก 4 fields หรืออย่างน้อยข้อความ 4 บรรทัดตาม format

### 📌 Step 7 — สร้าง Priority Decision

#### ถ้ามี Structured output

1. เพิ่ม control **Switch**
   **UI MAY VARY:** หากไม่มี Switch ให้ใช้ Condition ซ้อนกัน
2. เลือก dynamic content `priority` จาก AI step
3. สร้าง cases:

```text
HIGH
MEDIUM
LOW
```

4. ตั้ง Default/Otherwise เป็น Human Review สำหรับ `NEEDS CLARIFICATION` หรือค่าอื่น

#### ถ้ามีเพียง Text output

แนะนำให้กลับไปใช้ JSON/Structured output ก่อน เพราะทนต่อการเปลี่ยนข้อความได้ดีกว่า หากจำเป็นจริง ให้ตรวจค่าที่ normalize แล้ว:

```text
toUpper(trim(<priority text>))
```

จากนั้นใช้ `equals(..., 'HIGH')` ตามลำดับ

⚠️ **Common Problem**  ช่องว่าง, markdown เช่น `**HIGH**` หรือประโยคยาวทำให้ Condition ไม่ match วิธีแก้ที่ดีที่สุดคือ structured output ไม่ใช่เพิ่มเงื่อนไขเดาจำนวนมาก

💡 **Why This Matters**  Decision boundary ควรอ่านได้ ตรวจสอบได้ และมี default branch เพื่อไม่ให้ค่าที่ผิด format ไปทำ Action เสี่ยงสูง

✅ **Checkpoint**  มี HIGH, MEDIUM, LOW และ Default/Human Review ครบ

> 📷 Screenshot needed:
> Priority Switch/Condition ที่แสดง 3 branches และ Default

### 📌 Step 8 — HIGH → Teams notification

ใน branch `HIGH`:

1. เพิ่ม Microsoft Teams action:

```text
Post a message in a chat or channel
```

2. ตั้งค่าตัวอย่าง:

| Setting | Value |
|---|---|
| Post as | Flow bot |
| Post in | Channel |
| Team | Team ที่ผู้สอนเตรียม |
| Channel | High Priority Requests |
| Message | ใช้ [Teams Message Template](prompts.md#teams-message-template) |

3. แทรก dynamic content แทน placeholder

> [!CAUTION]
> Teams message เป็น notification ไม่ใช่การอนุมัติหรือแก้ปัญหาโดยอัตโนมัติ Owner ที่ได้รับแจ้งยังต้องตรวจสอบข้อเท็จจริงและตัดสินใจ

✅ **Checkpoint**  Teams action มี Team, Channel และ Message ครบ

### 📌 Step 9 — MEDIUM/LOW → Excel

ใน branch `MEDIUM` และ `LOW` เพิ่ม action:

```text
Excel Online (Business) → Add a row into a table
```

ตั้งค่า:

| Field | Value |
|---|---|
| Location | OneDrive for Business หรือ SharePoint Site |
| Document Library | ตำแหน่งที่เก็บ workbook |
| File | `BusinessRequests.xlsx` |
| Table | `BusinessRequestsTable` |

Map columns:

| Excel column | Dynamic content / value |
|---|---|
| SubmittedAt | Submission time หรือ `utcNow()` |
| RequesterName | Requester Name |
| Department | Department |
| BusinessRequest | Business Request |
| RequiredDate | Required Date |
| Summary | AI `summary` |
| Priority | AI `priority` |
| Reason | AI `reason` |
| RecommendedAction | AI `recommendedAction` |
| ReviewStatus | `Pending` |

💡 **Why This Matters**  Excel ทำหน้าที่เป็น work queue และ audit trail เบื้องต้น ผู้จัดการยังตรวจ แก้ไข และติดตามได้

✅ **Checkpoint**  MEDIUM และ LOW มี Excel action และเลือก table ถูกต้อง

> [!TIP]
> Optional improvement: บันทึก HIGH ลง Excel ด้วยเพื่อให้ทุก request มี audit trail แล้วค่อยส่ง Teams เพิ่มใน HIGH branch การปรับนี้เหมาะสำหรับอภิปรายหลังจากทำ core lab เสร็จ

### 📌 Step 10 — Default → Human review

เมื่อ Priority เป็น `NEEDS CLARIFICATION`, ว่าง หรือไม่ตรง format:

- ส่งข้อความไป queue ของผู้สอน/ผู้จัดการ หรือ
- บันทึก Excel โดยตั้ง `ReviewStatus = Needs Clarification`

ห้าม route ไป HIGH/MEDIUM/LOW ด้วยการเดา

💡 **Why This Matters**  Exception path คือส่วนสำคัญของ Responsible Agentic AI ระบบที่ไม่มีทางออกเมื่อไม่แน่ใจมักสร้างความเสี่ยงมากกว่าความเร็วที่ได้

## Part C — Save and test

### 📌 Step 11 — บันทึกและทดสอบ end-to-end

🧪 **Test**  ส่งคำขอจำลองผ่าน Form แล้วติดตามข้อมูลเดียวกันตั้งแต่ trigger จนถึง Teams/Excel

1. เลือก **Save**
2. ใช้ **Flow checker** หากมี และแก้ connection/required field
3. เลือก **Test** → Manual หรือวิธีที่ UI เสนอ
4. กลับไป Microsoft Forms แล้ว submit 3 responses จาก [Sample Requests](../templates/sample-requests.md):
   - 1 HIGH
   - 1 MEDIUM
   - 1 LOW
5. เปิด Run history และตรวจทีละ action
6. ตรวจผล:
   - HIGH ปรากฏใน Teams
   - MEDIUM/LOW เพิ่ม row ใน Excel
   - fields ใน output ไม่สลับกัน

**UI MAY VARY:** บาง trigger poll เป็นระยะ จึงอาจไม่เริ่มทันที อย่ากด submit ซ้ำหลายครั้งโดยไม่ตรวจ run history เพราะจะสร้างข้อมูลซ้ำ

✅ **Final checkpoint**

- [ ] Trigger ทำงานจาก Form submission
- [ ] Get response details ดึงค่าถูก response
- [ ] AI output มี 4 fields
- [ ] Priority branch match แบบ exact
- [ ] Teams ได้เฉพาะ HIGH ใน core lab
- [ ] Excel ได้ MEDIUM/LOW
- [ ] Default/Human Review รองรับ ambiguous output

⚠️ **Common Problem**  ไปที่ [Troubleshooting Guide](../troubleshooting/README.md) และใช้ instructor fallback หลัง 5 นาทีหากเป็นปัญหา tenant/permission

## 💬 Discussion — From Agent to Agentic Workflow

| Lab 1 | Lab 2 |
|---|---|
| มนุษย์เริ่ม chat | Form event เริ่ม flow |
| Agent วิเคราะห์และแนะนำ | AI output เข้า Decision branch |
| ไม่มี Action ต่อระบบ | Teams/Excel action |
| ผู้ใช้เห็นคำตอบ | มี operational outcome และ run history |

คำถามสำคัญ:

1. Lab 2 เป็น Agentic AI เต็มรูปแบบหรือเป็น Agentic Workflow?
2. ระบบ observe ผลหลังส่ง Teams/เขียน Excel หรือยัง?
3. ใครรับผิดชอบถ้า HIGH ถูกจัดเป็น LOW?
4. KPI ควรวัดเวลาตอบสนอง ความถูกต้อง หรือ business impact?

คำตอบที่สมเหตุผล: ระบบนี้เป็น **Agentic Workflow** ที่มี event, AI reasoning, decision และ action แต่ feedback loop ยังจำกัด และมนุษย์ยังต้องจัดการ high-impact/ambiguous cases จึงควรอธิบาย autonomy อย่างตรงไปตรงมา

## 🏁 Completed

คุณได้เปลี่ยน Business Request Assistant จาก Agent ที่รอคำถาม ให้เป็น workflow ที่เริ่มจากเหตุการณ์และทำ Action ภายใต้ decision rules และ human fallback

---

[← Previous: Lab 1](../02-build-ai-agent/README.md) · [Home](../README.md) · [Next: MBA Challenge →](../04-mba-challenge/README.md)
