# Manus Lab Input — Simulated Business Requests

ใช้สำหรับ [Lab 4: Manus AI](../06-manus-ai/README.md) เท่านั้น

> Dataset นี้เป็นข้อมูลจำลอง ไม่มี Expected Priority หรือคำตอบเฉลย ผู้เรียนต้องตรวจผลด้วย Business Rules

| Request ID | Requester | Department | Business Request | Context / Deadline |
|---|---|---|---|---|
| BR-001 | Demo Requester A | Sales | ลูกค้ารายใหญ่ไม่สามารถชำระเงินผ่านระบบได้และอาจยกเลิกคำสั่งซื้อ | ต้องแก้ภายในวันนี้; order มีมูลค่าสำคัญ |
| BR-002 | Demo Requester B | Sales | ขอรายงานยอดขายแยกตามสาขาสำหรับ review ประจำสัปดาห์ | ใช้ในอีก 4 วัน; งานขายยังเดินต่อ |
| BR-003 | Demo Requester C | Marketing | มีโพสต์กล่าวหาบริษัทเรื่องความปลอดภัยและกำลังถูกแชร์อย่างรวดเร็ว | Public reputation risk กำลังขยาย |
| BR-004 | Demo Requester D | Marketing | ด่วนมาก ขอข้อมูล conversion ของแคมเปญล่าสุด | ไม่บอกว่าจะใช้เมื่อใดหรือ decision ใดขึ้นกับข้อมูล |
| BR-005 | Demo Requester E | Finance | ระบบรับชำระเงินล้มเหลวหลายช่องทาง ลูกค้าไม่สามารถจ่ายได้ | เกิดอยู่ขณะนี้; กระทบหลาย orders |
| BR-006 | Demo Requester F | Finance | ต้องการ reconciliation report เพื่อปิดงบในอีกสามวัน | มี deadline; งานส่วนอื่นยังทำต่อได้ |
| BR-007 | Demo Requester G | HR | ระบบ payroll คำนวณเงินเดือนผิดสำหรับพนักงานจำนวนมากก่อนวันจ่าย | อาจกระทบค่าจ้างและ compliance |
| BR-008 | Demo Requester H | HR | พนักงานใหม่ขอวิธีเปลี่ยนรูป Profile ในระบบประชุมออนไลน์ | ไม่มี deadline |
| BR-009 | Demo Requester I | Operations | ระบบรับคำสั่งซื้อของหนึ่งสาขาหยุดทำงาน พนักงานรับ Order ไม่ได้ | เริ่มตั้งแต่ 10:00; ไม่ทราบเวลาแก้เสร็จ |
| BR-010 | Demo Requester J | Operations | ลูกค้าหลายรายร้องเรียนการส่งสินค้าล่าช้าซ้ำในสัปดาห์นี้ | ยังส่งได้แต่ SLA เริ่มเสีย |
| BR-011 | Demo Requester K | IT | ผู้ใช้ทุกสาขาเข้า ERP ไม่ได้และไม่สามารถออกใบสั่งซื้อ | เกิดอยู่ขณะนี้; core operations หยุด |
| BR-012 | Demo Requester L | IT | เข้าโฟลเดอร์ไม่ได้ ช่วยแก้ ASAP | ไม่ระบุโฟลเดอร์ งานที่หยุด หรือจำนวนผู้ใช้ |
| BR-013 | Demo Requester M | Customer Service | ลูกค้าหลายรายถูกตัดเงินแต่ระบบไม่สร้างคำสั่งซื้อ | เกิดอยู่ขณะนี้; มี financial/reputation risk |
| BR-014 | Demo Requester N | Customer Service | ลูกค้าขอทราบเวลาทำการของสาขา | ไม่มีเหตุเร่งด่วน |

## Business Rules Reference

**HIGH**

- Immediate customer impact
- Significant revenue or financial impact
- Critical operational disruption
- Serious compliance or reputation risk
- Time-sensitive issue where delay causes significant business impact

**MEDIUM**

- Important but not immediately critical
- Requires management attention
- Deadline within several days
- Operations can continue

**LOW**

- Routine administrative work
- General information request
- No immediate business impact
- No urgent deadline

> `urgent`, `ASAP`, `immediately` หรือ `as soon as possible` ไม่ใช่เหตุผลเพียงพอสำหรับ HIGH ต้องพิจารณา business impact และระบุ missing information เมื่อข้อมูลไม่พอ
