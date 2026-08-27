# Instructor Checklist — 50-person Workshop

[← Home](../README.md) · [Troubleshooting](../troubleshooting/README.md)

ใช้ checklist นี้ก่อนสอน `Build Your First Agentic AI for Business` ทุกครั้ง เพราะ free-tier eligibility, quota และ UI เปลี่ยนได้

## 7–14 วันก่อนสอน

### Account and Access

- [ ] ผู้เรียนมี Google Account ที่ได้รับอนุญาตให้ใช้บริการภายนอก
- [ ] ทดสอบ [Google AI Studio](https://aistudio.google.com/) ด้วยบัญชีประเภทเดียวกับผู้เรียน
- [ ] ทดสอบว่ามองเห็นพื้นที่ System Instructions
- [ ] ทดสอบ Make account creation/verification
- [ ] ทดสอบ Google Sheets, Google Docs, Google Drive และ Gmail
- [ ] ตรวจว่าบัญชีตัวอย่างสร้าง Gemini API key แบบ free tier ได้โดยไม่เปิด billing
- [ ] ตรวจ restrictions ของบัญชีโรงเรียน/องค์กรและประเทศ
- [ ] ไม่ใช้ instructor API key ร่วมกันทั้งห้อง

### Make Connections

- [ ] ทดสอบ connection ไป Gemini ด้วย key สำหรับ demo
- [ ] ทดสอบ Google Sheets read/write
- [ ] ทดสอบ Router/filters ด้วย exact Priority values
- [ ] ทดสอบการอ่านหลาย rows และ aggregate request data
- [ ] ทดสอบ document generation path ที่บัญชีปัจจุบันรองรับ
- [ ] ทดสอบ PDF export/conversion
- [ ] ทดสอบ Google Drive upload/save
- [ ] ทดสอบ Gmail ส่งถึงอีเมลทดสอบของผู้สอนเอง
- [ ] ปิด schedule ของ scenario หลังทดสอบ

### Free-tier and Capacity

- [ ] ตรวจ [Gemini API Pricing](https://ai.google.dev/gemini-api/docs/pricing)
- [ ] ตรวจ [Gemini API Rate Limits](https://ai.google.dev/gemini-api/docs/rate-limits)
- [ ] ตรวจ [Make Pricing/Credits](https://www.make.com/en/pricing)
- [ ] ยืนยันว่าไม่มี Lab บังคับ paid model, paid Make feature หรือ Cloud Billing
- [ ] จำกัด Lab 2 คนละ 3–5 Gemini requests
- [ ] จำกัด Lab 3 dataset 10–20 rows
- [ ] วางแผนกระจายเวลาสร้าง API keys ไม่ให้ 50 คนทำพร้อมกันวินาทีเดียว
- [ ] เตรียม quota/rate-limit fallback

## 2–3 วันก่อนสอน

### Materials

- [ ] เปิดลิงก์ทุก Lab จาก [README](../README.md)
- [ ] ตรวจ Previous / Home / Next navigation
- [ ] เตรียม [Sample Requests](sample-requests.md) อย่างน้อย 20 รายการ
- [ ] เตรียมสำเนา sample data ใน Sheet ของผู้สอน
- [ ] เตรียม fallback JSON จาก [Lab 2 Prompts](../03-build-agentic-workflow/prompts.md#fallback-json)
- [ ] เตรียม fallback management report จาก [Lab 3 Prompts](../04-generate-management-report/prompts.md)
- [ ] เตรียม blank Google Doc และ Drive folders สำหรับ fallback
- [ ] เตรียม PDF ตัวอย่างที่ไม่มีข้อมูลจริง
- [ ] เตรียม worksheet สำหรับ 13–17 ทีม
- [ ] เตรียม Exit Ticket

### Screenshots and Demo

- [ ] ถ่าย screenshot ตาม [Screenshot Guide](../images/README.md)
- [ ] ปิด API key, email, IDs และ webhook URLs ในทุกภาพ
- [ ] ใส่ `UI MAY VARY` และวันที่ถ่าย
- [ ] ทดสอบ flow สดหนึ่งรอบ HIGH/MEDIUM/LOW
- [ ] บันทึกภาพหรือวิดีโอ fallback ของ run ที่สำเร็จ
- [ ] หากสาธิต LINE OA ให้ใช้ demo account/channel เท่านั้น
- [ ] เตรียม LINE architecture-only fallback

### Room and Network

- [ ] Wi‑Fi รองรับ browser sessions ประมาณ 50 คน
- [ ] เตรียม QR/short link ไป repository
- [ ] แนะนำจับคู่ 2 คนต่อเครื่องหาก Wi‑Fi หรือ account จำกัด
- [ ] เตรียม projector scaling และ browser zoom
- [ ] มีช่องทางประกาศ “หยุด API test” เมื่อ quota เริ่มมีปัญหา
- [ ] แบ่งผู้ช่วยดูแลประมาณ 1 คนต่อผู้เรียน 12–15 คนหากทำได้

## วันสอน — ก่อนเริ่ม 60 นาที

- [ ] Sign in Google AI Studio และ Make ด้วย demo account
- [ ] ตรวจว่า model ที่เลือกยังมี free-tier access
- [ ] Run Lab 1 test case หนึ่งรายการ
- [ ] Run Lab 2 HIGH request end-to-end
- [ ] ตรวจ row ใน Business Request Log
- [ ] Run Lab 3 ด้วย sample data
- [ ] เปิด PDF จาก Drive
- [ ] ส่ง Gmail ถึงตนเองและเปิด attachment
- [ ] ตรวจ Make credit/quota dashboard
- [ ] เปิด browser tabs: repository, AI Studio, Make, Sheets, Drive, Gmail
- [ ] เปิด troubleshooting และ fallback files
- [ ] ลบผล demo เก่าที่อาจทำให้ผู้เรียนสับสน แต่ไม่ลบ audit ที่ต้องเก็บ

## Class Setup สำหรับ 50 คน

### Grouping

- [ ] ให้ผู้เรียนทำ Lab 1 รายบุคคลหรือคู่
- [ ] Lab 2–3 อนุญาตจับคู่เพื่อช่วยเรื่อง connection/quota
- [ ] MBA Challenge ทีมละ 3–4 คน
- [ ] กำหนดตัวแทนทีมเพียงหนึ่งคนกด Run ใน Make

### Timing Guardrails

- [ ] 00:25 เริ่ม Lab 1 ไม่ช้ากว่า 5 นาที
- [ ] 01:05 หยุด Lab 1 แม้บางคนใช้ fallback
- [ ] 01:15 เริ่ม Lab 2 พร้อมกันจาก architecture
- [ ] 01:40 ผู้ที่ API ยังไม่ผ่านเปลี่ยนเป็น fallback JSON
- [ ] 02:05 เริ่ม Lab 3 ด้วย sample data ทันที
- [ ] 02:20 ผู้ที่ PDF connector ไม่ผ่านใช้ manual document fallback
- [ ] 02:35 เริ่ม Challenge
- [ ] 02:50 หยุด pitch และเข้าสู่ Responsible AI

## Risk Register

| Risk | Early warning | Mitigation | Fallback |
|---|---|---|---|
| Gemini API rate limit | 429/quota messages หลายคน | ลด run, stagger teams, ใช้สั้นลง | Lab 1 manual AI + fallback JSON |
| Free-tier model unavailable | Model หาย/ขอ billing | ใช้ model ฟรีที่บัญชีแสดง | Instructor output/sample JSON |
| API key creation blocked | ไม่มี create option/permission | จับคู่กับผู้เรียนที่มีสิทธิ์โดยไม่แชร์ key | Instructor scenario หรือ manual simulation |
| Make module differences | หา action ตามชื่อไม่พบ | สอนตาม function และ screenshot วันที่ล่าสุด | Architecture card/manual mapping |
| Make account verification | เข้า builder ไม่ได้ | ตรวจล่วงหน้า/จับคู่ | ผู้เรียนออกแบบบน worksheet |
| Make credits low | dashboard ใกล้ limit | จำกัด 3 runs ปิด schedule | Use recorded run/sample output |
| Slow Wi‑Fi | หน้าโหลดช้า/timeouts | จับคู่ ลด tabs หยุด simultaneous runs | Instructor-led walkthrough |
| Google account restrictions | OAuth blocked | ใช้บัญชีที่สถาบันอนุญาต | Manual copy/paste path |
| Sheets connection fail | file/columns ไม่แสดง | refresh headers/connection | Paste rows manually |
| Gmail authorization fail | OAuth denied | ใช้ email ตนเอง/ตรวจ permission | Save Drive link only |
| PDF generation fail | ได้ text/link ไม่ใช่ PDF | ตรวจ export/binary path | Google Docs manual export |
| 50 API keys พร้อมกัน | throttling/verification delay | stagger 5 กลุ่ม | แชร์ผลผ่าน projector ไม่แชร์ key |
| Sensitive data ถูก paste | พบชื่อ/email จริง | หยุด run และลบจาก workspace/history ตาม policy | ใช้ sample dataset ใหม่ |

## Fallback Ladder

ใช้ระดับต่ำสุดที่ยังรักษา Learning Objective:

### Level A — Full Hands-on

```text
Input → Make → Gemini → Router → Sheet → Report → PDF → Drive → Gmail
```

### Level B — AI Manual, Workflow Hands-on

```text
Input → Google AI Studio → Copy JSON → Make Router → Sheet
```

### Level C — Prepared Output

```text
Prepared JSON → Make Router → Sheet → Prepared report data
```

### Level D — Manual Simulation

```text
Input card → Team applies AI rules → Decision card → Action card
→ Prepared data → Management insight discussion
```

> Workshop ต้องสำเร็จได้แม้ automation connectors fail ผู้เรียนยังต้องอธิบาย Goal, Reasoning, Decision, Action, Data และ Human Oversight

## Security Checklist

- [ ] ใช้ข้อมูลจำลองเท่านั้น
- [ ] ไม่ใส่ API key ใน GitHub, Prompt, Sheet หรือ screenshot
- [ ] ไม่มีอีเมลจริงใน repository; ใช้ `[Your Email]`
- [ ] ใช้ least-privilege connections
- [ ] ส่ง Gmail ถึงตนเองเท่านั้น
- [ ] Drive files private/restricted
- [ ] ปิด Scenario schedule หลังจบ
- [ ] Rotate/revoke demo key หลัง class หากไม่ใช้ต่อ
- [ ] ไม่บันทึกหน้าจอที่มี secret
- [ ] ไม่สาธิต high-impact automatic action

## หลังสอน

- [ ] ปิด scenario schedules/webhooks ที่ไม่ใช้
- [ ] ลบหรือ anonymize test data ตาม retention plan
- [ ] Rotate/revoke workshop API keys ที่ไม่ใช้
- [ ] ตรวจ Make credits/quota
- [ ] เก็บ feedback ว่า issue ใดเกิดบ่อย
- [ ] Update troubleshooting และ screenshots
- [ ] ตรวจลิงก์ free-tier/pricing ก่อนรอบถัดไป
- [ ] บันทึก UI/module ที่เปลี่ยน แต่หลีกเลี่ยงคำรับประกันชื่อเมนู

---

[← Home](../README.md) · [Troubleshooting](../troubleshooting/README.md)
