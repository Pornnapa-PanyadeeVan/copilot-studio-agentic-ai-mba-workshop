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
| `l2-01-form-title.png` | Google Forms editor | ชื่อ Form, คำเตือนข้อมูลจำลอง และคำถาม 4 ข้อ | Lab 2 L2-01 |
| `l2-02-form-preview.png` | Google Forms preview | หน้าผู้กรอกและ required fields | Lab 2 L2-02 |
| `l2-03-link-to-sheets.png` | Google Forms responses | ปุ่ม Link to Sheets และชื่อ Business Request Log | Lab 2 L2-03 |
| `l2-04-sheet-13-columns.png` | Google Sheets | Headers A–M ตั้งแต่ Timestamp ถึง Follow-up Status | Lab 2 L2-04 |
| `l2-05-api-key-redacted.png` | Google AI Studio | จุดสร้าง key โดยปิด key/project/account | Lab 2 L2-05 |
| `l2-06-make-empty-scenario.png` | Make | Scenario ว่าง ชื่อ Lab 2 และ Scheduling OFF | Lab 2 L2-06 |
| `l2-07-watch-new-rows-settings.png` | Make | Watch New Rows settings และ range/limit | Lab 2 L2-07 |
| `l2-08-gemini-connection-redacted.png` | Make | Gemini connection โดยไม่เห็น key | Lab 2 L2-08 |
| `l2-09-gemini-prompt-mapping.png` | Make | Prompt และ mapping tokens จาก Sheet | Lab 2 L2-09 |
| `l2-10-json-data-structure.png` | Make | JSON structure/output 4 fields | Lab 2 L2-10 |
| `l2-11-router-filters.png` | Make | HIGH และ MEDIUM/LOW filter conditions | Lab 2 L2-11 |
| `l2-12-high-update-row.png` | Make | HIGH Update a Row mappings และ statuses | Lab 2 L2-12 |
| `l2-13-medium-low-update-row.png` | Make | MEDIUM/LOW Update a Row mappings | Lab 2 L2-13 |
| `l2-14-high-gmail.png` | Make Gmail | Subject/body mapping เฉพาะ HIGH | Lab 2 L2-14 |
| `l2-15-complete-scenario.png` | Make | Scenario Lab 2 ครบทุก module และ Scheduling OFF | Lab 2 L2-15 |
| `l2-16-high-run-history.png` | Make run history | HIGH bundle ผ่าน HIGH route เท่านั้น | Lab 2 L2-16 |
| `l2-17-sheet-test-results.png` | Google Sheets | HIGH/MEDIUM/LOW สามแถวและผลในแถวเดิม | Lab 2 L2-17 |
| `l3-01-restricted-drive-folder.png` | Google Drive | HIGH-Follow-up และ General access = Restricted | Lab 3 L3-01 |
| `l3-02-new-report-scenario.png` | Make | Scenario Lab 3 ว่างและ Scheduling OFF | Lab 3 L3-02 |
| `l3-03-search-high-row.png` | Make | Search Rows filters BR-001 + HIGH และ Row number output | Lab 3 L3-03 |
| `l3-04-report-prompt-mapping.png` | Make Gemini | HIGH report prompt และ source mappings | Lab 3 L3-04 |
| `l3-05-draft-report-output.png` | Make run history | DRAFT banner, Request ID และ Human Review | Lab 3 L3-05 |
| `l3-06-report-validation-filter.png` | Make | Draft report passed filter 4 conditions | Lab 3 L3-06 |
| `l3-07-create-file-from-text.png` | Make Google Drive | Create a File from Text และ Convert to Docs | Lab 3 L3-07 |
| `l3-08-download-pdf.png` | Make Google Drive | Document File ID และ PDF conversion | Lab 3 L3-08 |
| `l3-09-upload-pdf.png` | Make Google Drive | Restricted folder, PDF filename และ binary data | Lab 3 L3-09 |
| `l3-10-update-follow-up-row.png` | Make Google Sheets | Row number, report link และ Follow-up OPEN | Lab 3 L3-10 |
| `l3-11-optional-report-email.png` | Make Gmail | DRAFT email และ optional PDF attachment | Lab 3 L3-11 |
| `l3-12-complete-report-scenario.png` | Make | Scenario Lab 3 ครบทุก module และ Scheduling OFF | Lab 3 L3-12 |
| `l3-13-final-pdf-and-tracker.png` | Google Drive + Sheets | PDF DRAFT และ BR-001 tracker ที่อัปเดตแล้ว | Lab 3 L3-13 |
| `15-line-demo.png` | LINE OA + Make | Channel → Webhook → Make | Instructor demo |
| `l4-01-goal-and-team-roles.png` | Notes/worksheet | Goal, Operator, Reviewer และ no external action | Lab 4 L4-01 |
| `l4-02-dedicated-project-folder.png` | Finder/File Explorer | Dedicated project ที่มี input/ และ outputs/ | Lab 4 L4-02 |
| `l4-03-input-dataset-preview.png` | Text preview | BR-001 ถึง BR-004 และ simulated-data notice | Lab 4 L4-03 |
| `l4-04-select-new-project.png` | Google Antigravity | Select Project → New Project | Lab 4 L4-04 |
| `l4-05-add-one-project-folder.png` | Google Antigravity | Dedicated folder เพียงหนึ่งรายการ | Lab 4 L4-05 |
| `l4-06-project-review-settings.png` | Google Antigravity | Planning/Request Review, terminal review และ isolation | Lab 4 L4-06 |
| `l4-07-new-planning-conversation.png` | Google Antigravity | Project ที่ถูกเลือกและ Planning Mode | Lab 4 L4-07 |
| `l4-08-bounded-task-prompt.png` | Google Antigravity | Project boundary, prohibited actions และ deliverables | Lab 4 L4-08 |
| `l4-09-implementation-plan-review.png` | Google Antigravity Artifact | Plan, output allowlist และ Proceed gate | Lab 4 L4-09 |
| `l4-10-task-list-before-execution.png` | Google Antigravity Artifact | Task List ไม่เกิน 5 ขั้นก่อน execution | Lab 4 L4-10 |
| `l4-11-permission-review.png` | Google Antigravity | Permission dialog ที่อ่าน target/action ได้ | Lab 4 L4-11 |
| `l4-12-task-progress-file-changes.png` | Google Antigravity | Task progress และ changes เฉพาะ outputs/ | Lab 4 L4-12 |
| `l4-13-output-file-tree.png` | Google Antigravity | Output files หลัก 4 รายการ | Lab 4 L4-13 |
| `l4-14-request-triage-results.png` | Markdown artifact | 4 Request IDs และผล HIGH/MEDIUM/LOW | Lab 4 L4-14 |
| `l4-15-high-report-follow-up-index.png` | Markdown artifacts | BR-001 DRAFT report, OPEN status และ index | Lab 4 L4-15 |
| `l4-16-validation-walkthrough.png` | Google Antigravity Artifact | Validation summary, Walkthrough และ Human Review | Lab 4 L4-16 |

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
