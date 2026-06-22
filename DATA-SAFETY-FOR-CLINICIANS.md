# Before you type a real patient in: a 2-minute read for clinicians

You don't need to understand the technology. You need to understand **where your words go**
when you type them into one of these AI assistants. This page explains that in plain language.

---

## The one thing to remember

> [!WARNING]
> On the simple "try it" setup, **what you type leaves your computer, travels across the
> internet to an AI company abroad, and passes through an ordinary messaging app on the way.**
>
> So:
> - ✅ **Made-up cases, teaching examples, fully anonymised cases** → fine.
> - ⛔ **Real, identifiable patient information** → not on this setup. Not yet.

That's it. If you remember nothing else, remember that line.

---

## What the jargon means

You'll see two terms thrown around. Here's what they actually mean for you:

**"PHI" — patient health information.**
Anything that could point back to a real person: name, date of birth, the date and place
of an injury, a record number, a face or tattoo in a photo, or even a rare combination of
details ("the only 7-year-old with this fracture in our village last Tuesday"). If a
stranger could figure out *who* it is, treat it as PHI.

**"End-to-end encrypted" (E2E).**
It means a message is sealed so that *only* the sender and the intended reader can open it —
nobody in between. It's the difference between a **sealed letter** and a **postcard**.

---

## So how does my message actually travel?

Think of it as a postcard relay:

1. You type a case into **WhatsApp** or **Telegram**, or the desktop app.
2. It arrives at the **assistant running on the operator's computer**.
3. That computer then **forwards your words to an AI model run by a company abroad**
   (on the quick setup, a US-hosted service) to get the answer.
4. The answer comes back to you the same way.

Two leaks matter here:

- **Telegram** ordinary chats are like **postcards** — not sealed end-to-end. ⛔
- **WhatsApp** is sealed only as far as step 2. After that, at step 3, your words are
  **handed on to the AI company** — sealed letter to the door, postcard the rest of the way. ⛔

Either way, on the quick setup, **a real patient's details would end up on someone else's
computer in another country.** For Swiss and EU data-protection rules, that's a problem
unless it has been set up specifically to handle it.

---

## "But it's just for education — does it matter?"

For **learning and demos, no** — as long as the case is invented or properly anonymised,
nothing private is at risk, and you should explore freely.

The moment a **real patient** is involved, yes, it matters — the same way you wouldn't
discuss a named patient in a crowded café. The quick setup is the café. It's great for
practice; it's the wrong room for real charts.

---

## When *can* I use real patients?

When your team has done the proper version of the setup — a **governed deployment** — where:

- the AI runs **on your own hospital/clinic computers**, so patient text **never leaves
  the building**;
- only **approved people** can reach the assistant;
- and **every answer is logged** with who reviewed and signed off on it.

That's a job for your operator or engineer, not for you. Until they tell you *"this one is
cleared for real patients,"* assume it isn't — and stick to teaching cases.

---

> [!IMPORTANT]
> **OrthoSkills is an educational reference only. It is not medical advice.** It can help
> you reason and learn; it cannot examine your patient. Every decision remains yours.

*Questions? <coordinator@maivan.ai>*
