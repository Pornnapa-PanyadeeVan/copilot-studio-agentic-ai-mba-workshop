# 04 — MBA Agentic AI Challenge

🎯 **Goal**  ออกแบบ Agentic Workflow สำหรับปัญหาธุรกิจจริง โดยแสดง Goal, Trigger, AI Reasoning, Decision, Action, Human-in-the-loop และ Business Value

⏱ **Estimated Time**  20 นาที

👥 **Team size**  3–4 คน

## Challenge brief

แต่ละทีมเลือกปัญหาธุรกิจหนึ่งเรื่อง แล้วออกแบบ:

```text
Trigger
  ↓
Input
  ↓
AI Reasoning
  ↓
Decision
  ↓
Action
```

ทีมไม่ต้องสร้างระบบจริง เป้าหมายคือออกแบบ workflow ที่มีเหตุผลทางธุรกิจ ใช้งานได้ และมี guardrails

## เลือกหนึ่ง Business Problem

- Customer Complaint Management
- Sales Lead Qualification
- Purchase Request
- Invoice Processing
- Employee Request
- Email Prioritization
- Customer Review Management
- Recruitment Screening

หรือเลือกปัญหาอื่นที่ทีมมีประสบการณ์ โดยต้องอธิบาย owner และ measurable outcome ได้

## บทบาทในทีม

| Role | หน้าที่ |
|---|---|
| Business Owner | นิยาม Goal, policy และ KPI |
| Process Designer | วาด Trigger → Action และ exception path |
| Risk Challenger | ถามว่าอะไรผิดพลาดได้และ Human-in-the-loop อยู่ตรงไหน |
| Presenter | สรุป proposal ภายใน 60–90 วินาที |

ทีม 3 คนรวม Business Owner กับ Presenter ได้

## Challenge timeline

| นาที | กิจกรรม |
|---:|---|
| 0–2 | เลือก Business Problem และกำหนด Goal |
| 2–10 | กรอก worksheet และออกแบบ workflow |
| 10–15 | เพิ่ม Human-in-the-loop, risk และ KPI |
| 15–19 | 2–3 ทีม pitch; ทีมอื่นส่ง worksheet |
| 19–20 | Instructor synthesis |

## 📌 Step 1 — กำหนด Business Goal

Goal ที่ดีควรระบุผลลัพธ์ ไม่ใช่แค่ “ใช้ AI”

| ไม่ชัด | ชัดกว่า |
|---|---|
| ใช้ AI จัดการ complaint | ลดเวลาคัดแยก complaint พร้อมรักษาความถูกต้องของ escalation |
| สร้าง recruitment agent | ช่วยสรุป evidence ตามเกณฑ์งาน โดยไม่ตัดสินจ้างแทนมนุษย์ |

💡 **Why This Matters**  ถ้า Goal ไม่ชัด ระบบจะ optimize สิ่งที่วัดไม่ได้ หรือทำ Action ที่ไม่สอดคล้องกับเจ้าของกระบวนการ

## 📌 Step 2 — ออกแบบ 5 ขั้นหลัก

กรอก [Challenge Worksheet](worksheet.md) โดยตอบอย่างน้อย:

1. What is the business goal?
2. What triggers the agent?
3. What information does it need?
4. What must AI reason about?
5. What decision can AI make?
6. What action can the system take?
7. Where should a human remain in the loop?
8. What could go wrong?
9. How would you measure business value?

✅ **Checkpoint**  ทุกกล่องมี owner หรือ data source ที่อธิบายได้ ไม่ใช้คำกว้าง ๆ เช่น “AI decides everything”

## 📌 Step 3 — วาด Happy path และ Exception path

ตัวอย่าง:

```text
New complaint
    ↓
Read customer message + account tier
    ↓
Reason about severity, customer impact, evidence
    ↓
Decision
 ├─ Clear low risk → Log + standard response draft
 ├─ High impact → Notify service manager
 └─ Missing/conflicting data → Human review
```

💡 **Why This Matters**  ระบบธุรกิจล้มเหลวบ่อยในกรณีข้อมูลไม่ครบ ไม่ใช่ happy path จึงต้องออกแบบ “เมื่อ AI ไม่แน่ใจ” ตั้งแต่ต้น

## 📌 Step 4 — กำหนด Decision Boundary

ระบุให้ชัด:

- AI **may decide** อะไร
- AI **may recommend** อะไร
- AI **must not decide** อะไร
- เหตุการณ์ใดต้องหยุดรอ approval

ตัวอย่าง Recruitment Screening:

- May decide: จัดหมวดทักษะจาก CV ตามเกณฑ์ที่ประกาศ
- May recommend: รายชื่อที่ควรได้รับ human review
- Must not decide: ปฏิเสธผู้สมัครหรือส่ง offer โดยอัตโนมัติ
- Human gate: ทุกการตัดสินที่มีผลต่อสถานะผู้สมัคร

⚠️ **Common Problem — เลือก Action ที่เสี่ยงเกินไป**  เปลี่ยนจาก “approve/reject” เป็น “summarize, prioritize, draft, route, flag” แล้ววาง human approval ก่อน Action ที่ย้อนกลับยาก

## 📌 Step 5 — เลือก KPI

KPI ควรสมดุลอย่างน้อย 3 ด้าน:

| มิติ | ตัวอย่าง |
|---|---|
| Speed | Median triage time, response time |
| Quality | Priority agreement with reviewers, false escalation rate |
| Outcome | Revenue saved, complaints resolved, cycle time reduced |
| Risk | Incorrect high-impact decisions, privacy incidents |
| Adoption | % requests processed, human override rate |

อย่าวัดเพียงจำนวนงานที่ AI ทำ เพราะจำนวนมากไม่ได้แปลว่าสร้างคุณค่า

## 🧪 60-second stress test

ทีมอื่นถามหนึ่งข้อ:

- ถ้า input ว่างหรือขัดแย้ง ระบบทำอะไร?
- ถ้า AI มั่นใจแต่ผิด ใครหยุด Action ได้?
- ถ้า connector ใช้สิทธิ์ของ owner ผู้ใช้เห็นข้อมูลเกินสิทธิ์หรือไม่?
- ถ้า volume เพิ่ม 10 เท่า KPI และต้นทุนเปลี่ยนอย่างไร?

## 💬 Pitch format

ใช้โครง 60–90 วินาที:

```text
Our business goal is...
The workflow starts when...
The AI reasons about...
It may decide...
The system then...
A human must review when...
We will measure value using...
```

## Evaluation rubric

| เกณฑ์ | 0 | 1 | 2 |
|---|---|---|---|
| Business goal | ไม่ชัด | ชัดแต่ไม่วัดผล | ชัด มี owner และ KPI |
| Workflow logic | ขาดหลายขั้น | มี happy path | มีครบและมี exception path |
| AI reasoning | ไม่มีเหตุผลให้ใช้ AI | AI task กว้าง | ระบุ judgment/evidence ชัด |
| Decision boundary | AI ทำทุกอย่าง | มี human review บางส่วน | แยก may/must not ชัด |
| Business value | อ้างทั่วไป | มี KPI 1 ด้าน | มี speed, quality และ risk/outcome |

คะแนนเต็ม 10 จุด ใช้เพื่อ feedback ไม่ใช่แข่งขันว่าใคร “ใช้ AI มากที่สุด”

## ✅ Checkpoint

- [ ] ตอบครบ 9 คำถาม
- [ ] Workflow มี Trigger → Input → AI Reasoning → Decision → Action
- [ ] มี Human-in-the-loop
- [ ] มีอย่างน้อย 2 risks
- [ ] มี KPI ที่วัด quality ไม่ใช่ speed อย่างเดียว

## 🏁 Completed

ทีมได้แบบออกแบบ Agentic Workflow ที่เชื่อมความสามารถของ AI กับ business process, decision rights, risk และ measurable value

---

[← Previous: Lab 2](../03-build-agentic-workflow/README.md) · [Home](../README.md) · [Next: Responsible Agentic AI →](../05-responsible-agentic-ai/README.md)
