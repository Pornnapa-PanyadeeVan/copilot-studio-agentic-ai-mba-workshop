# Sample Business Requests

ข้อมูลจำลองสำหรับ Microsoft Forms, Agent Test/Preview และ end-to-end workflow test ไม่มีข้อมูลบุคคลจริง

> [!TIP]
> ผู้สอนสามารถซ่อนคอลัมน์ Expected Priority/Why ก่อนแจกผู้เรียน แล้วใช้เป็น answer guide ระหว่าง debrief

## HIGH priority

| # | Requester Name | Department | Business Request | Required Date | Expected Priority | Why |
|---:|---|---|---|---|---|---|
| 1 | Customer Service Lead | Customer Service | A key customer paid this morning but the account is still blocked. They cannot place orders and may move to a competitor. Restore access today. | Today | HIGH | Immediate customer, revenue and reputation impact; ≤24h |
| 2 | Revenue Operations Manager | Sales | The quoting system is failing for all sales representatives. Three enterprise proposals must be submitted by 4 PM today. | Today, 4 PM | HIGH | Critical operational issue and revenue deadline within hours |
| 3 | Accounts Payable Manager | Finance | A supplier appears to have been paid twice for a large invoice. The bank file will settle this afternoon unless an authorized manager intervenes. | This afternoon | HIGH | Financial impact and immediate deadline; human authorization required |
| 4 | Service Desk Manager | IT | The customer checkout service is unavailable in all regions. Orders have stopped and monitoring shows continued failures. | Immediately | HIGH | Critical outage and immediate revenue/customer impact |
| 5 | Brand Director | Marketing | A live campaign may contain an unlicensed image. Legal asked us to pause distribution while ownership is verified. | Within 2 hours | HIGH | Serious compliance/reputation risk; AI must route, not make legal decision |

## MEDIUM priority

| # | Requester Name | Department | Business Request | Required Date | Expected Priority | Why |
|---:|---|---|---|---|---|---|
| 6 | Finance Analyst | Finance | Prepare the monthly margin report for next Friday's management meeting. Data is available but needs manager review. | Next Friday | MEDIUM | Deadline within several days and management attention |
| 7 | HR Coordinator | HR | Create the onboarding schedule for six employees who start next Monday. Managers need the draft in four days. | In 4 days | MEDIUM | Important, time-bound, not immediate crisis |
| 8 | Campaign Manager | Marketing | Review the launch plan and recommend which of two media options should receive the remaining budget. Leadership meets in three days. | In 3 days | MEDIUM | Management decision and financial relevance within days |
| 9 | Procurement Specialist | Operations | Compare two supplier renewal options before the current agreement expires in five days. | In 5 days | MEDIUM | Time-bound and needs management attention |
| 10 | Sales Operations Analyst | Sales | Clean and prioritize the lead list before the weekly pipeline review on Friday. No customer is currently waiting. | Friday | MEDIUM | Supports management process within several days |

## LOW priority

| # | Requester Name | Department | Business Request | Required Date | Expected Priority | Why |
|---:|---|---|---|---|---|---|
| 11 | HR Assistant | HR | How do I change my profile picture in Microsoft Teams? | No deadline | LOW | General information; no immediate impact |
| 12 | Sales Coordinator | Sales | Please send the link to the standard travel policy for future reference. | No deadline | LOW | Routine information request |
| 13 | Content Coordinator | Marketing | Where is the current presentation template stored? | When convenient | LOW | Routine administrative request |
| 14 | Support Technician | IT | Please explain how to switch Teams from dark mode to light mode. | No deadline | LOW | General how-to question |
| 15 | Finance Assistant | Finance | What naming format should we use for internal cost-center folders? | This month | LOW | Administrative information with no immediate impact |

## AMBIGUOUS / debate cases

| # | Requester Name | Department | Business Request | Required Date | Expected Priority | Why / discussion point |
|---:|---|---|---|---|---|---|
| 16 | Operations Coordinator | Operations | We need approval for the vendor issue urgently. Please handle it. | Soon | NEEDS CLARIFICATION | No specific impact, amount, decision or deadline |
| 17 | Account Executive | Sales | A customer wants a special discount and is waiting. Please approve it quickly. | Not specified | NEEDS CLARIFICATION | Missing discount value, authority, deal value and deadline; AI must not approve |
| 18 | HR Business Partner | HR | An employee raised a serious concern about a manager. We need a decision as soon as possible. | As soon as possible | NEEDS CLARIFICATION | Potential high impact, but facts are unverified; route to authorized HR review |
| 19 | Sponsorship Manager | Marketing | Management wants a recommendation on a significant conference sponsorship. The offer expires in two days and could influence next quarter's leads. | In 2 days | MEDIUM (debate) | Management and financial attention; debate whether more evidence could justify HIGH |
| 20 | Warehouse Supervisor | Operations | A packing machine is making an unusual sound, but production continues normally. Maintenance can inspect tomorrow; no safety assessment has been completed. | Tomorrow | NEEDS CLARIFICATION (debate) | Possible operational/safety risk requires verified facts and human safety review |

## Copy/paste format for Forms

```text
Requester Name: Customer Service Lead
Department: Customer Service
Business Request: A key customer paid this morning but the account is still blocked. They cannot place orders and may move to a competitor. Restore access today.
Required Date: Today
```

## Suggested testing order

1. เริ่ม LOW เพื่อยืนยัน basic formatting
2. ทดสอบ MEDIUM เพื่อดู management/deadline logic
3. ทดสอบ HIGH และตรวจ Teams notification
4. ทดสอบ ambiguous และตรวจ Default/Human Review
5. ทดสอบ debate case แล้วเปรียบเทียบ evidence ระหว่างทีม

---

[← Home](../README.md) · [Lab 1](../02-build-ai-agent/README.md) · [Lab 2](../03-build-agentic-workflow/README.md)
