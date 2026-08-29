# 05 — Instructor Demo: LINE OA → Make → Gemini

[← Previous: Lab 3](../04-generate-management-report/README.md) · [Home](../README.md) · [Next: Lab 4 Google Antigravity →](../06-antigravity/README.md)

> **INSTRUCTOR-LED DEMO** อยู่ในเส้นทางหลัก 10 นาที แต่ผู้เรียนไม่ต้องสร้าง LINE Official Account, Messaging API channel หรือ webhook เอง

🎯 **Goal**  แสดงว่า Business Request มาจาก channel จริงอย่าง LINE ได้ โดย Agentic AI architecture ยังเหมือนเดิม

⏱ **Estimated Demo Time**  10 นาที

## Architecture

```text
Customer
↓
LINE OA
↓
Webhook
↓
Make
↓
Gemini
↓
Priority Decision
↓
Reply / Record / Alert
↓ if HIGH
Situation Report + OPEN Follow-up (Lab 3 pattern)
```

## Key Teaching Point

> LINE OA เป็นเพียง Channel (ช่องทางรับ/ส่งข้อความ) ไม่ใช่ Agentic AI

Agentic behavior อยู่ที่:

```text
Goal + Reasoning + Decision + Tools + Action + Data + Oversight
```

การเปลี่ยน input จาก manual/form เป็น LINE ไม่เปลี่ยนหลักการออกแบบ

## ก่อนสาธิต

- [ ] ใช้ LINE OA และ Messaging API channel สำหรับ demo เท่านั้น
- [ ] ใช้ Make Scenario ของผู้สอนที่ทดสอบล่วงหน้า
- [ ] ใช้บัญชี/ผู้ทดสอบที่ยินยอม
- [ ] ใช้ข้อความจำลอง ไม่มีลูกค้าจริง
- [ ] ซ่อน webhook URL, channel secret, access token และ user ID
- [ ] จำกัด reply/alert destination
- [ ] เตรียม recording/screenshot หรือ manual fallback

> **UI MAY VARY:** LINE Official Account Manager, LINE Developers Console และ Make module/connection อาจเปลี่ยน UI และสิทธิ์ตามบัญชี คู่มือนี้อธิบาย architecture ไม่รับประกันชื่อเมนู

## Demo Flow

### 1. Observe — รับข้อความ

ผู้สอนส่งข้อความจำลองไปยัง LINE OA:

```text
ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้
และอาจยกเลิกคำสั่งซื้อหากแก้ไม่ทันวันนี้
```

LINE Platform ส่ง webhook event ไปยัง endpoint ที่ลงทะเบียนไว้ ตาม [LINE Messaging API overview](https://developers.line.biz/en/docs/messaging-api/overview/) และ [Receive messages](https://developers.line.biz/en/docs/messaging-api/receiving-messages/)

### 2. Analyze — Make ส่ง text เข้า Gemini

Map เฉพาะข้อความที่จำเป็นเข้า Prompt เดียวกับ Lab 2 ให้ตอบ JSON:

```text
summary
priority
reason
recommended_action
```

### 3. Decide — Router

```text
HIGH → Record + alert + Follow-up Status OPEN + Lab 3 report handoff
MEDIUM → Record + normal acknowledgement
LOW → Record + self-service acknowledgement
```

### 4. Act — Reply / Record / Alert

ตัวอย่าง reply ที่ปลอดภัย:

```text
ได้รับคำร้องแล้ว ระบบได้บันทึกเพื่อให้ผู้รับผิดชอบตรวจสอบ
หมายเลขอ้างอิง: [Demo Request ID]

หมายเหตุ: ข้อความนี้เป็นการสาธิต ไม่ใช่คำยืนยันการแก้ไขหรือการอนุมัติ
```

บันทึก Request Log และส่ง HIGH alert ไปยังช่องทาง demo ของผู้สอน ใน production design HIGH row ควรส่งต่อ control แบบ Lab 3 เพื่อสร้าง DRAFT report และติดตามสถานะ `OPEN`; Demo 10 นาทีไม่ต้องสร้าง PDF ซ้ำ

## Security Notes

- LINE แนะนำให้ verify webhook signature เพื่อยืนยันแหล่งที่มา ดู [Verify webhook signature](https://developers.line.biz/en/docs/messaging-api/verify-webhook-signature/)
- อย่าพึ่ง IP allowlist แทน signature verification
- Webhook อาจถูก redeliver จึงต้องป้องกัน duplicate ด้วย event/request ID
- Reply token, channel secret และ access token เป็น secret
- อย่าบันทึก message/user ID เกินความจำเป็น
- Demo นี้ไม่ใช่ production security design

## Instructor Fallback

หาก LINE/Make connection ไม่พร้อม:

1. แสดง architecture diagram
2. ใช้ sample webhook payload ที่ลบ identifier แล้ว
3. เริ่ม Scenario หลัง webhook ด้วยข้อความจำลอง
4. แสดงผล Router/Sheet จาก run ที่บันทึกไว้

ผู้เรียนยังตอบได้ว่า:

```text
Channel เปลี่ยนได้ แต่ Agentic AI architecture ยังเหมือนเดิม
```

## 💬 Discussion

1. LINE OA เพิ่ม Business Value อะไรเมื่อเทียบกับ manual input?
2. Channel จริงเพิ่ม privacy, consent และ service expectation อย่างไร?
3. ควรให้ AI ตอบอะไรอัตโนมัติ และอะไรต้องรอเจ้าหน้าที่?
4. หาก webhook ส่งซ้ำ ระบบจะป้องกัน duplicate action อย่างไร?

## 🏁 Demo Completed

- [ ] ผู้เรียนเห็น message → webhook → AI → decision → action
- [ ] อธิบายได้ว่า LINE OA เป็น Channel
- [ ] ไม่มี secret หรือข้อมูลจริงปรากฏ
- [ ] Human Review ยังอยู่ใน HIGH route
- [ ] อธิบายได้ว่า HIGH case ส่งต่อ Situation Report + OPEN follow-up ได้

---

[← Previous: Lab 3](../04-generate-management-report/README.md) · [Home](../README.md) · [Next: Lab 4 Google Antigravity →](../06-antigravity/README.md)
