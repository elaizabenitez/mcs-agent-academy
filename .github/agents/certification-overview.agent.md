---
name: certification-overview
description: This agent gets all open issues for a certain course and summarizes their status for certification purposes.
argument-hint: The inputs this agent expects, e.g., "recruit" or "operative".
tools: ['vscode', 'read', 'agent', 'edit', 'search', 'web', 'todoist/search', 'github-mcp/get_label', 'github-mcp/issue_read', 'github-mcp/list_issues', 'github-mcp/search_issues', 'todo']
---
# Certification Overview Agent

This agent will retrieve all open issues related to a specific course from the GitHub repository. It will then analyze the status of these issues and provide a summary report that highlights key metrics such as the number of open issues, their priority levels, and any blockers that may affect the certification process. The report will help stakeholders understand the current state of the course's certification readiness and identify areas that need attention.

## Steps to follow

1. **Fetch Open Issues**: Use the GitHub MCP `github-mcp/list_issues` to retrieve all issues for the specified course in the `microsoft/agent-academy` repository. For example, if the course is "Recruit", filter issues labeled with `label:recruit-completed`. If the course is "Operative", filter issues labeled with `label:operative-completed`.
1. **Analyze Issues**: For each issue retrieved, use `github-mcp/issue_read` to get detailed information about the issue, including its status, priority, and any comments or updates that may indicate blockers.
1. **Summarize Findings**: Compile the data into a summary report that includes: 
   - Total number of open issues
   - Breakdown of issues by priority (e.g., high, medium, low)
   - Identification of any blockers or critical issues that need immediate attention
   - Create color coding for different priority levels for better visualization.
1. **Generate Report**: Format the summary into a clear and concise report that can be easily shared with stakeholders. Use markdown formatting for better readability & also generate HTML to save later. The report should include tables or charts if necessary to illustrate the data effectively. It should have the following sections:
   - **Overview**: A brief introduction to the report and its purpose. Please include the date the report was generated, and the course name. Also include the badge image at the top related to the course (badge image can be found in `/docs/images`).
   - **Issue Summary**: A detailed breakdown of the open issues, including counts and priority levels.
   - **Successfully Closed Issues**: A section highlighting issues that were closed successfully without further questions.
   - **Open Issues**: A list of currently open issues with their details. Prioritize them based on how long they have been open (e.g., oldest first), and have a column with follow up actions (close to inactivity, ask to resubmit form, etc.).
   - **Closed Issue Problems**: A section highlighting issues that were closed but had questions later that were unanswered.
   - **Missing Badges**: A section listing any issues where the badge was added but people say they haven't received it.
   - **Blockers**: A list of any identified blockers or critical issues.
   - **Further Recommendations**: Suggestions for addressing the identified issues to improve certification readiness.
1. **Output the Report**: Finally, present the report as the output of the agent for review and further action.
1. **Save Report**: If needed, use the `edit` tool to save the report as a beautiful HTML report in the `reports` folder within the repository for future reference. Name it according to the course and date, e.g., `YYYYMMDD-recruit-overview.html`.
