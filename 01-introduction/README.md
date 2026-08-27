# 01 — Introduction: จาก Generative AI สู่ Agentic AI

🎯 **Goal**  เข้าใจเส้นทางการเรียนรู้ คำศัพท์ และกรณีศึกษาเดียวที่จะใช้ตลอด Workshop

⏱ **Estimated Time**  25 นาที

> 📷 Screenshot needed:
> ภาพสไลด์หรือ whiteboard ที่แสดง `Generative AI → AI Agent → Agent + Tools → Workflow → Decision → Action → Agentic AI`

## 📌 Step 1 — เริ่มจากสิ่งที่คุ้นเคย: Generative AI

**Generative AI** รับ prompt แล้วสร้างเนื้อหา เช่น สรุปข้อความ เขียนอีเมล หรือสร้างไอเดีย

```text
Prompt → Model → Generated content
```

💡 **Why This Matters**  การสร้างคำตอบที่ดีมีคุณค่า แต่ยังไม่เท่ากับการรับผิดชอบผลลัพธ์ทางธุรกิจ ระบบอาจเพียง “ตอบ” โดยไม่ได้เลือกเครื่องมือ ตัดสินใจ หรือทำ Action ต่อ

✅ **Checkpoint**  ลองอธิบายด้วยประโยคเดียวว่า Generative AI ทำอะไร: “สร้างเนื้อหาจากข้อมูลและคำสั่งที่ได้รับ”

## 📌 Step 2 — เพิ่ม Goal, Instructions และ Tools: AI Agent

**AI Agent** ทำงานเพื่อเป้าหมาย โดยประสานองค์ประกอบสำคัญ:

- Goal — ต้องการให้งานสำเร็จแบบใด
- Instructions — กติกาและขอบเขต
- Context/Knowledge — ข้อมูลที่ใช้ประกอบ
- Reasoning — วิเคราะห์สถานการณ์
- Tools — อ่านหรือเปลี่ยนข้อมูลในระบบอื่น

```text
Goal + Instructions + Context + Tools
                  ↓
               AI Agent
```

ใน Lab 1 เราจะสร้าง Agent ที่วิเคราะห์ Business Request แต่ผู้ใช้ยังต้องนำคำขอไปถามเองทุกครั้ง

💬 **Discussion**  ถ้า Agent เพียงตอบคำถามอย่างมีโครงสร้าง แต่ไม่เริ่มงานหรือทำ Action เอง เราควรเรียกว่า AI Agent หรือ Agentic AI?

## 📌 Step 3 — เชื่อม Agent เข้ากับ Workflow

Workflow ทำให้ขั้นตอนเกิดตามลำดับที่ตรวจสอบได้:

```text
Trigger → Input → AI Analysis → Decision → Action
```

ในกรณีศึกษานี้:

- **Trigger:** พนักงานส่ง Microsoft Form
- **Input:** ชื่อ แผนก คำขอ และวันที่ต้องการ
- **AI Analysis:** สรุปและจัด Priority
- **Decision:** HIGH, MEDIUM, LOW หรือ NEEDS CLARIFICATION
- **Action:** แจ้ง Teams หรือบันทึก Excel

💡 **Why This Matters**  Workflow เปลี่ยนคำตอบของ AI ให้เป็นกระบวนการธุรกิจ แต่ workflow ที่เดินตามกฎตายตัวไม่ได้เป็น Agentic AI โดยอัตโนมัติ

## 📌 Step 4 — Agentic AI เป็นวงจร ไม่ใช่เพียงเส้นตรง

ใช้โมเดลนี้ในการอภิปราย:

```text
Goal
 ↓
Observe
 ↓
Reason
 ↓
Decide
 ↓
Act
 ↓
Observe
 ↺
```

| ขั้น | คำถามทางธุรกิจ |
|---|---|
| Goal | ต้องการผลลัพธ์อะไร และใครเป็นเจ้าของผลลัพธ์? |
| Observe | ระบบเห็นข้อมูลหรือเหตุการณ์อะไร? |
| Reason | ต้องตีความหรือเปรียบเทียบอะไร? |
| Decide | ระบบได้รับอนุญาตให้ตัดสินใจแค่ไหน? |
| Act | ทำอะไรใน Teams, Excel หรือระบบงาน? |
| Observe again | รู้ได้อย่างไรว่า Action สำเร็จ และควรแก้ไขอะไร? |

### Autonomy is a spectrum

| ระดับ | ตัวอย่าง | บทบาทมนุษย์ |
|---|---|---|
| AI-assisted | AI สรุปคำขอ | มนุษย์เริ่มและตัดสินใจทั้งหมด |
| Agent | Agent วิเคราะห์เป้าหมายตาม instructions | มนุษย์เริ่มงานและตรวจผล |
| Agentic workflow | Event เริ่มงาน, AI วิเคราะห์, workflow ตัดสินและทำ Action | มนุษย์ออกแบบกติกาและจัดการ exception |
| Higher autonomy | ระบบสังเกตผลและปรับแผนภายใน guardrails | มนุษย์กำกับ KPI, permission และเหตุการณ์เสี่ยงสูง |

## เปรียบเทียบ 4 แนวคิด

| แนวคิด | จุดเด่น | มี Reasoning? | ทำ Action? | เริ่มเองได้? |
|---|---|---:|---:|---:|
| AI Automation | กฎและขั้นตอนคงที่ | ไม่จำเป็น | ได้ | ได้เมื่อมี trigger |
| AI Agent | ทำงานตาม Goal/Instructions และใช้ tools ได้ | มี | อาจมี | อาจต้องให้มนุษย์เริ่ม |
| Agentic Workflow | ผสาน AI judgment กับ workflow ที่ตรวจสอบได้ | มีในบางขั้น | มี | ได้เมื่อมี event |
| Agentic AI | วงจร Observe–Reason–Decide–Act–Observe ภายใต้ guardrails | มี | มี | มีระดับ autonomy สูงกว่า |

> [!CAUTION]
> อย่าเรียกทุก automated workflow ว่า Agentic AI หากไม่มี AI reasoning, decision boundary, feedback หรือความสามารถปรับการทำงานตามบริบท ระบบนั้นอาจเป็น automation ที่ดี—ซึ่งก็มีคุณค่าทางธุรกิจ—แต่ไม่จำเป็นต้องเป็น Agentic AI

## Business Request Management

### Input

- Requester Name
- Department
- Business Request
- Required Date

### Required output

```text
Summary:
Priority:
Reason:
Recommended Action:
```

### Priority policy

| Priority | ใช้เมื่อ |
|---|---|
| HIGH | ลูกค้าหรือรายได้กระทบทันที, critical operation, deadline ≤ 24 ชั่วโมง, compliance/reputation risk ร้ายแรง |
| MEDIUM | สำคัญแต่ยังไม่วิกฤต, deadline ภายในหลายวัน, ต้องการ management attention |
| LOW | งาน routine, general information, ไม่มีผลกระทบทันที |
| NEEDS CLARIFICATION | ข้อมูลไม่พอตัดสิน; ห้ามเดาความเร่งด่วน |

🧪 **Test — 2-minute classification warm-up**

ให้ผู้เรียนโหวต Priority:

> “ลูกค้ารายใหญ่ชำระเงินแล้ว แต่ระบบยังระงับบัญชี ทำให้ใช้งานไม่ได้ ต้องแก้วันนี้”

คำตอบที่คาดหวัง: **HIGH** เพราะมี immediate customer impact และ financial/reputation risk

> “ขอวิธีเปลี่ยนรูปโปรไฟล์ใน Teams ไม่มี deadline”

คำตอบที่คาดหวัง: **LOW** เพราะเป็น general information และไม่มี immediate business impact

## 💬 Discussion — AI ควรตัดสินใจได้แค่ไหน?

ถามกลุ่ม:

1. ถ้า Agent จัด Priority ผิด ใครได้รับผลกระทบ?
2. คำขอใดควรส่งให้มนุษย์เสมอ?
3. ความเร็วหรือความถูกต้องสำคัญกว่ากันในแต่ละกรณี?
4. เราจะรู้ได้อย่างไรว่าระบบสร้างคุณค่าทางธุรกิจจริง?

## 🏁 Completed

คุณพร้อมไป Lab 1 เมื่อสามารถอธิบายได้ว่า:

- Generative AI สร้างเนื้อหา
- AI Agent ทำงานเพื่อ Goal โดยใช้ Instructions และ Tools
- Agentic AI ต้องพิจารณา Reasoning, Decision, Action, Feedback และ Guardrails ร่วมกัน

---

[← Home](../README.md) · [Next: Lab 1 — Build an AI Agent →](../02-build-ai-agent/README.md)
