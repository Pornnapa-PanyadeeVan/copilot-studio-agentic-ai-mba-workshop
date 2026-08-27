# 05 — MBA Agentic AI Challenge

[← Previous: Lab 3](../04-generate-management-report/README.md) · [Home](../README.md) · [Next: Responsible AI →](../06-responsible-agentic-ai/README.md)

🎯 **Goal**  ออกแบบ Agentic AI use case ที่เชื่อม Business Goal, Reasoning, Decision, Action, Data, Insight และ Human Oversight

⏱ **Estimated Time**  15 นาที

👥 **Team**  3–4 คน (ประมาณ 13–17 ทีมสำหรับผู้เรียน 50 คน)

📋 **Deliverable**  [Agentic AI Design Worksheet](worksheet.md) หนึ่งชุดต่อทีม + pitch 60 วินาที

## เลือกหนึ่ง Use Case

- Customer Complaint Management
- Sales Lead Qualification
- Purchase Request
- Invoice Processing
- Employee Request
- Email Prioritization
- Customer Review Management
- Recruitment Screening

หรือกรณีธุรกิจอื่นที่ผู้สอนอนุมัติและใช้ข้อมูลจำลองได้

## Design Flow

```text
Goal
↓
Trigger
↓
Input
↓
AI Reasoning
↓
Decision
↓
Action
↓
Data / Memory
↓
Management Insight
```

## 📌 Step 1 — Define Business Value (3 นาที)

ตอบให้ชัด:

1. Business Goal คืออะไร?
2. ใครเป็นผู้ได้รับประโยชน์?
3. ปัจจุบันเสียเวลา ต้นทุน รายได้ หรือคุณภาพเท่าใด?
4. KPI ใดบอกว่าระบบดีขึ้น?

ตัวอย่าง KPI:

- Response time ลดลง
- Backlog ลดลง
- Escalation accuracy เพิ่มขึ้น
- Revenue conversion เพิ่มขึ้น
- Rework/error rate ลดลง
- Manager review time ลดลง

💡 **Why This Matters**  “ใช้ AI” ไม่ใช่ Business Goal ต้องผูกกับผลลัพธ์ที่วัดได้

✅ **Checkpoint**  Goal เป็นประโยคที่มี outcome และ stakeholder

## 📌 Step 2 — Map the Agentic System (5 นาที)

ตอบคำถาม:

1. What triggers the workflow?
2. What data is required?
3. What must AI reason about?
4. What decision can AI make?
5. What action can the system take?
6. What data should be stored?
7. What report or insight can management receive over time?

### 📋 Copy This Canvas

```text
Goal:
Trigger:
Input:
AI Reasoning:
Decision:
Action:
Data / Memory:
Management Insight:
```

💡 **Why This Matters**  Canvas แยก AI reasoning ออกจาก rule-based routing และแยก recommendation ออกจาก real action

✅ **Checkpoint**  Action เปลี่ยนสถานะในโลกธุรกิจจริง ไม่ใช่เพียงสร้างข้อความ

## 📌 Step 3 — Add Human Oversight and Risk (4 นาที)

ตอบ:

1. Where should a human remain in the loop?
2. What could go wrong?
3. Action ใด reversible และ action ใด high-impact?
4. ต้องเก็บ audit trail อะไร?
5. ใครเป็น accountable owner?

### Risk Prompts

- AI อาจ hallucinate ข้อมูลใด?
- Decision อาจไม่เป็นธรรมกับใคร?
- Permission กว้างเกินไปหรือไม่?
- ถ้า connector หยุด ระบบจะทำอย่างไร?
- ผู้ใช้จะ override หรือ appeal ได้หรือไม่?

⚠️ **Common Problem**  อย่าให้ AI อนุมัติการเงิน ลงโทษพนักงาน ให้คำตัดสินกฎหมาย/compliance หรือจัดการข้อมูลอ่อนไหวโดยไม่มี Human Approval

✅ **Checkpoint**  มีอย่างน้อยหนึ่ง approval gate และหนึ่ง fallback

## 📌 Step 4 — Prepare a 60-second Pitch (3 นาที)

ใช้รูปแบบ:

```text
Our business problem is...
The system observes...
The AI reasons about...
It decides...
It can automatically...
A human must approve...
It stores...
Management learns...
We measure value by...
```

## 🧪 Team Review Test

ให้ทีมข้าง ๆ ถาม 3 ข้อ:

1. ส่วนใดเป็น AI reasoning จริง?
2. Action ใดเกิดขึ้นจริงและมีความเสี่ยงเท่าใด?
3. หาก AI ผิด คนหยุดหรือแก้ระบบได้อย่างไร?

## 💬 Discussion

- Use case นี้เป็น automation, AI-assisted workflow หรือ Agentic AI ระดับใดบน autonomy spectrum?
- การเพิ่ม autonomy อีกหนึ่งระดับให้ value เพิ่มจริงหรือแค่เพิ่ม risk?
- Data สะสมจะสร้าง Management Insight อะไรที่คำร้องเดี่ยวให้ไม่ได้?

## 🏁 Completed

- [ ] Business Goal และ KPI ชัด
- [ ] Trigger/Input/Reasoning/Decision/Action ครบ
- [ ] ระบุ Data/Memory และ Management Insight
- [ ] มี Human-in-the-loop, risk และ fallback
- [ ] พร้อม pitch ภายใน 60 วินาที

---

[← Previous: Lab 3](../04-generate-management-report/README.md) · [Home](../README.md) · [Next: Responsible AI →](../06-responsible-agentic-ai/README.md)
