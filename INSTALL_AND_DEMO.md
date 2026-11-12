# TrustFlow AI — Three-upgrade pack

Includes (1) public GitHub PR evidence inspection, (2) structured explainable Gemini reviews, and (3) AG Grid Community milestone/payment workspace with searching, sorting, filtering, and CSV export.

## Safety first

On your Mac, inside your existing TrustFlow folder, save your working code before replacing anything:

```bash
git status
git add app.py dashboard.html requirements.txt
git commit -m "Checkpoint working PayPal sandbox MVP"
cp app.py app.before_upgrade.backup
cp dashboard.html dashboard.before_upgrade.backup
cp trustflow.db trustflow.before_upgrade.backup.db
```

Backups are local and should **not** be published; `.gitignore` should exclude `*.db` and `*.backup`.

## Installation

1. Copy the supplied `github_evidence.py` and `dashboard.html` into your local TrustFlow folder, replacing only `dashboard.html`.
2. Add this to the BOTTOM of `app.py`, outside all functions, only once:

```python
from github_evidence import install_github_evidence
install_github_evidence(app, globals())
```

3. Preserve your existing Gemini and PayPal `.env` settings. No new secrets are required for public GitHub PRs; unauthenticated GitHub API access is rate-limited.
4. Start with `python -m uvicorn app:app --reload` and open `http://127.0.0.1:8000/`.
5. Load an existing project using its ID. Confirm prior paid milestones and PayPal capture IDs are unchanged.

## Test evidence with a real PR

- Create a *new* $3 or $30 test project with criteria that can be supported by code changes (e.g. 'add a responsive navigation bar').
- Make a new branch in your GitHub repository, commit a small change, push it and open a *public pull request* targeting `main`.
- Paste its full `https://github.com/OWNER/REPO/pull/NUMBER` link into **Public GitHub PR evidence** on the matching pending milestone.
- Click **Inspect GitHub PR with Gemini**; expect a structured report of supported and unverified criteria.
- If the report says `needs_revision`, that is a valid and meaningful safety result. Only `recommend_approve` enables the existing manual approval step.
- Under **Payment intelligence workspace**, use search, filters and CSV export to demonstrate AG Grid.

## Limitations

- The PR reviewer inspects public PR metadata and a maximum of 20 changed files / 14,000 patch characters. It does not run code, check deployment, verify signatures, or certify work. The report shows coverage.
- No authentication and role-based access control: run only as a local single-user sandbox prototype. **Never publicly expose this server**.
- Sandbox payments only; do not claim escrow or production safety.
- Existing paid milestone rows are not modified by the extension. Never retry payment for a paid milestone.
- AG Grid Community is loaded through a version-pinned CDN; the visual table requires internet. The payment backend is independent of AG Grid.

## Publishing after testing

```bash
git add app.py dashboard.html github_evidence.py README.md
git commit -m "Add GitHub evidence review and AG Grid payment intelligence"
git push
```

Update README to describe the new endpoints and AG Grid.
