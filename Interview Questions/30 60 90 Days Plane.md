# What do you do in the first 30/60/90 days?

> **Interview context:** This question tests strategic thinking, stakeholder management, and whether you can lead a transformation without burning trust. The interviewer wants to see a *structured*, *evidence-based* approach — not a hero story.

---

## The Full Answer (Speak This)

> "My first instinct is never to fix anything in the first 30 days. My job is to *understand* the problem before I prescribe the solution. A lot of architects come in and immediately start rewriting frameworks or pushing tools — and they lose the team before they've even built trust. Here's how I actually approach it."

---

## 🗓️ First 30 Days — Listen, Observe, Assess

**Goal:** Understand the real state — not the state people *think* they're in.

### What I do:
- **Shadow the QA team** through 2–3 full test cycles. Observe without suggesting.
- **Interview stakeholders** — dev leads, QA engineers, product owners, release managers. Ask: *"Where does quality fail you most?"* not *"What tools do you use?"*
- **Run a maturity assessment** across 5 dimensions (see below).
- **Map the current flow** — from code commit to production deploy. Where does manual testing live? Where are the bottlenecks?
- **Audit existing automation** (if any) — test coverage %, flaky rate, last-run date, who owns it.
- **Identify the 3 biggest pain points** that the *team* feels, not the ones I assume they have.

### Maturity assessment model (Grade 1–5 each):

| Dimension | Grade 1 (Basic) | Grade 5 (Advanced) |
|---|---|---|
| **Tooling** | Manual spreadsheets | AI-enabled, self-healing frameworks |
| **Test coverage** | Ad-hoc, undocumented | Full UI/API/performance/security coverage |
| **CI/CD integration** | No automation in pipeline | Continuous testing, shift-left |
| **Skills** | Manual testers only | Full-stack automation + AI literacy |
| **Process maturity** | Reactive, firefighting | Proactive, metrics-driven |

> 💡 **Interview tip:** *"Most teams rate themselves a 3. The assessment usually reveals they're a 2. I say this without judgment — I say it so we can set a realistic roadmap."*

### What I don't do:
- ❌ Push a tool or framework yet.
- ❌ Criticise the existing setup in front of the team.
- ❌ Make promises about timelines.

### Deliverable: Assessment report
- Current maturity scores per dimension
- Top 3 pain points with evidence
- Preliminary risk areas

---

## 🗓️ Days 30–60 — Plan, Prioritise, Align

**Goal:** Turn observations into a credible roadmap. Get stakeholder buy-in before building anything.

### What I do:
- **Define the target state** — where does the client want to be in 6/12 months? (Faster releases? Fewer regression bugs? Compliance coverage?)
- **Build a prioritised roadmap** with 3 horizons:
  - *Horizon 1 (0–3 months):* Quick wins — visible impact, low risk
  - *Horizon 2 (3–6 months):* Foundation work — framework, CI/CD integration
  - *Horizon 3 (6–12 months):* AI-enabled testing, agentic workflows
- **Select tooling** based on the team's existing stack, skills, and budget — not my personal preferences.
- **Present the roadmap** to engineering leads and business stakeholders. Frame everything in business language: *"This reduces regression cycle time by an estimated X%"*, not *"We're going to use Playwright."*
- **Identify the quick win** — the specific thing we'll pilot in days 60–90.

### Tool selection criteria (share this in interviews):

| Criteria | Why it matters |
|---|---|
| Team skill fit | A tool the team can't use is a liability, not an asset |
| Stack compatibility | Avoid introducing language mismatches |
| CI/CD integration | Must plug into Jenkins/GitHub Actions/Azure DevOps |
| AI capability | Self-healing, test generation, anomaly detection |
| License & cost | Realistic for client's budget |

### Deliverable: Transformation roadmap
- Maturity baseline → target state
- Phased plan with success metrics per phase
- Tool recommendations with rationale
- Stakeholder-approved quick win scope

---

## 🗓️ Days 60–90 — Pilot, Prove, Scale

**Goal:** Execute the quick win. Show measurable results. Build momentum for the bigger transformation.

### What I do:
- **Execute the quick win** — scope matters here. It must be:
  - Small enough to complete in 30 days
  - Impactful enough for stakeholders to *notice*
  - Repeatable as a pattern for the rest of the suite
- **Typical quick win options** (pick based on assessment):

| Quick win | When to pick it | Expected impact |
|---|---|---|
| Automate top 10 regression tests | High manual regression burden | 30–40% cycle time reduction on that suite |
| Plug smoke tests into CI/CD | No pipeline automation at all | Immediate PR-level quality gate |
| API test layer for core endpoints | UI tests are slow and brittle | Faster, more stable coverage |
| Self-healing locators on existing suite | High flaky test rate | Reduce false failures, restore team confidence |

- **Measure and report results** — before/after metrics, not anecdotes.
- **Run a retrospective** with the team — what worked, what didn't, what to do differently in the next phase.
- **Socialise the win** — demo to stakeholders, document the pattern for the team to replicate.

### What success looks like at 90 days:
- ✅ Team understands the roadmap and believes it's achievable
- ✅ At least one concrete, measurable improvement is live
- ✅ Stakeholders have seen evidence, not just promises
- ✅ The team trusts the process — they're asking "what's next?" not "why is this happening to us?"

---

## 🏢 Real Example — Equitable Life

| Phase | What happened |
|---|---|
| **30 days** | Maturity assessment across QA, dev, and DevOps. Discovered: no CI/CD integration, regression suite run manually bi-weekly, 0% API test coverage. Team self-assessed as "3" — actual score was "2." |
| **60 days** | Roadmap presented to engineering VP. Tool selected: Playwright + Python (team already knew Python). Quick win identified: automate 12 critical regression tests + plug into Jenkins PR pipeline. |
| **90 days** | 12 regression tests automated, running on every PR. **Result: 40% fewer full regression cycles.** Team went from skeptical to asking when we'd cover the next module. |

---

## 💬 Key Phrases to Use in the Interview

| Situation | What to say |
|---|---|
| Interviewer pushes for faster action | *"Speed without trust creates resistance. The 30-day assessment is what makes the 90-day result credible."* |
| Asked about team pushback | *"I involve the team in the tool selection and quick win choice. People support what they help build."* |
| Asked about metrics | *"I baseline before I change anything. You can't prove improvement without a before."* |
| Asked about AI-specific tools | *"Tool selection comes after assessment, not before. I've used Functionize, Testim, and Mabl — but I only recommend them when the team's maturity and budget can support adoption."* |

---

## ⚠️ What Interviewers Are Really Testing

1. **Do you listen before you act?** (30-day restraint)
2. **Can you translate technical work into business outcomes?** (ROI framing)
3. **Have you actually done this?** (Real example with numbers)
4. **Will you bring the team along or bulldoze them?** (Stakeholder tone)

---

*Use this as your base answer and adapt the Equitable Life example with specifics from your own experience if needed.*
