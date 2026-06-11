# Lab Inventory & Refill Alert System — Biotech Lab Automation

> Smart inventory monitoring with automatic LOW/CRITICAL detection and refill alerts.



![Status](https://img.shields.io/badge/Status-Complete-brightgreen)



---

## The Problem

Lab managers manually check inventory levels — a tedious, error-prone process. Running out of critical reagents mid-experiment can halt research for days and cost thousands.

Most labs don't know they're out of stock until it's too late.

---

## The Solution

Lab Inventory & Refill Alert automatically monitors all inventory levels in Airtable, detects LOW and CRITICAL stock, and delivers a formatted email alert — so lab managers always know what needs reordering before it runs out.

- Zero manual checking — runs on schedule automatically
- Instant CRITICAL/LOW detection via smart formula
- Color-coded email with full inventory status
- Reorder list — only critical items highlighted for action

---

## Time & Effort Saved

| Task | Manual | This Automation |
|---|---|---|
| Checking stock levels | Daily manual check | Zero — fully automatic |
| Identifying critical items | Visual scanning | Auto-detected instantly |
| Notifying team | Manual email | Auto-delivered to Gmail |
| Tracking reorder needs | Sticky notes/memory | Clear reorder list in email |

---

## Final Output

- ✅ Inventory Summary — Total / Critical / Low count at top
- ✅ Color-coded table — RED for CRITICAL, ORANGE for LOW
- ✅ Immediate Reorder List — only critical items listed
- ✅ Supplier name per item for quick reordering
- ✅ Professional HTML Gmail alert

---

## What It Does

Automatically monitors lab inventory levels in Airtable, detects LOW and CRITICAL stock, and sends formatted Gmail alerts for refilling.

- **Auto status detection** — GOOD / LOW / CRITICAL calculated automatically
- **Inventory Summary** — Total / Critical / Low count in every email
- **Refill alerts** — Gmail notification when stock is low
- **Reorder list** — critical items highlighted separately for action
- **Multi-item monitoring** — tracks all lab items simultaneously
- **Airtable database** — full inventory management with history
- **Scheduled automation** — runs automatically, no manual trigger needed

---

## Tech Stack

| Layer | Tool |
|---|---|
| Automation | n8n workflow |
| Database | Airtable |
| Email | Gmail HTML |

---

## Architecture

```
Scheduled trigger (n8n)
        ↓
Airtable fetches all inventory items
        ↓
Formula field calculates status per item
        ↓
Filter: LOW or CRITICAL items only
        ↓
Loop Over Items — process each alert
        ↓
JavaScript builds HTML email with summary
        ↓
Gmail sends formatted refill alert
```

---

## Airtable Schema

| Field | Type |
|---|---|
| Item Name | Single line text |
| Current Stock | Number |
| Minimum Threshold | Number |
| Unit | Single select (L, mL, g, mg, pcs, box) |
| Supplier | Single line text |
| Status | Formula (auto) |
| Last Alerted | Date |

---

## Status Formula

```
IF({Current Stock}=0, "CRITICAL",
  IF({Current Stock}<={Minimum Threshold}*0.5, "CRITICAL",
    IF({Current Stock}<{Minimum Threshold}, "LOW", "GOOD")))
```

---

## Technical Notes

- Status field: Formula type in Airtable (not Single Select)
- Loop Over Items node added for correct multi-item processing
- Airtable filter: `OR({Status}='LOW', {Status}='CRITICAL')`
- JavaScript node builds HTML with summary + reorder list

---

*Built by Deman Meshram | BSc Biotechnology + AI Automation*
