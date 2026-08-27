---
name: JIRA Requirement Analyser
description: >-
  Read a JIRA ticket and judge whether it is actually ready to test. Use when a
  tester says "analyze this ticket", "is this story ready to test", "find gaps in
  JIRA-123", or pastes a user story / acceptance criteria and wants it pressure-tested.
  Fetches the ticket, scores it against a readiness checklist, and returns a
  gaps / ambiguities / risks report plus clarifying questions to send back to the author.
---

# Test Case Template

Use the ticket details below to generate an enterprise-grade, traceable set of test cases.

## Ticket

- **Key:** {{TICKET_KEY}}
- **Summary:** {{SUMMARY}}
- **Description:**
  {{DESCRIPTION}}
- **Acceptance Criteria:**
  {{ACCEPTANCE_CRITERIA}}

## Required Output Format

Return the test cases as a single markdown table with these columns, in this exact order:

| TID | Test Case Description | Pre-Condition | Test Steps | Expected Result | Priority | Is Automated |

Rules:
- Generate a minimum of 5 test cases; add more if the ticket coverage requires it.
- Cover both valid (positive) and invalid (negative) scenarios.
- Base every test case strictly on the ticket content above. Do not invent features,
  error codes, UI elements, or behavior that is not present in the ticket.
- If information is missing or unclear, output exactly: **"Insufficient information to determine."**
- If a detail is inferred rather than stated, label it exactly: **"Inference (low confidence)"**.
- Output the markdown table only. No preamble, no explanation, no text outside the table.
