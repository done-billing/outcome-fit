# 🎯 outcome-fit

> A [Claude Code](https://claude.ai/code) skill that takes your raw event data and tells you whether you're ready to charge on outcomes, and what you'd earn if you did.

![outcome-fit demo](screenshare.gif)

---

## Why this exists

According to the [2025 State of B2B Monetization](https://www.growthunhinged.com/p/2025-state-of-b2b-monetization) report by Kyle Poyar, more teams than ever want to tie revenue to results, but most don't know if their data actually supports it.

`outcome-fit` answers that question in under 5 minutes.

---

## What it does

Outcome-based pricing charges customers only when your product delivers a confirmed result: a ticket resolved, a payment collected, a document signed.

`outcome-fit` runs your event data through the **CAMP framework**, scoring four dimensions that determine whether you're ready to price on outcomes. You get a score, a phase, and concrete next steps.

### 🏕️ The CAMP framework

| Dimension | Question |
|-----------|----------|
| 🔁 **Consistency** | Do all customers value the same outcome, or does it vary per contract? |
| 🎯 **Attribution** | Can your product take credit for the result, or does the customer claim they drove it? |
| 📏 **Measurability** | Can you measure outcomes in real-time from your own data? |
| 📈 **Predictability** | Can you forecast outcome rates accurately enough to price confidently? |

Each dimension is scored 1–5. Your total determines your phase:

| Score | Phase | What it means |
|-------|-------|---------------|
| 4-8 | 🔬 **Measure** | Instrument your product and run outcomes in shadow mode |
| 9-15 | 🔗 **Attribute** | Analyse confirmed rates, run a pilot with your top customers |
| 16-20 | 💰 **Price** | You're ready. Set the price and start signing contracts |

---

## How it works

The skill runs a guided conversation in Claude Code:

1. 📂 **Share your data.** Paste a CSV/JSON export or connect a database. The skill auto-detects columns.
2. 🎯 **Define the outcome.** Answer two questions: what starts an outcome, and what makes it successful.
3. 💵 **Set a price.** One number. The skill submits everything and shows your CAMP score.

**Total time: under 5 minutes.**

---

## What your data needs to look like

The skill needs an event log where individual actions are grouped into sessions or units of work. Three things must be present:

1. **A start event** that opens an outcome window (e.g. a ticket being created)
2. **A grouping key** that links all events in one session (e.g. a ticket or chat ID)
3. **A success signal** that the skill can evaluate against a condition (e.g. a CSAT score, a status change, a closing event)

Here is a real example from a customer support product:

```
customer_id,    chat_id,   event_type,        event_value, created_at
aperture,       449c...,   ticket_opened,                  2026-03-01T10:01
aperture,       449c...,   response_sent,                  2026-03-01T10:05
aperture,       449c...,   user_closed_chat,               2026-03-01T10:14
aperture,       449c...,   csat,              5,           2026-03-01T10:22
```

In this case:
- `ticket_opened` is the **start event** that begins the outcome window
- `chat_id` is the **grouping key** that ties all events to the same conversation
- `csat >= 4` is the **success condition** the skill evaluates to decide whether the outcome was achieved

The skill auto-detects your columns and asks you to map them. You do not need to pre-process anything.

---

## Installation

In Claude Code, run:

```
/plugin marketplace add https://github.com/done-billing/outcome-fit
/plugin install outcome-fit@outcome-fit
/reload-plugins
```

Then start the analysis:

```
/outcome-fit:outcome-fit
```

---

## Requirements

- [Claude Code](https://claude.ai/code) v2.0 or later
- A sample of your product's event log (CSV, JSON, or a connected database)
