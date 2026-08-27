# 05 — Responsible Agentic AI

🎯 **Goal**  ใช้ Agentic AI ให้เกิดคุณค่าทางธุรกิจโดยมี decision rights, permissions, auditability และ Human-in-the-loop ที่เหมาะสม

⏱ **Estimated Time**  10 นาที

## หลักคิดสำหรับผู้บริหาร

> ยิ่งระบบมี autonomy และทำ Action ที่กระทบคน เงิน ลูกค้า หรือชื่อเสียงมากเท่าไร ยิ่งต้องเพิ่ม evidence, permission, monitoring และ human control มากขึ้นเท่านั้น

ความเสี่ยงไม่ได้มาจาก model เพียงอย่างเดียว แต่เกิดจากการผสมกันของ:

```text
Model output × Business rule × Permission × Automated action × Scale
```

## Risk and control map

| ประเด็น | ความเสี่ยงทางธุรกิจ | Control ขั้นต่ำ |
|---|---|---|
| Human-in-the-loop | AI ทำ decision เกินอำนาจ | Human approval ก่อน high-impact/irreversible action |
| Data privacy | ข้อมูลลูกค้า/พนักงานถูกใช้เกินวัตถุประสงค์ | Data minimization, approved environment, retention policy |
| Hallucination | AI แต่ง deadline, impact หรือ policy | Grounding, evidence-based reason, default to clarification |
| Incorrect classification | HIGH ถูกจัดเป็น LOW หรือกลับกัน | Test set, reviewer sampling, escalation path, override |
| Automation bias | คนเชื่อ AI เพราะดูมั่นใจ | แสดง evidence/uncertainty และฝึก reviewer ให้ challenge ได้ |
| Permissions | Connector ใช้สิทธิ์ owner กว้างเกินไป | Least privilege, dedicated connection owner, periodic review |
| Audit trail | หาสาเหตุการตัดสินไม่ได้ | เก็บ input, output, timestamp, action, owner, override |
| High-impact decisions | กระทบสิทธิ์ งาน การเงิน กฎหมาย หรือสุขภาพ | AI ช่วยสรุป/แนะนำ; ผู้มีอำนาจตัดสินและอนุมัติ |

## Human-in-the-loop

มนุษย์ไม่ควรเป็น “rubber stamp” ที่กด approve โดยไม่อ่าน ควรกำหนด:

- ใครเป็น reviewer
- ข้อมูล/evidence ที่ reviewer ต้องเห็น
- SLA ในการ review
- ความสามารถ approve, edit, reroute หรือ reject
- วิธีบันทึก override และเหตุผล

### Human review triggers สำหรับกรณีศึกษา

- `NEEDS CLARIFICATION` หรือ confidence ไม่พอ
- มี compliance, legal, employment หรือ payment decision
- คำขอมีข้อมูลขัดแย้ง
- Action เปลี่ยนสิทธิ์หรือข้อมูลสำคัญ
- Priority สูง แต่ไม่มี evidence สนับสนุน
- ระบบหรือ connector ล้มเหลว

## Data privacy

ก่อนเชื่อมข้อมูล ให้ถาม:

1. จำเป็นต้องใช้ field นี้จริงหรือไม่?
2. ผู้ใช้และ connection owner มีสิทธิ์อ่าน/เขียนหรือไม่?
3. ข้อมูลจะถูกเก็บใน run history, Teams และ Excel นานเท่าไร?
4. มีข้อมูลส่วนบุคคล ข้อมูลการเงิน หรือข้อมูลพนักงานหรือไม่?
5. การใช้ข้อมูลสอดคล้องกับนโยบายองค์กรและวัตถุประสงค์ที่แจ้งไว้หรือไม่?

สำหรับ Workshop ใช้ข้อมูลจำลองเท่านั้น ห้ามใส่ secrets, tokens, tenant IDs, อีเมลจริง หรือข้อมูลลูกค้า/พนักงานจริง

## Hallucination and incorrect classification

Agent อาจตอบได้คล่องแต่ไม่มี evidence จึงควร:

- บังคับให้ Reason อ้างข้อมูลที่อยู่ใน request
- ห้ามสร้าง deadline, financial impact หรือ policy เอง
- มี `NEEDS CLARIFICATION`
- ทดสอบ adversarial และ ambiguous cases
- วัด agreement ระหว่าง AI กับ reviewer แยกตาม Priority
- ตรวจ false LOW อย่างจริงจัง เพราะอาจซ่อนเหตุการณ์สำคัญ

## Automation bias

ผู้ใช้มักเชื่อคำตอบที่เป็นระเบียบหรือมีน้ำเสียงมั่นใจ แม้จะผิด วิธีลดความเสี่ยง:

- แสดง Original Request ควบคู่กับ AI Summary
- แสดง Reason ไม่แสดงเพียง Priority
- ใช้คำว่า “Recommended Action” ไม่ใช่ “Approved Action”
- ให้ reviewer เปลี่ยน Priority ได้
- เก็บ override rate และวิเคราะห์สาเหตุ

## Permissions

Connector อาจทำงานด้วย credentials ของ maker/flow owner ไม่ใช่ผู้ส่ง Form ทุกคน จึงต้อง:

- ใช้ least privilege
- จำกัด Team, Channel, workbook และ repository/data source ที่เข้าถึง
- แยกบัญชี workshop ออกจาก production หากนโยบายอนุญาต
- ทบทวน connections เมื่อเปลี่ยนผู้สอนหรือ owner
- ปิด flow หลัง Workshop หากไม่ต้องการใช้งานต่อ

> [!WARNING]
> การที่ action “ทำงานได้” ไม่ได้แปลว่า permission “เหมาะสม” ผู้สอนต้องตรวจขอบเขตการเข้าถึงกับผู้ดูแล tenant

## Audit trail

บันทึกอย่างน้อย:

- Input ต้นฉบับ
- AI summary, priority, reason และ recommended action
- Model/flow version หรือวันที่แก้ instructions
- Timestamp และ run ID ที่ระบบสร้าง
- Action ที่ทำและผลสำเร็จ/ล้มเหลว
- Reviewer, override และเหตุผล

Excel ใน Lab เป็นเพียง audit trail เบื้องต้น ระบบจริงอาจต้องใช้ Dataverse, ticketing system หรือระบบควบคุมที่มี governance มากกว่า

## High-impact decisions

ตัวอย่างที่ AI ไม่ควรตัดสินขั้นสุดท้ายใน Workshop:

- อนุมัติ/ปฏิเสธการจ่ายเงิน
- จ้าง เลิกจ้าง หรือให้โทษพนักงาน
- ตัดสิน legal/compliance case
- เปลี่ยนสิทธิ์เข้าถึงข้อมูลสำคัญ
- ปฏิเสธบริการที่มีผลต่อสิทธิ์ของบุคคล

AI ยังช่วยได้โดยสรุปข้อมูล ตรวจความครบถ้วน จัด queue เตรียมคำถาม และแนะนำผู้มีอำนาจที่ควร review

## Responsible launch checklist

- [ ] Goal และ process owner ชัดเจน
- [ ] AI may/must not decision boundary ถูกเขียนไว้
- [ ] ใช้ข้อมูลจำลองในการสอนและทดสอบ
- [ ] Least-privilege connections
- [ ] Default branch ไป Human Review
- [ ] HIGH และ ambiguous cases มี human gate
- [ ] เก็บ original input + AI reason + action result
- [ ] มี kill switch เช่นปิด flow หรือ disconnect connector
- [ ] ทดสอบ false HIGH, false LOW และ prompt injection
- [ ] KPI รวม speed, quality, outcome และ risk

## 💬 Wrap-up discussion

1. Automation ใดควรคงเป็น deterministic rule แทน AI?
2. Decision ใดควรให้ AI recommend แต่ไม่ execute?
3. Feedback signal ใดทำให้วงจร `Observe → Reason → Decide → Act → Observe` สมบูรณ์ขึ้น?
4. ถ้าปิด AI แล้วกระบวนการธุรกิจยังเดินต่อได้หรือไม่?

## 🏁 Completed

Responsible Agentic AI ไม่ได้หมายถึงการหยุดนวัตกรรม แต่หมายถึงการออกแบบ autonomy ให้พอดีกับผลกระทบ มีผู้รับผิดชอบ และตรวจสอบย้อนกลับได้

---

[← Previous: MBA Challenge](../04-mba-challenge/README.md) · [Home](../README.md) · [Troubleshooting →](../troubleshooting/README.md)
