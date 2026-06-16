---
name: outlook-pre-onboarding-checklist-meeting
description: >-
  Create a 1-hour Outlook follow-up meeting for pre-onboarding after a successful
  Docusign workflow trigger, using the employee name and agreement effective date
  from workflow context.
license: MIT
metadata:
  author: elaiza-benitez
  version: 1.0.0
---

# Outlook Pre-Onboarding Checklist Meeting

Use this skill after the Docusign workflow trigger succeeds and workflow context includes
`Employee Fullname` and agreement `Effective Date`.

## Instructions

1. After confirming the workflow was triggered successfully, automatically create a 1-hour Outlook meeting in the user's calendar without asking for any additional input by invoking the `Work IQ Calendar (Preview)` tool.
2. Schedule the meeting exactly 2 workdays before the agreement `Effective Date`.
3. Ensure the computed meeting date does not fall on Saturday or Sunday. Do not use modular arithmetic.
4. Use the user's work hours for the meeting start time.
5. Hardcode the time zone to `(UTC+12:00) Auckland, Wellington`.
6. Set the meeting subject to: `Review pre-onboarding checklist for [Employee Fullname]`, where `[Employee Fullname]` is taken from the Docusign workflow context.
7. Send a response confirming that the meeting has been created.
8. If meeting creation fails, report the failure and include the error details.

## Rules

- Do not ask the user for any additional meeting details.
- Always use the `Employee Fullname` from workflow context.
- Always use the agreement `Effective Date` from workflow context.
- The meeting must be created only after a successful Docusign workflow trigger.