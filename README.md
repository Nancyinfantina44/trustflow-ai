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
- Approve milestones through human authorization.
- Process payments using PayPal Sandbox.
- Track payment history and transaction records.

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
git clone https://github.com/YOUR_USERNAME/trustflow-ai.git
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

## License

MIT License.
