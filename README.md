# Evidence Reuse Intelligence System
### A Multi-Agent AI System for CPA Engagement Teams

# Evidence Reuse Intelligence System
### A Multi-Agent AI System for CPA Engagement Teams


## What This Is

A multi-agent document intelligence system that helps CPA teams surface reusable evidence from prior-year engagements before opening a new client engagement cycle.

Instead of starting every recurring engagement with a blank document request list, this system tells you:

- What evidence likely already exists from prior engagements
- What exists but needs validation before reuse
- What is period-specific and must be collected fresh

One input. One structured brief. Less client friction. Faster engagement prep.

---

## The Problem It Solves

Every CPA team running recurring engagements knows this cycle.

Same client. Same engagement type. Quarter after quarter, year after year.

And yet, the evidence request goes out as if nothing has ever been done before.

Bank statements the firm already has. Organizational charts unchanged for two years. Policy documents sitting in a workpaper system, unlabeled and unfound.

This system breaks that cycle.

---

## How It Works

### Input (4 fields)

| Field | Description |
|---|---|
| `client_name` | Name of the client entity |
| `engagement_type` | Audit / Review / Compilation / Tax / AUP |
| `fiscal_year` | The engagement fiscal year |
| `client_status` | `existing` or `new` |

### Output (Structured Evidence Brief)

The system returns evidence organized into three categories:
✅ LIKELY REUSABLE
Evidence available from prior engagements with high reuse confidence.

⚠️ REUSABLE WITH VALIDATION
Evidence that exists but requires a confirmation step before relying on it.

🔄 COLLECT FRESH
Period-specific or engagement-context evidence that must come from the client.

text

---

## Evidence Reusability Framework

The system reasons across four evidence dimensions:

### 1. Entity-Level Evidence
Organizational charts, governing documents, policies, operating procedures.
Often reusable with a simple confirmation that nothing material has changed.

### 2. Operational and Control Evidence
Internal control narratives, process walkthroughs, system descriptions, access logs.
Reusable if underlying systems and processes have not changed materially since the prior period.

### 3. Period-Specific Financial Evidence
Bank statements, confirmation letters, period-end balances, transaction samples.
Always flagged as requiring fresh collection. These are intrinsically tied to a specific fiscal period.

### 4. Engagement-Context Documents
Management representation letters, engagement letters.
Always refreshed per engagement cycle regardless of client continuity.

---

## New Client vs. Existing Client

| Scenario | System Behavior |
|---|---|
| **Existing client** | Reasons against prior engagement history. Returns differentiated reuse view. |
| **New client** | Resets to baseline. Returns full evidence set required for the engagement type. |
| **Existing but changed** | Flags scenarios where client context has shifted enough to require fresh evidence despite prior history. |

---

## Architecture
┌─────────────────────────────────┐
│ Frontend (Input UI) │
│ client · engagement · year · │
│ new or existing │
└────────────────┬────────────────┘
│
▼
┌─────────────────────────────────┐
│ Orchestration Agent │
│ Routes by engagement type │
│ and client status │
└────────────────┬────────────────┘
│
┌────────┴────────┐
▼ ▼
┌───────────────┐ ┌───────────────┐
│ Evidence │ │ Reusability │
│ Retrieval │ │ Classifier │
│ Agent │ │ Agent │
└───────┬───────┘ └───────┬───────┘
└────────┬──────────┘
▼
┌─────────────────────────────────┐
│ Structured Brief Output │
│ Reusable · Validate · Fresh │
└─────────────────────────────────┘

text

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | v0 (Vercel) |
| Workflow Orchestration | n8n |
| LLM | OpenAI GPT-4o (swappable for Claude, Gemini, Mistral) |
| Evidence Storage | Your existing document / workpaper system |
| Output Format | Structured JSON / downloadable brief |

---

## Getting Started

### Prerequisites

- Node.js 18+
- n8n instance (cloud or self-hosted)
- OpenAI API key (or your preferred LLM provider)
- Access to your firm's document or workpaper storage

### Installation

```bash
git clone https://github.com/yourusername/evidence-reuse-intelligence.git
cd evidence-reuse-intelligence
npm install
```

### Configuration

Create a `.env` file in the root directory:

```env
OPENAI_API_KEY=your_openai_api_key
N8N_WEBHOOK_URL=your_n8n_webhook_url
DOCUMENT_STORE_API=your_document_store_endpoint
```

### Running Locally

```bash
npm run dev
```

Navigate to `http://localhost:3000` to access the input UI.

### Deploying the n8n Workflow

1. Open your n8n instance
2. Import `workflow/evidence-reuse-workflow.json`
3. Update the webhook URL in your `.env` file
4. Activate the workflow

---

## Sample Input

```json
{
  "client_name": "Acme Corporation",
  "engagement_type": "audit",
  "fiscal_year": "2025",
  "client_status": "existing"
}
```

## Sample Output

```json
{
  "client": "Acme Corporation",
  "engagement": "Annual Audit - FY2025",
  "brief": {
    "reusable": [
      "Organizational chart (FY2024) — confirm no structural changes",
      "Entity governing documents — confirm amendments since last engagement",
      "IT general controls walkthrough — confirm no system changes"
    ],
    "validate_before_reuse": [
      "Internal control narratives — confirm process changes since FY2024",
      "Risk assessment documentation — review for updated risk factors"
    ],
    "collect_fresh": [
      "Bank statements — FY2025 period required",
      "Management representation letter — required per engagement cycle",
      "Period-end account balances — FY2025 specific",
      "Engagement letter — refresh required"
    ]
  }
}
```

---

## Roadmap

- [ ] Integration with common workpaper platforms (CaseWare, Thomson Reuters, Wolters Kluwer)
- [ ] Multi-entity client support
- [ ] Engagement history trend view across multiple prior years
- [ ] Automated client-facing document request generation from fresh evidence list
- [ ] RAG layer for pulling context from prior engagement notes and reviewer comments
- [ ] Audit trail and evidence version tracking

---

## Why I Built This

This system came out of a recurring observation: professional service teams spend significant time collecting evidence they already have, asking clients for things they already provided, and rebuilding context that exists somewhere in the system but is never surfaced at the right moment.

The AI does not replace professional judgment. It removes the overhead of starting from zero every time.


---

## Connect

Built by **Roly Arora**
Newsletter: [The Aligned PM (TAPM)](https://substack.com/@thealignedpm)
LinkedIn: [Your LinkedIn Profile](https://www.linkedin.com/in/rolyarora/)
