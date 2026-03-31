# journey-persona-tool
A journey-anchored customer persona prompt generator for product and experience teams
# Journey Persona Tool

A lightweight, single-file tool for generating structured customer persona prompts anchored to specific journeys, stages, and relationship tiers. Designed for product and experience teams who write user stories.

---

## What It Does

Most persona frameworks produce demographic profiles. This tool produces **situated personas** — a specific person, at a specific moment, in a specific journey, with a friction map and story-ready output.

You select:
- An **archetype** (relationship tier × demographic band)
- A **value stream and journey**
- A **stage** within that journey
- A **channel**

The tool generates a structured prompt you paste into Claude to produce a full persona output, including a narrative paragraph and three user story starters ready for a backlog.

---

## The Framework

### Relationship Depth Model

Archetypes are organized across three tiers — based on the breadth and complexity of a customer's relationship with your organization, not just demographics. Each preset defines its own tier names and logic. The banking preset uses Solution / Relationship / Dedicated. Healthcare uses Episodic / Ongoing / Complex Care. The tier structure is fully editable.

### Journey Hierarchy

Journeys are organized in three levels:

```
Value Stream → Journey → Stage
```

A **value stream** is a high-level category of customer experience (e.g. Loan Value Stream, Care Access Value Stream). A **journey** is a named end-to-end customer experience within that stream (e.g. New Mortgage, Appointment Scheduling). A **stage** is the discrete moment within the journey where a story gets written (e.g. Application, Underwriting Wait).

Stories written at the stage level are specific enough to be useful and general enough to anchor a sprint.

### Four-Layer Output

Every generated persona contains:

1. **Identity Layer** — archetype, age/career stage, household or role, relationship depth
2. **Journey Context** — journey, stage, channel, trigger
3. **Behavioral & Motivational Layer** — goal, decision style, trust signals, what "easy" means at this tier, success definition
4. **Friction Map** — stall point, bad outcome, good outcome, downstream business risk

Followed by a plain-language narrative paragraph and three `As a... I want... so that...` story starters.

---

## Vertical Presets

Four presets ship with this tool:

| Preset | Tier Model | Value Streams |
|---|---|---|
| Community Banking | Solution / Relationship / Dedicated | Loan, Deposit & Savings, Account Servicing, Money Movement |
| Regional Healthcare | Episodic / Ongoing / Complex Care | Care Access, Care Delivery, Care Management, Billing & Admin |
| B2B SaaS | Starter / Growth / Enterprise | Acquisition, Onboarding, Adoption, Renewal & Expansion, Support |
| Specialty Retail | Casual / Enthusiast / Pro | Discovery & Research, Purchase, Post-purchase, Loyalty & Community |

All preset fields are editable — select a preset as a starting point and modify org name, market description, tier definitions, and systems to match your organization.

---

## How to Use

1. Download `persona-prompt-generator-v2.html`
2. Open it in any modern browser (Chrome or Edge recommended)
3. Select a vertical preset or configure manually
4. Work through steps 1–4 in the generator
5. Click **Generate Prompt**
6. Copy the output and paste it into a new [Claude](https://claude.ai) chat
7. Use the persona output to write user stories

No installation. No server. No API key required. The tool runs entirely in the browser.

---

## Adding a Custom Vertical

Open the HTML file and locate the `PRESETS` object in the `<script>` section. Add a new entry following this structure:

```javascript
your_vertical: {
  id: 'your_vertical',
  label: 'Display Name',
  icon: '🏷️',
  sub: 'Short descriptor',
  orgName: 'Example Org Name',
  systems: 'List of primary systems',
  marketDesc: 'Describe your market, customer base, and key experience drivers.',
  tiers: [
    { name: 'Tier 1 Name', tagline: 'Short tagline', def: 'Full tier definition including what easy means at this tier.' },
    { name: 'Tier 2 Name', tagline: 'Short tagline', def: 'Full tier definition.' },
    { name: 'Tier 3 Name', tagline: 'Short tagline', def: 'Full tier definition.' }
  ],
  archetypes: [
    { code: 'A1', friendlyName: 'The Example', tierIdx: 0, age: '25–40', desc: 'One-line description' },
    // add more...
  ],
  valueStreams: {
    'Value Stream Name': [
      { name: 'Journey Name', stages: ['Stage 1', 'Stage 2', 'Stage 3'] },
      // add more journeys...
    ],
    // add more value streams...
  }
}
```

Three tiers is the convention but not a hard constraint. The tier index (`tierIdx`) on each archetype maps to the position in the `tiers` array.

---

## Design Decisions

**Why journey-anchored?** A demographic archetype without a journey context is an arbitrary starting point. The same 45-year-old behaves differently applying for a mortgage than disputing a charge. The journey is what makes the persona usable.

**Why a prompt generator rather than a direct AI integration?** This is a POC. The prompt output is intentionally transparent — you can read it, edit it, and understand exactly what context Claude receives. A direct API integration is a natural next step.

**Why three tiers?** The three-tier relationship depth model (broad / growing / complex) maps cleanly across industries. It is grounded in the idea that the cost-to-serve and the expected service model differ meaningfully across tiers — and that personas built without tier awareness will produce stories that optimize for the wrong customer.

---

## Requirements

- A modern browser (Chrome or Edge recommended)
- A [Claude](https://claude.ai) account to receive and use the generated prompts

---

## License

MIT — see `LICENSE` for details.

---

## Author

**Brian Goeller**  
CTO / CIO

---

*This tool is a working proof of concept. Contributions, vertical presets, and forks are welcome.*
