# SaajhaKhata

**A shared AI ledger that keeps gold job-work fair for jewellers and karigars.**

*Saajha Khata* means "shared ledger". Nothing is final until both the jeweller and the karigar agree.

Built for the Tech for Bharat hackathon (Jeweltech, problem statement 2.2: *Gold given to karigars for job-work is tracked on trust, and disputes follow*).

---

## The problem

A jeweller gives a karigar 20 g of gold to make a necklace. The wastage is agreed out loud, the entry goes into a notebook or onto a slip, and the deadline is chased by phone. At month end the two sides have different numbers and no record both accept.

The result:

- Gold losses nobody can explain
- Disputes that damage long working relationships
- Missed wedding and occasion dates
- Karigars waiting weeks to be paid, with the least power in the relationship

## Our approach

SaajhaKhata is an AI agent that records every issue and return of gold, checks the weights, tracks deadlines and payments, and asks both parties to approve every entry and settlement. It is designed karigar-first: fairness to the artisan comes before convenience for the shop.

## Core features

| Feature | What it does |
|---|---|
| **Voice and text entry** | The jeweller says or types, for example, "20 grams to Ramesh, necklace, 8% wastage, due 15th, wedding order". The agent turns it into a structured entry. Hindi plus one regional language is the target. |
| **Two-sided confirmation** | Every entry goes to the other party to accept. Nothing counts until both confirm. |
| **Weight reconciliation** | When the piece returns, the app checks issued weight against finished weight, returned scrap and agreed wastage, and flags any gap with the working shown. |
| **Deadline tracking** | Open orders are ranked by occasion date, and both sides are reminded as the date nears. |
| **Payment tracking** | Settlements are drafted, and overdue karigar payments are flagged. |
| **Audit trail** | An append-only log of every entry and approval, with timestamps. |
| **Karigar account view** | Each karigar sees only his own account. |
| **Work passport (planned)** | A verified record of delivered work that a karigar can show to lenders and cooperatives. |

## Design rules

1. **The agent proposes, people decide.** It never edits, settles or closes anything on its own.
2. **The AI does not do the maths.** The language model only reads and drafts. All weight calculations use fixed, deterministic code, with weights stored in milligrams as whole numbers.
3. **Both sides see the same record.** Settlements need approval from both parties.
4. **Privacy by account.** A karigar can only see his own account.
5. **Wastage rules are configurable** per karigar and per item, because every shop works differently.

## Example: how reconciliation works

```
Issued:           20,000 mg   (20 g)
Agreed wastage:    8%         -> 1,600 mg allowed loss
Finished piece:   17,900 mg
Scrap returned:      400 mg

Actual loss  = 20,000 - 17,900 - 400 = 1,700 mg
Allowed loss = 1,600 mg
Result: 100 mg over the agreed wastage -> flagged for both parties to review
```

The flag is raised when the piece is returned, not at month end.

## How it works

```
Voice / text input
        |
        v
  AI parsing  -->  structured entry (karigar, item, weight, wastage, due date)
        |
        v
  Confirmation request to the other party
        |
        v
  Ledger (append-only log)  <-->  Reconciliation engine (deterministic)
        |
        v
  Reminders (deadlines, payments)  -->  Settlement drafted for both to approve
```

## Tech stack

*Update this section to match what you actually build.*

- **Frontend:** web app (mobile-first) or chat-style interface
- **Backend:** Python (FastAPI)
- **Database:** SQLite for the prototype
- **AI:** a large language model for parsing voice and text into entries and drafting reminders
- **Voice:** speech-to-text for Hindi and one regional language

## Project status

*Keep this honest. Tick only what is done.*

- [x] Problem research and design
- [ ] Ledger and two-sided confirmation
- [ ] Weight reconciliation engine
- [ ] Voice and text entry
- [ ] Deadline and payment reminders
- [ ] Karigar account view
- [ ] Field testing with real jewellers and karigars

## Field notes

*Add one or two real conversations with a jeweller or karigar here, with what they said about how gold is issued, how wastage is agreed, and how long payment takes. Link them from `docs/field-notes.md` if you keep a separate file.*

## Business potential

- A simple monthly subscription per jewellery shop
- Free for karigars, so adoption does not depend on them paying
- Later, the verified work record can help karigars show their history to lenders and cooperatives

## References

- World Gold Council, [Jewellery market structure: India gold market series](https://www.gold.org/goldhub/research/jewellery-market-structure-india-gold-market-series)
- World Gold Council, [India's gold jewellery market structure](https://www.gold.org/goldhub/research/indias-gold-jewellery-market-structure)
- Bureau of Indian Standards, [Hallmarking of Gold Jewellery & Artefacts](https://services.bis.gov.in/php/BIS_2.0/BISBlog/?p=560)

## Team

SHREYA B
VISMAYA JAIN P


