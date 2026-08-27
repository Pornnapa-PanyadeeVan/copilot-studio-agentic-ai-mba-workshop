# Lab 2 — Copy/Paste Prompts and Test Data

[← Lab 2 Guide](README.md) · [Home](../README.md) · [Next: Lab 3 Prompts →](../04-generate-management-report/prompts.md)

> ใช้ simulated data เท่านั้น และห้ามวาง API key ใน Prompt

## Business Request JSON Prompt

แทน `{{BUSINESS_REQUEST}}` ด้วยค่าจาก Trigger ผ่าน Make mapping ไม่ใช่พิมพ์วงเล็บปีกกาตายตัว

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

## Test Requests

### HIGH

```text
Requester: Demo Customer
Department: Customer Service
Request: ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้ และอาจยกเลิกคำสั่งซื้อหากแก้ไม่ทันวันนี้
```

### MEDIUM

```text
Requester: Demo Marketing Manager
Department: Marketing
Request: ต้องการรายงานผลแคมเปญเพื่อประชุมผู้บริหารในอีกสี่วัน ขณะนี้งานการตลาดยังดำเนินต่อได้
```

### LOW

```text
Requester: Demo Employee
Department: HR
Request: ขอทราบขั้นตอนเปลี่ยนรูป Profile ในระบบประชุมออนไลน์ ไม่มี deadline และไม่กระทบงานปัจจุบัน
```

### Anti-keyword Test

```text
Requester: Demo Employee
Department: HR
Request: ด่วนมาก ASAP กรุณาส่งคู่มือการตั้งค่าธีมสีของระบบ ไม่มีลูกค้า รายได้ หรือ operations ได้รับผลกระทบ
```

Expected: `LOW` ไม่ใช่ `HIGH`

## Fallback JSON

ใช้เมื่อ Gemini API/connection ไม่พร้อม เพื่อฝึก JSON → Router → Action ต่อ

### HIGH JSON

```json
{
  "summary": "ลูกค้ารายใหญ่ไม่สามารถชำระเงินและอาจยกเลิกคำสั่งซื้อภายในวันนี้",
  "priority": "HIGH",
  "reason": "มีผลกระทบต่อลูกค้าและรายได้ทันที พร้อมข้อจำกัดด้านเวลาที่สำคัญ",
  "recommended_action": "แจ้งเจ้าของระบบชำระเงินและผู้จัดการทันที พร้อมติดตามสถานะเป็นระยะ"
}
```

### MEDIUM JSON

```json
{
  "summary": "ฝ่ายการตลาดต้องการรายงานผลแคมเปญสำหรับการประชุมในอีกสี่วัน",
  "priority": "MEDIUM",
  "reason": "เป็นงานสำคัญที่มี deadline แต่ operations ยังดำเนินต่อได้",
  "recommended_action": "มอบหมายผู้รับผิดชอบและยืนยันเวลาส่งรายงานก่อนวันประชุม"
}
```

### LOW JSON

```json
{
  "summary": "พนักงานขอวิธีเปลี่ยนรูป Profile ในระบบประชุมออนไลน์",
  "priority": "LOW",
  "reason": "เป็นคำขอข้อมูลทั่วไป ไม่มีผลกระทบทันทีและไม่มี deadline",
  "recommended_action": "ส่งลิงก์คู่มือหรือบทความช่วยเหลือมาตรฐาน"
}
```

## Expected Data Structure

```json
{
  "summary": "string",
  "priority": "HIGH",
  "reason": "string",
  "recommended_action": "string"
}
```

ค่าที่อนุญาตสำหรับ `priority` มีเพียง:

```text
HIGH
MEDIUM
LOW
```

## HIGH Alert Email Template

ส่งถึงอีเมลของตนเองเท่านั้น

**Subject**

```text
[TEST] HIGH Priority Business Request — Human Review Required
```

**Body**

```text
นี่คือการแจ้งเตือนจาก Workshop ด้วยข้อมูลจำลอง

ผู้ร้อง: {{REQUESTER}}
หน่วยงาน: {{DEPARTMENT}}
สรุป: {{SUMMARY}}
Priority: {{PRIORITY}}
เหตุผล: {{REASON}}
การดำเนินการที่แนะนำ: {{RECOMMENDED_ACTION}}

โปรดตรวจสอบข้อเท็จจริงก่อนดำเนินการ
```

## Sheet Alert Marker Fallback

```text
⚠️ HIGH — Human review required: {{SUMMARY}}
```

---

[← Lab 2 Guide](README.md) · [Home](../README.md) · [Next: Lab 3 Prompts →](../04-generate-management-report/prompts.md)
