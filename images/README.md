# Images and Screenshot Checklist

Repository นี้ **ไม่สร้าง screenshot ปลอม** ผู้สอนควรถ่ายภาพจาก tenant ที่ใช้สอนจริง เพราะ Microsoft Copilot Studio และ Power Platform UI เปลี่ยนตาม environment, license และ rollout

## Screenshot standards

- ใช้บัญชี demo และข้อมูลจำลอง
- ปิดบังชื่อจริง อีเมล tenant ID environment ID connection ID และข้อมูลธุรกิจ
- เก็บภาพเฉพาะบริเวณที่ช่วยนำทาง
- ใส่วันที่ capture และ UI variant ใน alt text/caption
- ใช้ลูกศรหรือกรอบเน้นได้ แต่ห้ามเปลี่ยนข้อความของ UI
- หากมีทั้ง classic/new experience ให้เก็บสองภาพและระบุ variant

## Recommended filenames

```text
01-learning-path.png
02-environment-selector.png
03-create-agent.png
04-agent-name-description.png
05-agent-instructions.png
06-agent-preview-test.png
07-forms-fields.png
08-excel-table.png
09-flow-entry-points.png
10-forms-trigger-details.png
11-ai-analysis-action.png
12-priority-decision.png
13-teams-action.png
14-excel-add-row.png
15-flow-run-history.png
16-success-results.png
```

## Capture checklist

| File | Screen to capture | Crop/include | Lab placeholder |
|---|---|---|---|
| `01-learning-path.png` | Slide/whiteboard | Full learning path | Introduction |
| `02-environment-selector.png` | Copilot Studio Home | Environment selector + non-sensitive name | Lab 1 Before start |
| `03-create-agent.png` | Home/Agents | Agent tile or New agent | Lab 1 Step 1 |
| `04-agent-name-description.png` | Agent designer | Name + description | Lab 1 Step 2 |
| `05-agent-instructions.png` | Build/Overview | Instructions section, no tenant data | Lab 1 Step 3 |
| `06-agent-preview-test.png` | Preview/Test | One four-field response | Lab 1 Step 5 |
| `07-forms-fields.png` | Microsoft Forms | Four required fields | Lab 2 Step 1 |
| `08-excel-table.png` | Excel Online | Headers + table name | Lab 2 Step 2 |
| `09-flow-entry-points.png` | Copilot Studio + Power Automate | Workflows/Flows and Automated cloud flow | Lab 2 route choice |
| `10-forms-trigger-details.png` | Flow designer | Trigger + Get response details | Lab 2 Steps 4–5 |
| `11-ai-analysis-action.png` | Flow designer | Run a prompt/Run an agent + structured fields | Lab 2 Step 6 |
| `12-priority-decision.png` | Flow designer | HIGH/MEDIUM/LOW/Default branches | Lab 2 Step 7 |
| `13-teams-action.png` | Flow designer | Post as/Post in + redacted Team/Channel | Lab 2 Step 8 |
| `14-excel-add-row.png` | Flow designer | File, Table, field mapping | Lab 2 Step 9 |
| `15-flow-run-history.png` | Run history | Successful steps + timing, redacted IDs | Lab 2 Step 11 |
| `16-success-results.png` | Teams + Excel | Synthetic HIGH notification and MEDIUM/LOW rows | Wrap-up |

## Markdown pattern

เมื่อมีภาพจริงแล้ว แทน placeholder ด้วย:

```markdown
Alt text: Copilot Studio Create Agent screen, captured in the workshop tenant on YYYY-MM-DD
Image path: ../images/03-create-agent.png

> **UI MAY VARY:** หากไม่เห็นคำเดียวกัน ให้หา function สำหรับสร้าง Agent ใหม่
```

## Manual verification after UI updates

ก่อนสอนทุกครั้งให้ตรวจ:

- `Agent` vs `New agent` vs `Create agent`
- `Build/Overview` และตำแหน่ง Instructions
- `Preview` vs `Test your agent`
- `Flows`, `Workflows (preview)` และ `Agent flows`
- `Run a prompt` vs `Run an agent`
- New vs classic Power Automate designer
- Dynamic content picker icon/position
- Teams and Excel connector action names

---

[← Home](../README.md) · [Instructor Checklist](../templates/instructor-checklist.md) · [Troubleshooting](../troubleshooting/README.md)
