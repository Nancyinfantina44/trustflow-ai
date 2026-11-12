# TrustFlow AI

**Pay for progress, not just promises.**

TrustFlow AI is an AI-assisted milestone payment platform
powered by Google Gemini and PayPal.

## Problem

Freelancers and clients often struggle with unclear project
milestones, manual approvals, and disconnected payment tracking.

## Solution

TrustFlow AI helps users:
- Generate project milestones using AI.
- Define measurable acceptance criteria.
- Review submitted evidence with Gemini.
- Inspect public GitHub pull request metadata and sampled patches with Gemini.
- Approve milestones through human authorization.
- Process payments using PayPal Sandbox.
- Track payment history and transaction records in a searchable, sortable,
  filterable AG Grid Community workspace with CSV export.

## Technologies

- Python
- FastAPI
- Google Gemini API
- PayPal Orders v2 API
- PayPal JavaScript SDK
- SQLite
- HTML, CSS, JavaScript

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/Nancyinfantina44/trustflow-ai.git
cd trustflow-ai
```

### 2. Create a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Configure environment variables

Copy `.env.example` to `.env`.

Add your own Gemini API key, working Gemini model, and PayPal Sandbox credentials.

### 5. Run the application

```bash
python -m uvicorn app:app --reload
```

Open http://127.0.0.1:8000

## Review and payment workspace

- `POST /api/milestones/{id}/review` reviews a user-provided evidence description
  and returns a structured Gemini assessment with a decision, summary, supported
  criteria, and criteria still missing or unverified.
- `POST /api/milestones/{id}/review-github` accepts a public GitHub pull request
  URL and compares its metadata and sampled changed-file patches with the
  milestone criteria. `GET /api/milestones/{id}/github-review` returns the
  saved explainable report.
- `GET /` serves the workspace. Its AG Grid Community table supports searching,
  sorting, filtering, and CSV export for the currently selected project.

GitHub inspection uses bounded samples of public PR metadata and changed-file
patches: at most 20 files and 14,000 patch characters. It does not run the code,
so it cannot prove that the code works or that a client accepted the work. It
also does not verify deployment or signatures. AG Grid is loaded from a
version-pinned CDN, so the visual grid requires internet access; payment
processing does not depend on AG Grid.

## Demo Workflow

1. Create a project with a budget.
2. Gemini generates three milestones.
3. Submit evidence for AI review.
4. Review the AI recommendation.
5. Approve the milestone manually.
6. Pay through PayPal Sandbox.
7. View the verified payment and audit trail.

## Important Limitations

This is a hackathon prototype intended for sandbox testing.

- No real-money transactions are required.
- It is not an escrow service.
- AI evaluates user-provided evidence descriptions.
- External evidence is not independently verified.
- Authentication and production security are not implemented.
- Run only as a local, single-user sandbox prototype. Never publicly expose
  this server.
- Existing paid milestone rows and PayPal capture IDs are not modified by
  GitHub review. Never retry payment for a paid milestone.

## License

MIT License.
