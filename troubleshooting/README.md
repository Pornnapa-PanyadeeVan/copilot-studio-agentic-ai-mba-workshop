# Troubleshooting Guide

[← Home](../README.md) · [Instructor Checklist](../templates/instructor-checklist.md)

ทุกหัวข้อมี `Problem → Likely Cause → Quick Fix → Instructor Fallback` เพื่อให้ Workshop เดินต่อได้ภายใน 3 ชั่วโมง

> **UI MAY VARY:** ใช้ชื่อเมนูที่เห็นจริงในบัญชีและเลือก function เทียบเท่า อย่าเปิด paid tier เพียงเพื่อแก้ปัญหาในห้อง

## Cannot access Google AI Studio

| | |
|---|---|
| **Problem** | เปิด Google AI Studio ไม่ได้, redirect loop, service unavailable หรือบัญชีไม่มีสิทธิ์ |
| **Likely Cause** | Account/age/country/admin restriction, browser cookie, network หรือ service availability |
| **Quick Fix** | ตรวจ account ที่ sign in, ใช้ browser profile/incognito ที่ได้รับอนุญาต, refresh และตรวจ network; อย่าใช้ข้อมูลจริง |
| **Instructor Fallback** | จับคู่กับผู้เรียนที่เข้าได้ หรือให้ดู Instructor screen แล้วใช้ expected outputs/prompts ใน repository |

## System Instructions not visible

| | |
|---|---|
| **Problem** | ไม่พบพื้นที่ System Instructions |
| **Likely Cause** | Panel ถูกพับ, session/mode ต่างกัน หรือ UI rollout เปลี่ยน |
| **Quick Fix** | หา run/model settings หรือ function ที่กำหนด persistent model behavior ตาม [AI Studio quickstart](https://ai.google.dev/gemini-api/docs/ai-studio-quickstart) |
| **Instructor Fallback** | Paste System Instructions ไว้ส่วนต้นของ Prompt พร้อม delimiter แล้วทำ test ใน session ใหม่ อธิบายว่าคำสั่งไม่ได้ persistent แบบเดียวกัน |

## Gemini output not in expected format

| | |
|---|---|
| **Problem** | ขาดหัวข้อ, ตอบยาว, Priority ไม่ใช่ค่าเดียว หรือภาษาไม่ตรง |
| **Likely Cause** | Instruction ไม่ครบ, chat context รบกวน หรือ model ตีความ output format ไม่ชัด |
| **Quick Fix** | ย้ำ exact format/allowed values/Thai output แล้วเริ่ม session ใหม่; ลดคำสั่งที่ขัดกัน |
| **Instructor Fallback** | ใช้ expected output ตัวอย่างและให้ผู้เรียนตรวจว่าแต่ละ field มาจาก rule ใด |

## Cannot create API key

| | |
|---|---|
| **Problem** | ไม่มีตัวเลือกสร้าง key, permission denied หรือหน้าจอขอ billing |
| **Likely Cause** | Account/admin/country/project restriction หรือ free-tier eligibility ต่างกัน |
| **Quick Fix** | ตรวจบัญชีและหน้าจัดการ key; ใช้ตัวเลือก free ที่บัญชีมี; ไม่เปิด billing เพื่อ Workshop |
| **Instructor Fallback** | Lab 1 ต่อได้โดยไม่มี key; Lab 2 ใช้ [fallback JSON](../03-build-agentic-workflow/prompts.md#fallback-json) หรือ Instructor scenario โดยไม่แชร์ key |

## Gemini API quota issue

| | |
|---|---|
| **Problem** | Error `429`, quota exceeded, rate limit หรือ model unavailable |
| **Likely Cause** | 50 คน run พร้อมกัน, free-tier RPM/TPM/daily limit, preview model limit หรือ request ใหญ่เกิน |
| **Quick Fix** | หยุด 1–2 นาที, stagger team runs, ลด dataset/output, ใช้ model ฟรีที่ available และไม่ retry รัว |
| **Instructor Fallback** | ใช้ Google AI Studio manual output หรือ prepared JSON/report แล้วทำ Router/Action ต่อ |

## Make cannot connect to Gemini

| | |
|---|---|
| **Problem** | Connection rejected, authentication error หรือ Gemini action run ไม่ผ่าน |
| **Likely Cause** | Key ผิด/หมดอายุ/ถูก block, model unavailable, quota หรือ connection configuration |
| **Quick Fix** | สร้าง connection ใหม่ด้วย key ของตนเอง ตรวจ key/model/quota และดู error detail โดยไม่แชร์ secret |
| **Instructor Fallback** | ตัด AI step ชั่วคราวแล้วป้อน fallback JSON เข้า parsing/Router เพื่อรักษา Learning Objective |

## Make cannot connect to Google Sheets

| | |
|---|---|
| **Problem** | OAuth fail, ไม่เห็น Spreadsheet/Sheet หรือ permission denied |
| **Likely Cause** | Sign in ผิด account, admin blocks OAuth, file ownership/permission หรือ stale connection |
| **Quick Fix** | ตรวจ Google account, เปิด Sheet โดยตรง, reconnect และเลือก file ของตนเอง |
| **Instructor Fallback** | แสดง mapping บน Scenario แล้ว paste output ลง prepared Sheet ด้วยตนเอง |

## Router condition does not match

| | |
|---|---|
| **Problem** | Bundle ไม่เข้า HIGH/MEDIUM/LOW route |
| **Likely Cause** | Mapping ผิด field, lowercase, whitespace หรือ filter ใช้ค่าที่ไม่ตรง |
| **Quick Fix** | ดู parsed `priority`, trim/normalize และใช้ exact match กับ `HIGH`, `MEDIUM`, `LOW` |
| **Instructor Fallback** | ใช้ prepared JSON ที่ priority สะอาด แล้วสาธิตทีละ route |

## Priority contains extra text

| | |
|---|---|
| **Problem** | ค่าเป็น `Priority: HIGH`, `HIGH because...` หรือมี code fence |
| **Likely Cause** | Prompt ไม่บังคับ schema หรือ map จาก full response แทน parsed field |
| **Quick Fix** | ใช้ JSON prompt, ย้ำ allowed values และ map `priority` หลัง parse ไม่ใช้ full text |
| **Instructor Fallback** | แก้ค่าใน fallback JSON เพื่อสาธิต Router และอภิปรายว่าทำไม structured output สำคัญ |

## JSON cannot parse

| | |
|---|---|
| **Problem** | JSON parser error หรือไม่มี 4 fields |
| **Likely Cause** | Markdown fence, single quotes, trailing comma, ข้อความก่อน/หลัง JSON หรือ output ถูกตัด |
| **Quick Fix** | ตรวจ raw output, ย้ำ `Return ONLY valid JSON`, ลด verbosity และ run ใหม่หนึ่งครั้ง |
| **Instructor Fallback** | ใช้ [valid fallback JSON](../03-build-agentic-workflow/prompts.md#fallback-json) แล้วทำขั้นตอนถัดไป |

## Google Sheet does not receive row

| | |
|---|---|
| **Problem** | Scenario ผ่านแต่ไม่มี row หรือ row อยู่ผิด Sheet |
| **Likely Cause** | Action ไม่ได้ run, route ไม่ match, เลือก Spreadsheet/Sheet ผิด, header changed หรือ permission |
| **Quick Fix** | เปิด run history ตาม bundle, ตรวจ selected file/tab และ refresh column mapping |
| **Instructor Fallback** | Paste row ด้วยตนเองและให้ผู้เรียนวาด mapping Trigger/AI fields → 8 Sheet columns |

## Gmail connection unavailable

| | |
|---|---|
| **Problem** | OAuth denied, send action unavailable หรือ policy block |
| **Likely Cause** | Google Workspace admin policy, account type, connection scope หรือ Make plan/UI difference |
| **Quick Fix** | ใช้บัญชีของตนเองที่อนุญาต ส่งถึงตนเอง และ reconnect โดยอ่าน permission ก่อนยอมรับ |
| **Instructor Fallback** | ข้าม email; เก็บ PDF/Drive link และสร้าง email draft text ถือว่าผ่าน Lab 3 |

## PDF cannot generate

| | |
|---|---|
| **Problem** | ได้ text/link แทน PDF, file 0 bytes หรือเปิดไม่ได้ |
| **Likely Cause** | ยังไม่ได้ export binary, document ID ผิด, conversion action/format ไม่รองรับ |
| **Quick Fix** | ตรวจ document ก่อน แล้วเลือก function export/convert เป็น PDF; ตรวจ filename และ file data mapping |
| **Instructor Fallback** | Copy report ไป Google Docs แล้ว download/export PDF ด้วยตนเองตาม UI ปัจจุบัน |

## Google Drive permission issue

| | |
|---|---|
| **Problem** | หา folder ไม่พบ, upload denied หรือ link เปิดไม่ได้ |
| **Likely Cause** | ผิด account/Drive, folder ownership, insufficient scope หรือ shared-drive restriction |
| **Quick Fix** | ใช้ My Drive ของตนเอง สร้าง `Agentic-AI-Reports/Weekly-Reports` และ reconnect |
| **Instructor Fallback** | เก็บ PDF local ชั่วคราวและบันทึก intended Drive path ใน worksheet; ไม่เปิด public sharing |

## Report only summarizes individual requests

| | |
|---|---|
| **Problem** | รายงานไล่สรุป Record 1, 2, 3 แต่ไม่มี pattern/risk/insight |
| **Likely Cause** | Dataset เล็ก, ไม่มี theme ซ้ำ หรือ Prompt ไม่เน้น cross-record analysis |
| **Quick Fix** | ใช้ 10–20 sample rows ที่มี repeated themes และย้ำ `NOT to summarize each request separately` |
| **Instructor Fallback** | ใช้ Suggested Lab 3 Set ใน [sample data](../templates/sample-requests.md#suggested-lab-3-set) แล้วอภิปราย pattern ด้วยมือ |

## Workflow does not run

| | |
|---|---|
| **Problem** | Run once รออยู่, trigger ไม่เข้าหรือ Scenario หยุดกลางทาง |
| **Likely Cause** | Trigger ไม่ได้รับ event, schedule off, invalid connection, unmapped required field หรือ previous error |
| **Quick Fix** | เริ่มจาก trigger test ใหม่ ส่ง payload หลัง Scenario รอฟัง ตรวจ required fields และ run history จากซ้ายไปขวา |
| **Instructor Fallback** | เดิน architecture ด้วย prepared bundles ทีละขั้น: Input → JSON → Router → Sheet |

## Duplicate rows or alerts

| | |
|---|---|
| **Problem** | คำร้องเดียวเกิดหลาย row/email |
| **Likely Cause** | กด Run ซ้ำ, webhook redelivery, overlapping routes หรือ retry หลัง timeout |
| **Quick Fix** | ใช้ request/event ID, exact mutually exclusive filters และตรวจผลก่อน retry |
| **Instructor Fallback** | ลบ duplicate ในข้อมูลจำลอง แล้วอภิปราย idempotency และ audit trail |

## API key may have leaked

| | |
|---|---|
| **Problem** | Key ปรากฏใน screenshot, chat, Sheet, run input หรือ Git commit |
| **Likely Cause** | Paste ผิดที่หรือ connection ไม่เก็บเป็น secret |
| **Quick Fix** | หยุดใช้และ revoke/rotate key ทันที จากนั้นลบข้อมูลที่เปิดเผยตาม policy; อย่าคิดว่าการลบข้อความอย่างเดียวทำให้ key ปลอดภัย |
| **Instructor Fallback** | ใช้ prepared output ต่อ ห้ามแจก key ใหม่แบบ shared key |

## Cannot access Manus Agent Mode

| | |
|---|---|
| **Problem** | ไม่เห็น Agent Mode, เห็นเฉพาะ Chat Mode หรือบัญชีไม่เริ่ม task |
| **Likely Cause** | Free-plan entitlement, account rollout, region, queue หรือ mode availability เปลี่ยน |
| **Quick Fix** | ตรวจ mode/usage notice ที่บัญชีแสดงและใช้ Agent Mode Lite หาก available; ไม่เปิด paid mode เพื่อผ่าน Lab |
| **Instructor Fallback** | เปิด Instructor completed task หรือใช้ Chat Mode เพื่อเปรียบเทียบข้อจำกัด แล้วทำ architecture discussion ต่อ |

## Manus credits or queue unavailable

| | |
|---|---|
| **Problem** | Credits ไม่พอ, task อยู่ใน queue นาน หรือระบบเสนอ upgrade |
| **Likely Cause** | Task complexity, daily/monthly credit rules, concurrent demand หรือ Free-plan limit |
| **Quick Fix** | หนึ่ง task ต่อทีม ใช้ dataset 14 rows, no web research และ compact prompt; อย่า run ซ้ำโดยไม่ตรวจผลเดิม |
| **Instructor Fallback** | ใช้ recorded/completed Instructor run แล้วให้ทีม validate triage/report ด้วย source Request IDs |

## Manus cannot read the uploaded dataset

| | |
|---|---|
| **Problem** | Agent ไม่เห็นไฟล์, อ่านจำนวน records ผิด หรือข้าม Request IDs |
| **Likely Cause** | Upload ไม่สมบูรณ์, file context ไม่ถูกแนบ, table parsing หรือ task เริ่มก่อน upload เสร็จ |
| **Quick Fix** | ตรวจว่า `manus-lab-input.md` ปรากฏใน task และระบุให้ preserve 14 Request IDs โดยไม่เริ่ม task ใหม่ถ้าแก้ใน session เดิมได้ |
| **Instructor Fallback** | Paste dataset บางส่วนหรือใช้ Instructor task; ให้ทีมตรวจ row count และ missing IDs ด้วยตนเอง |

## Manus proposes a workflow or external action

| | |
|---|---|
| **Problem** | Agent เสนอสร้าง app, Workflow, schedule, integration, email หรือค้นเว็บ |
| **Likely Cause** | Goal กว้างเกินไปหรือข้อห้ามไม่เด่นพอ |
| **Quick Fix** | ใช้ [Boundary Correction Prompt](../06-manus-ai/prompts.md#boundary-correction-prompt) และหยุด task หากกำลังจะทำ external action |
| **Instructor Fallback** | ใช้ prepared artifacts ที่ analysis-only แล้วอภิปรายว่าทำไม boundary เป็นส่วนหนึ่งของ Agent design |

## Manus triage or report fails validation

| | |
|---|---|
| **Problem** | Row count ไม่ใช่ 14, total ไม่ตรง, Priority ผิด schema, pattern ไม่มี Request IDs หรืออ้างว่าทำ Action แล้ว |
| **Likely Cause** | Agent ข้าม record, dataset context หาย, hallucination หรือ validation ไม่ถูกทำ |
| **Quick Fix** | ตรวจด้วย checklist ใน Lab 4; ใช้ Validation Prompt เฉพาะเมื่อ credits พอ หรือแก้/annotate ด้วยมือ |
| **Instructor Fallback** | ให้ทีมทำ reviewer role ระบุ fail points และเปรียบเทียบกับ deterministic validation ใน Make |

## Escalation Rule

หากแก้ไม่สำเร็จภายใน 3 นาที ให้ใช้ fallback เพื่อรักษาเวลา Workshop:

```text
Full Automation
↓ fails
Manual AI + Workflow
↓ fails
Prepared JSON + Router
↓ fails
Paper/Sheet Simulation
```

---

[← Home](../README.md) · [Instructor Checklist](../templates/instructor-checklist.md)
