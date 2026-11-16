# Westpac Online Banking — Hackathon Prototype

A concept prototype for the "AI and what it means for Banking" hackathon.

A self-contained single-page mock of a Westpac-style online banking site featuring multi-user demo profiles, transaction creation, savings plans, BankSmart AI budgeting, and persistence.

- Styled with GEL-inspired design tokens (Westpac red `#DA1710`).
- Features BankSmart AI settings for income splitting (into pots) and transaction round-up increments ($1, $5, $10, $50, $100).
- Bills bucket lists the recurring bills BankSmart has detected.
- `index.html` is fully self-contained — just open it in any modern browser.

---

## New BankSmart features

**🛡️ Bill cover:** if a personal purchase is bigger than *Safe to spend*, it would eat into money set aside for bills. Wesley automatically moves the difference from savings, choosing carefully: protected goals are never touched, the goal due furthest away goes first (up to half of it), then the Buffer, then other goals. Goals due within 3 months are a last resort. The alert explains which savings were used and why, and each goal card has a 🔒 **Protect from bill cover** button and shows an alert on Overview, the account page and BankSmart. You then pick how to refill: **increase round-ups**, a **bigger lump sum**, or **balance both**. The Add transaction preview warns you before you submit. There's a toggle in AI controls. *Demo: as Priya, add a large purchase to see it spread across goals, or protect a goal first to see it skipped.*

**🔁 Subscription check:** Wesley watches each subscription for 6 months, then compares monthly against annual pricing. You get **Switch to annual** (or switch all), a running "you're saving $X a year" total, and Undo. New subscription-like debits are tracked automatically. Prices are demo values.

**🔮 What if…? future-proofing planner:** not just trips any more. Pick a change: **buy something big** (car, furniture, renovation; cash, loan or deposit + loan), **change my income** (part-time, new job, time off), **have a set amount by a date**, or **take on a new regular cost** (childcare, higher rent, a pet). Wesley asks a short series of questions, including whether to keep saving into your goals, how big a safety net you want and anything else coming up. Then it looks at the whole account: income, home, bills, everyday living, repayments, goals, savings, Buffer and term deposits. The result shows a calm verdict (✅ works for you, 🟡 doable with a few changes, 🌱 not quite yet but there's a path), a month-by-month today vs with-the-change table, savings and safety-net months, a 🧪 **surprise-cost stress test** that ties in Bill cover, what can and can't happen, how each goal is affected, and ideas with **Try this** buttons that re-run the check. Loans get example repayments and total interest, and a careful **See options** link-out. **Make it a plan** turns it into a savings goal. In chat, try *"What if I go part-time next year?"* or *"What if I buy a car?"*. Each demo customer has a monthly money profile (`finProfile`) the planner uses. General information only, not financial advice.

**AI controls & privacy** are now Westpac-style tiles with an On/Off band, at the top of BankSmart **Settings & Rules**.

**🧠 Wesley learns (habits, unusual activity and spending moments):**
- *Habit profile:* each customer has a learned history (transactions, usual supermarket, typical spend per category, usual hours, home area, regular merchants). It grows with every spend and every answer. See **What Wesley's learning about you** on BankSmart, or ask Wesley *"what have you learned about me?"*.
- *Unusual activity checks:* new spends are checked against the profile. Spends that are out of character (e.g. 15× your usual, a new overseas merchant at 3am) get a **"Was this you?"** card that lists the reasons. **Yes** teaches Wesley (that merchant is trusted next time), and Bill cover waits until you confirm. **No** explains what the live app would do (demo only).
- *Spending moments:* when flights or accommodation are detected (Qantas, Jetstar, Virgin, Booking.com, Airbnb and so on), a friendly card asks whether it's a holiday, work or not travel. For a holiday it asks whether it's part of a trip saver (or offers to create one) and whether you're going overseas. Then it shares helpful tips:
  - travel insurance, highlighting complimentary cover on cards that include it (e.g. Altitude Black), with eligibility and activation notes
  - adding your Qantas Frequent Flyer or Velocity number, with a "link it" option
  - telling Wesley your travel dates so overseas spends aren't flagged
  - comparing cards for international fees
  It remembers answers (e.g. "Qantas is usually work") so it stops asking.
- *Ideas based on how you spend:* travel → insurance or rewards cards, bigger purchases → What if…, many subscriptions → Subscription check. All links go to real westpac.com.au pages with "general information, not a recommendation" wording.
- *Demo:* **Try it** buttons on the panel, or the new **✈️ Flights** and **🌐 Overseas online** presets in Add transaction. **Reset what Wesley learned** clears it. Both features have toggles in Settings & Rules.

Also fixed: the "Wesley is paused" banner was always showing, even when Wesley was on.

---

## Pre-populated Demo Profiles

On the login screen, click the **👤 Demo accounts ▾** button in the bottom-left corner to quickly switch between demo users, or type any of their 8-digit Customer IDs directly into the login form:

| Customer ID | Name | Role | Profile & Accounts |
| :--- | :--- | :--- | :--- |
| `21157077` | **Alex Chen** *(Default)* | Young renter | Saving for a rental bond. Accounts: *Westpac Choice*, *Westpac Life* (Rental bond goal), *Low Rate Card*, and *COMPANY PTY LTD* business banking. |
| `18524718` | **Priya Sharma** | Family budgeter | Managing household finances. Accounts: *Westpac Choice*, *Westpac Life* (Family holiday & Kids' education goals), *Altitude Black Card*. Personal only. |
| `90815760` | **Sam Rossi** | Café owner | Director of Rollers Pty Ltd. Accounts: Personal *Choice* & *Life*, *Business Platinum Card*, and *Westpac Business One* with merchant settlement. Defaults to Business view. |
| `13138554` | **Margaret "Peggy" Wilson** | Retiree (age 71) | Living on Age Pension + super income. Accounts: *Westpac Choice*, *Westpac Life* (Grandkids' Christmas, Caravan trip, Rates bucket), and *Westpac Term Deposit* ($40,000 at 4.60% p.a.). |

*Entering any other credentials will default to signing in as Alex Chen.*

---

## Adding Transactions

On any account's transaction screen, click the **💳 + Add transaction** button in the bottom-left corner:
1. Select **Debit (− money out)** or **Credit (+ money in)**.
2. Choose the destination account (automatically pre-selects the account you are viewing).
3. Type a description or pick from convenient presets (e.g. ☕ Coffee, 🛒 Groceries, 💼 Salary).
4. Enter an amount and date.
5. Review the real-time balance preview and click **Add Transaction**.
6. The transaction is instantly recorded, running balances are recalculated, and personal everyday spending updates your **Safe to spend** allowance in BankSmart.

---

## Data Persistence & Reset

All demo data is automatically persisted in browser storage:
- **`localStorage` (`wbc_demo_v1`)**: Stores all accounts, custom transactions, saving goals/buckets, and Wesley AI preferences per user.
- **`sessionStorage` (`wbc_demo_user`)**: Maintains your active session across page reloads.
- **Resetting Data**: Click **👤 Demo accounts ▾** on the login screen and choose **↺ Reset all demo data** at any time to restore initial seed balances and transactions.

---

**Not affiliated with or endorsed by Westpac. Demonstration only.**
