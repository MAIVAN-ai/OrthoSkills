# OrthoSkills

**Open-source orthopaedic clinical reasoning skills for AI agents.**

OrthoSkills is a public, community-driven library of [Anthropic-style "skills"](https://www.anthropic.com/news/skills) covering the orthopaedic surgical workflow — from diagnosis and fracture classification (AO/OTA 2018) through treatment mapping, implant selection, outcome measurement, and aftercare.

Each skill is a self-contained Markdown file with YAML frontmatter that tells an AI assistant (Claude, ChatGPT, Gemini, or any MCP-compatible agent) *when* to use the skill and *how* to reason through that step of the orthopaedic workflow.

> 🩺 **Educational reference only.** These skills do not provide medical advice. Every clinical decision must be made by a qualified surgeon with the patient in front of them. Skills emphasise human-in-the-loop confirmation at every step.

---

## Why this exists

Eric Topol has rightly pointed out that medical AI lives or dies by the quality of its **ground truth, prospective validation, and outcome linkage**. Most orthopaedic AI today is trained on retrospective datasets with no surgeon confirmation and no outcome follow-up.

OrthoSkills is the **public reasoning layer** of a larger ecosystem being built by [MAIVAN.ai](https://maivan.ai) / ORTHO-X:

```
┌────────────────────────────────────────────────────────┐
│  OrthoSkills  (this repo, public, open-source)        │
│  → How an AI should reason about orthopaedic cases     │
└────────────────────────────────────────────────────────┘
                          │
                          ▼  consumed by
┌────────────────────────────────────────────────────────┐
│  OrthoClaw  (WhatsApp clinical reasoning agent)        │
│  → Surgeon-facing front-end                            │
└────────────────────────────────────────────────────────┘
                          │
                          ▼  validated by
┌────────────────────────────────────────────────────────┐
│  OrthoClass MCP  (registration-only, IP-protected)     │
│  → Prospective ground-truth + outcome linkage engine   │
└────────────────────────────────────────────────────────┘
```

The skills in this repo are **deliberately generic and open**. They encode how to *reason* through orthopaedic cases — not the proprietary case data, validated models, or PMCF infrastructure of OrthoClass.

---

## Skills index

The skills follow the orthopaedic surgical workflow:

| # | Skill | Purpose |
|---|---|---|
| 01 | [Case Intake](skills/01-case-intake/SKILL.md) | Structured history, mechanism, exam, red flags |
| 02 | [Image Quality Check](skills/02-image-quality-check/SKILL.md) | AP/lateral adequacy, projection, artefacts, missing views |
| 03 | [Anatomy Routing](skills/03-anatomy-routing/SKILL.md) | Map anatomy → applicable classification systems |
| 04 | [AO/OTA Classification](skills/04-aoota-classification/SKILL.md) | AO/OTA 2018 structured reasoning (canonical: proximal femur) |
| 05 | [Region-Specific Classifications](skills/05-region-classifications/SKILL.md) | Garden, Pauwels, Schatzker, Neer, Mason, Lauge-Hansen, etc. |
| 06 | [Differential Reasoning](skills/06-differential-reasoning/SKILL.md) | Primary + differentials, confidence calibration, when to escalate |
| 07 | [Treatment Mapping](skills/07-treatment-mapping/SKILL.md) | Classification → treatment options (educational, not advisory) |
| 08 | [Implant Selection](skills/08-implant-selection/SKILL.md) | Generic device class considerations (CMN vs DHS vs plate, etc.) |
| 09 | [Evidence Retrieval](skills/09-evidence-retrieval/SKILL.md) | PubMed / Consensus / AO Surgery Reference query patterns |
| 10 | [Outcome Measurement](skills/10-outcome-measurement/SKILL.md) | PROMs, union status, complications, follow-up schedule |
| 11 | [Aftercare & Rehab](skills/11-aftercare-rehab/SKILL.md) | Weight-bearing progression, physio milestones, red flags |
| 12 | [Case Report Publishing](skills/12-case-report-publishing/SKILL.md) | Structured export (JBJS, OrthoWiki, registry) |

**Canonical deep skill:** `04-aoota-classification` includes a full reference for the **proximal femur** (AO/OTA segment 31). Other anatomical regions are present as stub references for the community to expand.

---

## How to use

### As a Claude skill

Place any `SKILL.md` (or a folder containing one) in your Claude environment's skills directory. Claude will auto-discover it from the YAML frontmatter and invoke it when relevant queries arrive.

### As a generic AI prompt library

Each `SKILL.md` is plain Markdown — copy/paste the body into ChatGPT, Gemini, Claude.ai, or any agent's system prompt. The reasoning patterns work regardless of model.

### As an MCP tool consumer

The skills are designed to call the (forthcoming) **OrthoClass MCP server** for prospective case capture, ground-truth recording, and outcome linkage. See the `orthoclass.*` tool references throughout. When the MCP server is unavailable, skills degrade gracefully to advisory-only mode.

---

## Repo layout

```
OrthoSkills/
├── README.md                              ← you are here
├── LICENSE                                ← Apache-2.0
├── CONTRIBUTING.md                        ← how to add/improve skills
├── CODE_OF_CONDUCT.md
├── .github/workflows/validate-skills.yml  ← CI to lint SKILL.md frontmatter
└── skills/
    ├── 01-case-intake/SKILL.md
    ├── 02-image-quality-check/SKILL.md
    ├── 03-anatomy-routing/SKILL.md
    ├── 04-aoota-classification/
    │   ├── SKILL.md
    │   └── references/
    │       ├── proximal-femur-31.md       ← canonical, deep
    │       ├── humerus-stubs.md
    │       ├── forearm-stubs.md
    │       ├── femur-shaft-distal-stubs.md
    │       ├── tibia-stubs.md
    │       └── spine-pelvis-stubs.md
    ├── 05-region-classifications/
    │   ├── SKILL.md
    │   └── references/
    │       ├── garden-pauwels.md          ← canonical companion to proximal femur
    │       └── other-systems-stubs.md
    ├── 06-differential-reasoning/SKILL.md
    ├── 07-treatment-mapping/SKILL.md
    ├── 08-implant-selection/SKILL.md
    ├── 09-evidence-retrieval/SKILL.md
    ├── 10-outcome-measurement/SKILL.md
    ├── 11-aftercare-rehab/SKILL.md
    └── 12-case-report-publishing/SKILL.md
```

---

## Contributing

Pull requests are welcome from orthopaedic surgeons, registrars, residents, AI engineers, and anyone working at the intersection of orthopaedics and machine learning. See [CONTRIBUTING.md](CONTRIBUTING.md).

**Especially wanted:**
- Expanding stub regions in `04-aoota-classification/references/` into full reference files modelled on `proximal-femur-31.md`
- Region-specific classification systems in `05-region-classifications/references/` (Schatzker, Neer, Mason, Lauge-Hansen, Sanders, Hawkins, …)
- Real-world case examples (anonymised, with consent) for skill validation

---

## License

Apache License 2.0 — see [LICENSE](LICENSE).

The AO/OTA Fracture & Dislocation Classification Compendium 2018 is © AO Foundation. This repository **does not reproduce the Compendium**; it describes the *reasoning workflow* a surgeon or AI agent would follow when applying any classification system to a case. Always consult the official AO Foundation publications for authoritative classification text.

---

## Maintainers

- [MAIVAN.ai](https://maivan.ai) / ORTHO-X — by Bluenaut Matching Services AG, CH - Kilchberg, Zurich, Switzerland
- Contact: mailto:coordinator@maivan.ai

---

> *"As opposed to many randomized trials and prospective studies, most medical AI has no ground truth."*
> — Eric Topol
>
> OrthoSkills + OrthoClass exists to fix that, one fracture at a time.
