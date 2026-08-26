# JiraAIHelper 🎯

A lightweight Streamlit app that turns Jira tickets into QA deliverables using
Groq-hosted LLMs. It has two modes:

- **Generate Test Cases** — paste a Jira key (e.g. `QA-102`) and get an
  enterprise-grade, traceable test case table based on the ticket's summary,
  description and acceptance criteria.
- **Analyse Requirement** — pressure-test whether a ticket is actually ready to
  test: it scores the story, surfaces gaps / ambiguities / risks, and drafts
  clarifying questions for the author. If Jira is unreachable, you can paste the
  ticket body and analyse it anyway.

## How it works

1. You type a Jira ticket key in the chat.
2. The app fetches the ticket (summary, description, acceptance criteria) via
   the Jira Cloud REST API using the credentials saved in Settings.
3. The ticket content is merged into a prompt template from `templates/`.
4. Groq generates the test cases / analysis report, which is rendered in the
   chat pane. Test cases can be exported to CSV.

## Project structure

```
.
├── app.py                 # Chat screen (test case generation + requirement analysis)
├── pages/
│   └── settings.py        # Jira + Groq credential form and connectivity checks
├── config_store.py        # Persists settings to local config.json (gitignored)
├── jira_client.py         # Jira REST API client (fetch ticket, check connection)
├── llm_client.py          # Groq client (test case generation, analysis)
├── templates/
│   ├── test_cases_template.md
│   └── requirement_analyse_template.md
└── requirements.txt
```

## Setup

1. **Python 3.10+** and pip.

2. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

3. **Add your credentials** — either:

   - Copy `.env.example` to `src/.env` and fill in your values (used on first
     run to seed the settings), or
   - Start the app and enter them on the **Settings** page (they are saved to a
     local, gitignored `config.json`).

   You need:
   - **Jira URL** — e.g. `https://yourcompany.atlassian.net` (or just
     `yourcompany.atlassian.net`)
   - **Jira email** — the account email for your Jira Cloud site
   - **Jira API token** — create one at https://id.atlassian.com/manage-profile/security/api-tokens
   - **Groq API key** — from https://console.groq.com/keys

4. **Run the app**

   ```bash
   streamlit run app.py
   ```

5. Open the printed local URL (default http://localhost:8501), pick a mode in
   the dropdown, and type a Jira key like `QA-102`.

## Security

- Credentials are stored only in a local, gitignored `config.json` (or read
  from `src/.env`) — never in source code.
- The Settings page includes **Check Jira Connectivity** and **Check Groq
  Connectivity** buttons to validate your credentials before generating.
