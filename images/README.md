# Screenshot Guide

[← Home](../README.md)

Repository นี้ไม่สร้าง screenshot ปลอม เพราะ Google AI Studio, Make และ Google Workspace เปลี่ยน UI ได้ตามบัญชี ประเทศ เวอร์ชัน และ rollout ผู้สอนควรถ่ายภาพจากบัญชี workshop จริงก่อนสอน

## หลักการ

- ปิด API key, email, user ID, Sheet ID, webhook URL และข้อมูลส่วนบุคคลทุกครั้ง
- ใช้ข้อมูลจำลองเท่านั้น
- Crop เฉพาะส่วนที่ช่วยผู้เรียนหา function
- ใส่วันที่ถ่ายและข้อความ `UI MAY VARY` ใน caption
- ใช้ alt text ที่บอกหน้าที่ ไม่ยึดกับชื่อเมนูมากเกินไป
- เก็บไฟล์ภาพในโฟลเดอร์นี้และใช้ชื่อด้านล่าง

## Screenshot Checklist

| ชื่อไฟล์แนะนำ | หน้าจอ | จุดที่ควรเห็น | ใช้ใน |
|---|---|---|---|
| `01-ai-studio-start.png` | Google AI Studio | พื้นที่เริ่ม prompt โดยไม่มีข้อมูลส่วนตัว | Lab 1 Step 1 |
| `02-system-instructions.png` | Google AI Studio | System Instructions area | Lab 1 Step 3 |
| `03-agent-test-output.png` | Google AI Studio | Summary, Priority, Reason, Action | Lab 1 test |
| `04-ai-studio-api-key-redacted.png` | API key page | จุดสร้าง key โดยปิดค่าของ key | Lab 2 Step 2 |
| `05-sheet-columns.png` | Google Sheets | 8 columns ของ Business Request Log | Lab 2 Step 1 |
| `06-make-new-scenario.png` | Make | Scenario canvas | Lab 2 Step 3 |
| `07-make-gemini-connection.png` | Make | Connection dialog โดยไม่เห็น key | Lab 2 Step 4 |
| `08-make-json-output.png` | Make run history | JSON 4 fields | Lab 2 Step 5 |
| `09-make-router.png` | Make | HIGH/MEDIUM/LOW routes | Lab 2 Step 6 |
| `10-sheet-result.png` | Google Sheets | Synthetic rows | Lab 2 checkpoint |
| `11-report-flow.png` | Make | Read → Gemini → Document → PDF → Drive → Gmail | Lab 3 overview |
| `12-management-report.png` | Google Docs/PDF | Section headings ของ report | Lab 3 checkpoint |
| `13-drive-report.png` | Google Drive | Weekly-Reports folder และไฟล์จำลอง | Lab 3 Step 6 |
| `14-email-test.png` | Gmail | อีเมลถึงตนเอง ไม่มี address จริง | Lab 3 Step 7 |
| `15-line-demo.png` | LINE OA + Make | Channel → Webhook → Make | Instructor demo |
| `16-manus-agent-mode.png` | Manus | Agent Mode/credit notice โดยปิด account details | Lab 4 Step 2 |
| `17-manus-dataset-upload.png` | Manus | `manus-lab-input.md` และจำนวน 14 records | Lab 4 Step 3 |
| `18-manus-task-artifacts.png` | Manus | Execution plan, triage และ report โดยไม่มีข้อมูลจริง | Lab 4 validation |

## รูปแบบ Caption

```text
📷 Screenshot: Google AI Studio System Instructions area
Captured: YYYY-MM-DD
UI MAY VARY
```

## Alt Text Example

```text
Alt text: Google AI Studio prompt workspace showing the area used to define system instructions; account details are hidden.
```

## ห้ามปรากฏในภาพ

- Gemini API key หรือบางส่วนของ key
- LINE channel secret/access token
- Make webhook URL
- Email จริง รายชื่อลูกค้า หรือข้อมูลพนักงาน
- Sheet/Drive ที่มีข้อมูลส่วนบุคคล
- Browser password manager หรือ notification ที่เปิดเผยข้อมูล

---

[← Home](../README.md)
