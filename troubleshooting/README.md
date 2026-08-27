# Troubleshooting Guide

ใช้กติกา **5-minute fallback**: หากเป็นปัญหา permission, license, environment หรือ connector และแก้ไม่ได้ภายใน 5 นาที ให้ใช้ Instructor fallback เพื่อรักษา learning outcome และเวลา Workshop

> [!IMPORTANT]
> **UI MAY VARY:** บันทึกชื่อ environment, ขั้นตอนที่ล้มเหลว และข้อความ error แบบไม่เปิดเผยข้อมูลลับ ห้าม paste token, connection ID, tenant ID หรือข้อมูลบุคคลลง repository

## Cannot access Copilot Studio

| Item | Detail |
|---|---|
| Problem | เปิด Copilot Studio ไม่ได้, redirect loop หรือเห็นหน้าไม่มีสิทธิ์ |
| Likely cause | ไม่มี license, admin policy, conditional access, wrong account หรือ region/environment restriction |
| Quick fix | ตรวจ work/school account, sign out/in, เปิด private window, ตรวจ license กับ instructor/admin และใช้ URL `https://copilotstudio.microsoft.com` |
| Instructor fallback | จับคู่กับ maker ที่เข้าได้; ให้ผู้เรียนทำ prompt review และทดสอบผ่าน demo agent ของผู้สอน |

## Cannot create Agent

| Item | Detail |
|---|---|
| Problem | `New agent` ไม่มี, disabled หรือ Save ไม่สำเร็จ |
| Likely cause | Wrong environment, security role, capacity, trial limit หรือ agent creation ถูก admin ปิด |
| Quick fix | ตรวจ environment, refresh Agents page, ลอง blank agent, ตรวจ required Name/Language และให้ admin ตรวจ maker permission |
| Instructor fallback | 1 agent ต่อทีม; ใช้ agent ที่ผู้สอนสร้างไว้ แล้วให้ผู้เรียนวิเคราะห์/ปรับ Instructions บนสำเนา worksheet |

## Cannot find Workflow

| Item | Detail |
|---|---|
| Problem | ไม่เห็น `Workflows`, `Flows`, `New agent flow` หรือ Forms trigger |
| Likely cause | Classic/new experience ต่างกัน, preview ไม่เปิด, harness ต่างกัน หรือ license จำกัด |
| Quick fix | หา function ที่สร้าง flow; ลอง Copilot Studio → Flows/Workflows; หากไม่มีให้เปิด Power Automate → Create → Automated cloud flow ใน environment เดียวกัน |
| Instructor fallback | ใช้ flow demo ของผู้สอน หรือวาด flow conceptually ใน [Challenge Worksheet](../04-mba-challenge/worksheet.md) |

## Microsoft Forms connector unavailable

| Item | Detail |
|---|---|
| Problem | ไม่พบ connector/trigger หรือ Form ไม่อยู่ใน Form Id |
| Likely cause | Connection ใช้คนละบัญชี, Form เป็นของ group/คนอื่น, DLP policy, admin consent หรือ connection หมดอายุ |
| Quick fix | สร้าง Form ด้วยบัญชีเดียวกับ flow, refresh connection, ตรวจ environment/DLP และเลือก `When a new response is submitted` + `Get response details` |
| Instructor fallback | ใช้ Manual trigger พร้อม text inputs หรือ copy Form response ไป Agent ด้วยตนเอง |

## Teams connector unavailable

| Item | Detail |
|---|---|
| Problem | ไม่พบ Team/Channel, connection error หรือ post ไม่สำเร็จ |
| Likely cause | ไม่มี membership/post permission, connection หมดอายุ, private channel limitation หรือ DLP policy |
| Quick fix | ใช้ standard channel ที่ผู้เรียนเป็น member, reauthenticate, เลือก `Post a message in a chat or channel`, ตรวจ Post as/Post in |
| Instructor fallback | แทน Teams action ด้วย Compose หรือบันทึก notification text ใน Excel แล้วให้ผู้สอน demo Teams action |

## Excel table not detected

| Item | Detail |
|---|---|
| Problem | File พบแต่ Table dropdown ว่าง หรือ `Add a row into a table` ล้มเหลว |
| Likely cause | Data เป็น cell range ไม่ใช่ table, workbook อยู่ local device, connection ไม่มีสิทธิ์, file lock หรือ table เพิ่งสร้าง |
| Quick fix | เก็บไฟล์ใน OneDrive for Business/SharePoint, ใช้ Format as Table, ตั้งชื่อ `BusinessRequestsTable`, save/close workbook แล้ว refresh action |
| Instructor fallback | ใช้ Compose เพื่อแสดง row ที่ควรบันทึก หรือใช้ workbook/table ที่ผู้สอนเตรียมไว้ |

## AI output cannot be used in Condition

| Item | Detail |
|---|---|
| Problem | Dynamic content ไม่มี Priority หรือมี output เป็นข้อความก้อนเดียว |
| Likely cause | Prompt output เป็น Text, schema ยังไม่บันทึก/ทดสอบ หรือเลือก token ผิด action |
| Quick fix | เปลี่ยนเป็น JSON/Structured output และกำหนด `summary`, `priority`, `reason`, `recommendedAction`; save และ test AI step ใหม่ |
| Instructor fallback | ใช้ Compose/ตัวแปร Priority ที่ผู้เรียนกรอกเอง แล้วสาธิต Decision branch โดยไม่เรียก AI |

## Priority text does not match HIGH exactly

| Item | Detail |
|---|---|
| Problem | AI แสดง HIGH แต่ flow ไปผิด branch |
| Likely cause | มีช่องว่าง, markdown, sentence เพิ่ม, case ต่าง หรือเลือก token ผิด |
| Quick fix | ใช้ structured field; บังคับ allowed values; ตรวจ run output; หาก text-only ใช้ `toUpper(trim(...))` ก่อนเทียบ `HIGH` |
| Instructor fallback | ใช้ sample Priority value แบบคงที่เพื่อทดสอบ branch แล้วกลับไปปรับ prompt หลัง class |

## Workflow does not trigger

| Item | Detail |
|---|---|
| Problem | Submit Form แล้วไม่มี run |
| Likely cause | Flow ยัง off/unsaved, เลือก Form ผิด, trigger connection error, polling delay หรือ submit ก่อนบันทึก flow |
| Quick fix | Save/turn on flow, ตรวจ Form Id, ดู connection, ตรวจ run history และรอก่อน submit ใหม่ |
| Instructor fallback | ใช้ Test/Manual run หรือแสดง run history จาก flow ที่ผู้สอนทดสอบไว้ |

## Permission/environment issue

| Item | Detail |
|---|---|
| Problem | Asset หรือ connection ที่เพื่อนเห็นไม่ปรากฏ, action forbidden, share ไม่ได้ |
| Likely cause | คนละ Power Platform environment, security role ต่าง, connection เป็นของ owner หรือ DLP policy |
| Quick fix | เปรียบเทียบ environment name, account และ connection owner; ใช้ asset ของตนเอง; ให้ admin ตรวจ role/policy |
| Instructor fallback | 1 maker ต่อทีมและ screen-share; คนอื่นทำ testing, business rules และ risk review |

## Run succeeds but output is wrong

| Item | Detail |
|---|---|
| Problem | Flow สำเร็จแต่ Summary/Priority/Excel mapping ผิด |
| Likely cause | Dynamic content map สลับ, prompt placeholder ผิด, stale schema หรือ test data ไม่ครบ |
| Quick fix | เปิด run history ทีละ action; เปรียบเทียบ Inputs/Outputs; แก้ mapping; save; ส่ง test case ใหม่เพียงหนึ่งรายการ |
| Instructor fallback | ใช้ screenshots ของ correct run และให้ผู้เรียนหา mapping error เป็นกิจกรรม debugging |

## Duplicate Excel rows or Teams messages

| Item | Detail |
|---|---|
| Problem | Request เดียวสร้างหลาย rows/messages |
| Likely cause | Submit ซ้ำ, flow หลายสำเนาเปิดอยู่ หรือ retry หลัง timeout |
| Quick fix | ตรวจ Form response ID และ run history; turn off flow สำเนา; ใส่ Request ID/Response ID ใน audit row |
| Instructor fallback | ลบ test duplicates หลัง classตามนโยบาย; ระหว่าง classให้ทำเครื่องหมาย duplicate แทนการเสียเวลาแก้ data |

## Safe escalation note

เมื่อขอความช่วยเหลือ ให้ส่งเฉพาะ:

- ชื่อ step
- ข้อความ error ที่ตัดข้อมูลลับออกแล้ว
- เวลา run โดยประมาณ
- environment name ที่ไม่ใช่ secret
- screenshot ที่ปิดบังข้อมูลบุคคล

ห้ามส่ง password, token, connection details, tenant identifiers, customer data หรือ employee data

---

[← Home](../README.md) · [Instructor Checklist](../templates/instructor-checklist.md) · [Images Checklist](../images/README.md)
