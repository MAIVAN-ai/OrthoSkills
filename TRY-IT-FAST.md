# Try OrthoSkills the fast way (Hermes Agent)

This is **one fast path** to try OrthoSkills in about 15 minutes — not the only one, and
**not** the way to run it with real patients. It uses [Hermes Agent](https://hermes-agent.nousresearch.com)
by Nous Research, which speaks the same `SKILL.md` format these skills are written in, and
which can talk to you through a **Desktop app**, **WhatsApp**, and **Telegram**.

> [!WARNING]
> **Read this before you type anything about a real patient.**
>
> On this fast path, **everything a user types is sent out over the internet to an
> AI company in the United States** (Nous Portal, which routes to a model such as
> `anthropic/claude-opus-4.6`), and it travels there **through a consumer chat app**:
>
> - **Telegram** "cloud" chats are **not** end-to-end encrypted.
> - **WhatsApp** is end-to-end encrypted only as far as the gateway on your computer —
>   from there, the message content is forwarded on to whichever AI model you configured.
>
> **This is fine for learning and demos with made-up or fully anonymised cases.**
> **It is _not_ safe for real patient information (PHI).** To use real patient data you
> need a *governed deployment* — see the bottom of this page and
> [`DATA-SAFETY-FOR-CLINICIANS.md`](./DATA-SAFETY-FOR-CLINICIANS.md).

---

## Who does what

There are **two different roles**, and only one of them needs to touch a command line:

| Role | What they do |
| --- | --- |
| **Operator** (you, or an engineer) | Installs Hermes once, loads OrthoSkills, connects WhatsApp/Telegram. |
| **Surgeon / user** | Just messages the bot, or types in the Desktop app. Installs nothing. |

If you are a surgeon who only wants to *use* it, skip to **"For the surgeon"** at the end.

---

## Operator: 4 steps

### 1. Install Hermes

Easiest: download the **Hermes Desktop installer** for macOS or Windows from
<https://hermes-agent.nousresearch.com> and run it. (It installs both the app and the
command-line tool.)

Command-line only, if you prefer:

```bash
# macOS / Linux / WSL2
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
```

```powershell
# Windows (PowerShell)
iex (irm https://hermes-agent.nousresearch.com/install.ps1)
```

### 2. Turn it on (the fast path)

```bash
hermes setup --portal
```

This logs you in to **Nous Portal**, picks a model, and switches on the built-in tools —
all in one command. (Nous Portal is the hosted subscription referenced in the warning above.)

> Hermes needs a model with at least **64,000 tokens** of context. The hosted models meet
> this automatically — you don't have to think about it on this path.

### 3. Load the OrthoSkills

```bash
# get the skills
git clone https://github.com/MAIVAN-ai/OrthoSkills.git

# copy the skill folders into Hermes' skills directory
cp -R OrthoSkills/OrthoSkills-v0.1.1_cl/Ortho-Skills/* ~/.hermes/skills/
```

> If the path above has changed, just find the folders that each contain a `SKILL.md`
> and copy those into `~/.hermes/skills/`. Hermes auto-discovers them — no registration
> step. Each one also becomes a `/slash-command`.

Start a chat to confirm:

```bash
hermes            # classic
hermes --tui      # nicer interface (recommended)
```

Try: *"I have a displaced femoral neck fracture in a 78-year-old. Walk me through it."*
Hermes should pick up the OrthoSkills on its own.

### 4. Connect WhatsApp and Telegram (optional)

Only after a plain chat works:

```bash
hermes gateway setup     # interactive: choose Telegram, WhatsApp, etc.
hermes gateway status    # check it's running
```

Now the surgeon can message the bot from their phone, and the same OrthoSkills run there.

---

## For the surgeon

You don't install anything. Once your operator has set it up, you either:

- **Open the Hermes Desktop app** and type your question, or
- **Message the bot** on WhatsApp or Telegram, like texting a colleague.

Ask in plain language — *"68-year-old, fell on outstretched hand, swollen wrist, here's
the X-ray, what AO/OTA class is this?"* — and it will reason through the OrthoSkills
workflow (intake → imaging check → classification → treatment options → aftercare).

> [!IMPORTANT]
> OrthoSkills is an **educational reference only**. It does **not** give medical advice.
> Every clinical decision stays with the qualified surgeon in front of the patient.
> And on this fast path: **use invented or fully anonymised cases only — never real,
> identifiable patient data.** Please read
> [`DATA-SAFETY-FOR-CLINICIANS.md`](./DATA-SAFETY-FOR-CLINICIANS.md) first.

---

## When you're ready for real patients (governed deployment)

The fast path above is deliberately simple, which is exactly *why* it isn't safe for real
data. Hermes **can** be locked down — it just stops being a "quickstart" and becomes a
proper deployment that an engineer sets up:

- **Blank Slate setup** — start with everything off, switch on only what you need.
- **Local / on-premise model** — run inference on your own hardware via **Ollama**,
  **LM Studio**, or **vLLM** (`hermes model` → custom endpoint), so patient text never
  leaves the building.
- **`hermes tools` allowlists** — restrict what the agent is allowed to do, per platform.
- **Gateway allowlists** — only approved people can message the bot.
- **Docker sandboxing** — `hermes config set terminal.backend docker`.
- **Audit / traceability logging** — record model, prompt, sources, and the human who
  signed off on every output.

In short: **fast path = demo, no real patient data. Governed deployment = real patients.**
Don't mix them up.

---

*OrthoSkills is the open reasoning layer of the [MAIVAN.ai](https://maivan.ai) / ORTHO-X
ecosystem. Educational use only.*
