# 06 — Responsible Agentic AI

[← Previous: MBA Challenge](../05-mba-challenge/README.md) · [Home](../README.md) · [Optional: LINE OA Demo →](../07-instructor-demo-line-oa/README.md)

🎯 **Goal**  กำหนดขอบเขตที่ AI ทำเองได้ สิ่งที่ต้องให้คนอนุมัติ และ controls ที่ทำให้ระบบรับผิดชอบได้

⏱ **Estimated Time**  10 นาที

## หลักสำคัญ

> ความเสี่ยงไม่ได้มาจากคำตอบ AI เพียงอย่างเดียว แต่เพิ่มขึ้นเมื่อคำตอบนั้นเชื่อมกับ Decision, Permission และ Action จริง

```text
More autonomy
↓
More possible value
↓
More need for boundaries, monitoring and accountability
```

## 1. Human-in-the-loop

Human-in-the-loop (การให้มนุษย์ตรวจหรืออนุมัติในจุดสำคัญ) ไม่ได้หมายถึงให้คนตรวจทุกอย่าง แต่ต้องวาง gate ตามผลกระทบ

| Action | Auto ได้ | AI Recommend | Human Approval |
|---|:---:|:---:|:---:|
| บันทึกข้อมูลจำลองลง Sheet | ✓ | | |
| ติดป้าย Priority เบื้องต้น | ✓ | ✓ | เมื่อ confidence ต่ำ/impact สูง |
| ส่ง alert ถึงเจ้าของงาน | ✓ | | |
| ส่ง weekly internal report | | ✓ | ✓ หากข้อมูลจริง/วงกว้าง |
| อนุมัติการจ่ายเงิน | | ✓ | ✓ |
| ลงโทษ/ประเมินพนักงาน | | ✓ | ✓ |
| ตัดสิน legal/compliance | | ✓ | ✓ |
| คืนเงินหรือชดเชยลูกค้ารายใหญ่ | | ✓ | ✓ |
| เปิดเผย sensitive personal data | | | ต้องมีกระบวนการเฉพาะและสิทธิ์ตามกฎหมาย |

## 2. Data Privacy

- ใช้ simulated data ใน Workshop เท่านั้น
- เก็บข้อมูลเท่าที่จำเป็นต่อ Goal
- แยก identifier ออกจากข้อความเมื่อทำได้
- กำหนด retention และผู้เข้าถึง Sheet/Drive/Make run history
- ห้ามส่ง confidential, personal, financial, health หรือ employee-sensitive data เข้า free-tier model โดยไม่มีการประเมินนโยบายองค์กร
- ตรวจ terms/data-use ของผู้ให้บริการก่อน production

## 3. Hallucination

Hallucination (AI สร้างข้อมูลที่ไม่มีหลักฐาน) อาจเกิดใน summary, cause, count หรือ recommendation

Controls:

- แยก `observed fact` ออกจาก `hypothesis`
- บังคับให้ระบุ missing information
- ตรวจ count ด้วย Sheet/Workflow เมื่อทำได้
- ห้าม AI สร้าง policy, SLA หรือ financial figure ที่ไม่มีใน input
- ให้ Human Review สำหรับ claim ที่มีผลกระทบสูง

## 4. Incorrect Classification

False HIGH ทำให้ alert fatigue และเสียเวลา ส่วน false LOW อาจทำให้เหตุสำคัญถูกละเลย

Controls:

- ใช้ business-impact rules ไม่ใช้ urgent keyword อย่างเดียว
- ทดสอบ HIGH/MEDIUM/LOW/AMBIGUOUS และ edge cases
- บันทึก Manager override
- วิเคราะห์ confusion pattern เป็นระยะ
- กำหนด default escalation เมื่อข้อมูลไม่พอและ impact อาจสูง

## 5. Automation Bias

Automation bias คือการเชื่อ AI มากเกินไปเพราะระบบดูเป็นอัตโนมัติหรือมั่นใจ

- แสดง reason และ source data ควบคู่ decision
- ไม่ใช้สี/คำว่า “approved” หากเป็นเพียง recommendation
- ทำให้ override ง่ายและไม่ลงโทษผู้ใช้ที่ตั้งคำถาม
- ฝึกผู้ใช้ให้ตรวจ evidence ไม่ใช่ตรวจเพียงความลื่นไหลของภาษา

## 6. API Key Security

- ใช้ key เฉพาะบุคคลและเก็บใน Make connection/secret field
- ห้าม commit key ลง GitHub
- ห้ามวางใน Sheet, Prompt, screenshot, email หรือ chat
- จำกัด key ให้บริการที่จำเป็นตามตัวเลือกของ provider
- Rotate/revoke key เมื่อสงสัยว่ารั่วหรือหลัง Workshop หากไม่ใช้ต่อ
- อย่าแชร์ instructor key ให้ผู้เรียน 50 คน

ถ้า key ถูก commit ให้ถือว่ารั่วทันที: revoke ก่อน ลบจาก history ตามกระบวนการ แล้วสร้างใหม่

## 7. Permissions

ใช้ Least Privilege (ให้สิทธิ์น้อยที่สุดที่จำเป็น):

| Connection | สิทธิ์ที่ Lab ต้องใช้ | ไม่ควรเปิดโดยไม่จำเป็น |
|---|---|---|
| Google Sheets | อ่าน/เขียน Sheet ทดสอบ | Drive ทั้งหมดหรือไฟล์ธุรกิจจริง |
| Google Drive | สร้าง/เก็บ report folder | แชร์สาธารณะอัตโนมัติ |
| Gmail | ส่งอีเมลทดสอบถึงตนเอง | อ่าน/ส่งแทน mailbox องค์กรวงกว้าง |
| LINE OA demo | รับ/ตอบข้อความ demo | production customer channel |

## 8. Audit Trail

ควรบันทึก:

- Timestamp และ request ID
- Input ที่จำเป็นหลัง masking
- Prompt/rule/model version
- AI summary, priority, reason และ recommendation
- Route และ Action ที่ทำจริง
- Error/retry
- Human approver, override และเหตุผล

Audit trail ไม่ควรกลายเป็นที่เก็บข้อมูลลับโดยไม่จำเป็น

## 9. High-impact Decisions

ต้องมี stronger human review สำหรับ:

- Financial approval/payment
- Employee discipline, hiring หรือ termination
- Legal issues และ compliance
- Major customer escalation/compensation
- Sensitive personal information
- Safety หรือสิทธิขั้นพื้นฐาน

สำหรับกรณีเหล่านี้ AI เหมาะกับการจัดข้อมูล สรุป evidence และเสนอทางเลือก ไม่ควรเป็น final decision maker

## 10. Failure and Stop Conditions

ระบบควรหยุดหรือส่งให้คนเมื่อ:

- JSON parse ไม่ผ่าน
- Priority ไม่อยู่ใน allowed values
- ข้อมูลสำคัญหาย
- Model/API quota หรือ connector fail
- Action ซ้ำหรือไม่ทราบว่าทำสำเร็จหรือไม่
- Request มี legal, compliance, finance, employment หรือ sensitive data
- Confidence/impact อยู่นอกขอบเขตที่อนุญาต

## 💬 Discussion

เลือก Action จากทีมของคุณหนึ่งข้อแล้วตอบ:

1. ถ้า AI ผิด ใครได้รับผลกระทบ?
2. Action ย้อนกลับได้หรือไม่?
3. ใครต้อง approve?
4. ต้องเก็บหลักฐานอะไร?
5. Kill switch หรือ fallback คืออะไร?

## Exit Ticket

เติมประโยค:

1. “Agentic AI ต่างจาก chatbot เพราะ…”
2. “Action ที่ AI ทำอัตโนมัติได้ใน use case ของฉันคือ…”
3. “Action ที่ต้องมี Human Approval คือ…”
4. “Management Insight ที่จะเกิดจากข้อมูลสะสมคือ…”

## 🏁 Completed

- [ ] ระบุ Human Approval gate
- [ ] ระบุ privacy และ permission boundary
- [ ] มี audit trail และ override
- [ ] มี stop condition/fallback
- [ ] แยก recommendation ออกจาก final high-impact decision

---

[← Previous: MBA Challenge](../05-mba-challenge/README.md) · [Home](../README.md) · [Optional: LINE OA Demo →](../07-instructor-demo-line-oa/README.md)
