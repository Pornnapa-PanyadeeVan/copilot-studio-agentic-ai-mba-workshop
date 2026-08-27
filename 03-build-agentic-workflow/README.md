# 03 — Lab 2: Build an Agentic Workflow with Make

[← Previous: Lab 1](../02-build-ai-agent/README.md) · [Home](../README.md) · [Next: Lab 3 →](../04-generate-management-report/README.md)

🎯 **Goal**  เปลี่ยน AI reasoning เป็น Business Action ผ่าน Make, Gemini API และ Google Sheets

⏱ **Estimated Time**  45–50 นาที

🧰 **Tools**  Make + Gemini API key + Google Sheets

## Architecture

```text
Business Request
↓
Make
↓
Gemini
↓
Analyze
↓
Priority Decision
↓
Router
↙      ↓      ↘
HIGH  MEDIUM  LOW
↓       ↓       ↓
Action / Record
↓
Google Sheets
```

## Timebox

| นาที | งาน |
|---:|---|
| 0–7 | เตรียม Google Sheet |
| 7–14 | สร้าง API key และ connection |
| 14–23 | สร้าง Scenario และส่งคำร้องเข้า Gemini |
| 23–32 | ตรวจ/parse JSON |
| 32–41 | Router + Google Sheets action |
| 41–47 | HIGH alert |
| 47–50 | ทดสอบและสรุป |

> **UI MAY VARY:** Make และ Google AI Studio อาจเปลี่ยนชื่อ/ตำแหน่ง module, connection dialog, scenario controls และ model list ให้เลือก component ตามหน้าที่ที่อธิบาย อย่าเลือก paid-only feature หากบัญชีไม่มี และไม่ต้องอัปเกรดเพื่อทำ Lab

## ก่อนเริ่ม

- [ ] ผ่าน Lab 1 หรือมี [Lab 1 System Instructions](../02-build-ai-agent/prompts.md)
- [ ] Make account เปิด Scenario builder ได้
- [ ] Google Sheets ใช้งานได้
- [ ] ใช้ข้อมูลจำลองเท่านั้น
- [ ] เปิด [Lab 2 Prompts](prompts.md) อีก tab

## 📌 Step 1 — Prepare Google Sheet

1. สร้าง Google Spreadsheet ชื่อ `Business Request Log`
2. ตั้งชื่อ sheet/tab เช่น `Requests`
3. ใส่ชื่อ columns ในแถวแรกตามลำดับ:

```text
Timestamp
Requester
Department
Request
Summary
Priority
Reason
Recommended Action
```

4. Freeze header row หากต้องการ
5. อย่าใส่ชื่อคน อีเมลลูกค้า หรือข้อมูลจริง

💡 **Why This Matters**  Google Sheets ทำหน้าที่เป็น business data storage แบบง่าย เก็บ audit trail และสร้าง Request History สำหรับ Lab 3 ไม่ใช่ long-term production database

✅ **Checkpoint**  มี 8 columns สะกดตรงกันและ Sheet ยังไม่มีข้อมูลจริง

⚠️ **Common Problem**  Make มองไม่เห็น columns หาก header ว่างหรือซ้ำ ให้แก้ header แล้ว refresh/reselect data structure ใน connection

## 📌 Step 2 — Create a Gemini API Key

> ⚠️ **SECURITY: Never paste your API key into public GitHub files.**

1. เปิดหน้าจัดการ API keys จาก [Google AI Studio](https://aistudio.google.com/)
2. สร้าง key สำหรับบัญชี/โปรเจกต์ของตนเองตามตัวเลือกที่หน้า UI แสดง
3. คัดลอก key ไปใส่ใน Make connection โดยตรง
4. ไม่ส่ง key ให้เพื่อน ไม่วางใน Prompt, Sheet, screenshot หรือช่อง chat
5. หลัง Workshop ให้ลบ/rotate key หากไม่ใช้ต่อ

> **UI MAY VARY:** บัญชีใหม่บางประเภทอาจสร้าง project/key ให้อัตโนมัติ ขณะที่บัญชีองค์กร โรงเรียน หรือบางประเทศอาจถูกจำกัด ดู [Gemini API key documentation](https://ai.google.dev/gemini-api/docs/api-key)

### Free-tier Safety

- เลือก model ที่ระบุว่าใช้ได้ใน Free Tier ของบัญชี
- ไม่เปิด billing เพื่อผ่าน Workshop
- Free tier มี rate limits และรุ่นที่ใช้ได้อาจเปลี่ยน ตรวจ [Pricing](https://ai.google.dev/gemini-api/docs/pricing) และ [Rate limits](https://ai.google.dev/gemini-api/docs/rate-limits)
- จำกัดการทดสอบคนละ 3–5 ครั้ง
- หากสร้าง key ไม่ได้ ไปที่ [Fallback without API](#fallback-without-api)

✅ **Checkpoint**  Make connection บันทึก key แบบ secret/credential และไม่มี key ปรากฏในไฟล์หรือภาพ

⚠️ **Common Problem**  หาก Make connection ไม่ผ่าน ให้ตรวจว่า key ถูกคัดลอกครบ, model/region ใช้ได้ และ quota ยังเหลือ อย่าแชร์ key ของผู้สอนให้ทั้งห้อง

## 📌 Step 3 — Create a Make Scenario

สร้าง Scenario ใหม่ แล้วจัด component ตามหน้าที่:

```text
Trigger → AI → JSON Data → Router → Action
```

### Trigger ที่เหมาะกับห้อง 50 คน

เลือกหนึ่งทางตาม UI/บัญชี:

1. **Preferred:** จุดเริ่มแบบ run-on-demand/manual test ที่ให้ใส่ `Requester`, `Department`, `Business Request`
2. **Simple webhook:** รับ test payload จาก URL/form ทดสอบส่วนตัว
3. **Form-like trigger:** ใช้เฉพาะเมื่อ Instructor ทดสอบแล้วว่า free และทุกบัญชีเข้าถึงได้

อย่าใช้ channel จริงหรือ trigger ที่ต้องขอ enterprise permission

> **UI MAY VARY:** ใช้ Trigger ที่ผู้สอนยืนยันในวันสอน ไม่จำเป็นต้องชื่อเดียวกันทุกบัญชี หากใช้ webhook ห้ามแชร์ URL ต่อสาธารณะ เพราะ URL อาจเรียก Scenario ได้

### ข้อมูลเริ่มต้นสำหรับ Test Run

```text
Requester: Demo Customer
Department: Customer Service
Business Request: ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้ และอาจยกเลิกคำสั่งซื้อหากแก้ไม่ทันวันนี้
```

💡 **Why This Matters**  Trigger ระบุว่า Workflow เริ่มเมื่อใด ส่วน Agentic behavior มาจาก AI reasoning, decision และ action ที่ตามมา ไม่ได้มาจาก Trigger เพียงอย่างเดียว

✅ **Checkpoint**  Run test แล้ว Make รับค่าทั้ง 3 fields ได้

## 📌 Step 4 — Send the Request to Gemini

1. เพิ่ม Google Gemini AI integration หรือวิธีเรียก Gemini API ที่บัญชี Make รองรับ
2. สร้าง connection ด้วย API key ของตนเอง
3. เลือก text-generation function/model ที่ Free Tier เปิดให้บัญชี
4. Map `Business Request` ไปยัง `{{BUSINESS_REQUEST}}` ใน Prompt
5. ใช้ Prompt นี้จาก [prompts.md](prompts.md#business-request-json-prompt)

### 📋 Copy This Prompt

```text
You are a Business Request Assistant.

Analyze the following request.

Return ONLY valid JSON.

Use exactly this structure:

{
  "summary": "",
  "priority": "HIGH | MEDIUM | LOW",
  "reason": "",
  "recommended_action": ""
}

Priority rules:

HIGH:
customer, revenue, major operations, compliance,
reputation, or major time-sensitive business impact.

MEDIUM:
important but operations can continue.

LOW:
routine or informational request.

Do not classify HIGH only because the request says urgent.

Request:

{{BUSINESS_REQUEST}}

Respond in Thai except the priority value,
which must be HIGH, MEDIUM, or LOW.
```

💡 **Why This Matters**  JSON (รูปแบบข้อมูลที่มี key/value ชัดเจน) ช่วยให้ Workflow อ่านผลได้คาดการณ์มากกว่าข้อความอิสระ

🧪 **Test**  Run once แล้วเปิด output ของ Gemini ควรเห็น `summary`, `priority`, `reason`, `recommended_action`

✅ **Checkpoint**  Output เป็น JSON object เดียวและ `priority` เป็นตัวพิมพ์ใหญ่หนึ่งค่า

⚠️ **Common Problem**  หากมี Markdown code fence เช่น `````json`` ให้ย้ำ `Return ONLY valid JSON` แล้ว run ใหม่ หรือใช้ข้อความตัวอย่างจาก Instructor fallback

## 📌 Step 5 — Parse AI Output

ใช้ function/module ที่ทำหน้าที่ parse JSON ใน Make:

1. ใช้ Gemini text output เป็น input
2. กำหนด data structure จาก JSON ตัวอย่าง:

```json
{
  "summary": "ลูกค้ารายใหญ่ชำระเงินไม่ได้และอาจยกเลิกคำสั่งซื้อภายในวันนี้",
  "priority": "HIGH",
  "reason": "กระทบลูกค้าทันที รายได้ และมีผลกระทบด้านเวลาสำคัญ",
  "recommended_action": "แจ้งผู้รับผิดชอบระบบชำระเงินและผู้จัดการทันที พร้อมติดตามจนกู้ระบบได้"
}
```

3. ตรวจให้เห็น 4 output fields แยกจากกัน

💡 **Why This Matters**  AI output กำลังเปลี่ยนจาก “ข้อความ” เป็น “workflow data” ที่นำไปใช้ใน Condition และ Action ได้

✅ **Checkpoint**  Map ค่า `priority` เดี่ยว ๆ ไปยัง filter ได้โดยไม่ต้องคัดลอกด้วยมือ

⚠️ **Common Problem**  JSON parse ไม่ผ่าน ให้ตรวจ comma, quote, code fence และข้อความก่อน/หลัง object ดู [Troubleshooting](../troubleshooting/README.md#json-cannot-parse)

## 📌 Step 6 — Create the Decision Router

1. เพิ่ม Router (ตัวแยกเส้นทาง)
2. สร้าง 3 routes
3. ตั้ง Condition แบบ exact match:

```text
Priority = HIGH
Priority = MEDIUM
Priority = LOW
```

4. อย่าใช้ `contains HIGH` เพราะข้อความอื่นอาจทำให้ match ผิด

💡 **Why This Matters**  นี่คือ Decision step: ผล AI ไม่ได้เป็นเพียงข้อความ แต่กำหนดว่า Workflow จะทำอะไรต่อ

✅ **Checkpoint**  แต่ละ route มี filter ชัดเจนและไม่มีคำร้องหนึ่งรายการไปมากกว่าหนึ่ง route

⚠️ **Common Problem**  Route ไม่ match เพราะมีช่องว่าง/ข้อความเพิ่ม ให้ trim/normalize หรือแก้ Prompt ให้ `priority` เป็นค่าเดียว

## 📌 Step 7 — Add Actions

### Action สำหรับทุก Priority

ในแต่ละ route เพิ่ม Google Sheets action ที่ทำหน้าที่เพิ่ม row และ map:

| Sheet Column | Source |
|---|---|
| Timestamp | เวลาที่ Scenario ทำงาน |
| Requester | Trigger input |
| Department | Trigger input |
| Request | Business Request input |
| Summary | Parsed Gemini output |
| Priority | Parsed Gemini output |
| Reason | Parsed Gemini output |
| Recommended Action | Parsed Gemini output |

### Additional HIGH Alert

เพิ่ม Action ความเสี่ยงต่ำอีกหนึ่งอย่างเฉพาะ HIGH:

- ส่ง email ถึงอีเมลของผู้เรียนเอง โดยใช้ `[Your Email]` ตอนเขียนคู่มือ/ตัวอย่าง หรือ
- เพิ่ม alert marker ใน Sheet เช่น prefix `⚠️ HIGH — Human review required`

> Alert ไม่ใช่การอนุมัติ ไม่ใช่การคืนเงิน ไม่ใช่การลงโทษ และไม่ใช่การแก้ปัญหาอัตโนมัติ Manager ยังต้องตรวจข้อเท็จจริง

💡 **Why This Matters**  Workflow ทำ Real Action แล้ว แต่ Action ถูกจำกัดให้ reversible และ low-risk

✅ **Checkpoint**  ทุก route บันทึก Sheet; HIGH มี alert เพิ่มและส่งถึงตนเองเท่านั้น

⚠️ **Common Problem**  หาก Gmail connection unavailable ให้ใช้ alert marker ใน Sheet ซึ่งถือว่าผ่าน Lab 2

## 📌 Step 8 — Test HIGH, MEDIUM, LOW

ใช้ [Test Requests](prompts.md#test-requests) ทีละรายการ

```text
Input
↓
Gemini
↓
Priority
↓
Router
↓
Correct Branch
↓
Google Sheet
```

### 🧪 Test Checklist

- [ ] HIGH ไป HIGH route, มี row และ alert
- [ ] MEDIUM ไป MEDIUM routeและมี row
- [ ] LOW ไป LOW route และมี row
- [ ] Sheet มี 8 fields ที่ถูกต้อง
- [ ] ไม่มี request ซ้ำจากการกด Run หลายครั้ง
- [ ] ไม่มี API key ใน input/output history ที่แชร์กับผู้อื่น

✅ **Checkpoint**  เห็นอย่างน้อย 3 rows ใน Google Sheets และแต่ละ Priority เข้า route ถูกต้อง

## 💬 Discussion

เปรียบเทียบ:

```text
Generative AI: Prompt → Response

AI Agent: Goal → Reason → Decision → Recommendation

Agentic Workflow: Trigger → AI Reasoning → Decision → Tool → Action
```

คำถาม:

1. หากเอา Gemini ออกแล้วใช้ keyword rule อย่างเดียว ระบบยังเป็น Agentic AI หรือไม่?
2. หาก AI จัด HIGH ผิด Alert จะสร้างผลกระทบอะไร?
3. ควรเก็บ Manager override กลับมาเป็น feedback อย่างไร?

## Fallback without API

หากสร้าง key ไม่ได้, quota เต็ม หรือ Make เชื่อม Gemini ไม่สำเร็จ:

1. ใช้ Google AI Studio จาก Lab 1 วิเคราะห์คำร้องด้วยมือ
2. คัดลอกเฉพาะ JSON จำลองจาก [prompts.md](prompts.md#fallback-json)
3. ป้อน JSON เข้า Scenario หลังจุด AI หรือสาธิต mapping ด้วย Instructor scenario
4. ทำ Router และ Google Sheets ต่อให้ครบ

```text
Input → AI (manual) → Decision → Action
```

ผู้เรียนยังได้เรียนรู้ architecture แม้ connector ล้มเหลว

## Free-tier Reminder

- Make Free มี credit และ scheduling limits; ตรวจ [Make Pricing](https://www.make.com/en/pricing)
- Gemini Free Tier มี model/rate limits; ไม่รับประกันว่าจะรองรับ 50 accounts พร้อมกัน
- ปิด Scenario schedule หลังทดสอบเพื่อไม่ใช้ credits ต่อ
- Lab ผ่านเมื่อเห็น decision และ action ไม่จำเป็นต้องเปิดระบบ production

## 🏁 Completed

- [ ] สร้าง Business Request Log
- [ ] เก็บ API key ใน connection อย่างปลอดภัย หรือใช้ fallback
- [ ] Gemini ตอบ valid JSON
- [ ] Router มี 3 routes
- [ ] ทุก request บันทึกใน Sheet
- [ ] HIGH มี low-risk alert
- [ ] ทดสอบ HIGH, MEDIUM และ LOW แล้ว

---

[← Previous: Lab 1](../02-build-ai-agent/README.md) · [Home](../README.md) · [Next: Lab 3 →](../04-generate-management-report/README.md)
