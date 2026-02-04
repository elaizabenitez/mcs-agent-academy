---
name: analytics-report
description: Generate an Agent Academy analytics report using Microsoft Clarity data and GitHub badge statistics. Use this skill to create HTML dashboard reports showing session trends, user metrics, and badge completion stats for Recruit, Operative, and Commander courses.
---

# Agent Academy Analytics Report Generator

This skill generates a comprehensive HTML analytics dashboard for Agent Academy, pulling data from Microsoft Clarity and GitHub issue statistics.

## Report Overview

The report includes:
- **Agent Academy (Overall)**: Total sessions, weekly trends, daily trends with projections
- **Performance by Course**: Bar chart comparing all courses (Recruit, Operative, Commander)
- **Recruit Section**: Sessions, users, weekly/daily charts, badge statistics
- **Operative Section**: Sessions, users, weekly/daily charts, badge statistics

## Data Sources

### Microsoft Clarity
Use the Clarity MCP tools to query analytics data:
- `mcp_clarity_mcp_query-analytics-dashboard` for session and user counts

### GitHub Issues
Use the GitHub MCP tools to count badge requests:
- `mcp_github_mcp_search_issues` for counting issues with specific labels

## Step-by-Step Generation Process

### 1. Query Overall Agent Academy Stats

```
Query: Total sessions and unique users for Agent Academy for the last 4 complete weeks
```

### 2. Query Weekly Breakdown (Last 4-5 Weeks)

For each section (overall, recruit, operative):
```
Query: Sessions and unique users per week for pages containing "/[section]/" for the last 4 complete weeks
```

### 3. Query Daily Data (Last 2 Weeks)

For each section:
```
Query: Daily sessions and unique users for pages containing "/[section]/" for the last 2 complete weeks plus current partial week
```

### 4. Query Badge Statistics from GitHub

**Recruit Badges:**
- Requested (pending): `repo:microsoft/agent-academy label:recruit-completed is:open`
- Awarded via Credly: `repo:microsoft/agent-academy label:recruit-completed label:recruit-badge-issued is:closed`
- Awarded via Global AI Community: `repo:microsoft/agent-academy label:recruit-completed label:recruit-badge-issued-gaic is:closed`

**Operative Badges:**
- Requested (pending): `repo:microsoft/agent-academy label:operative-completed is:open`
- Awarded: `repo:microsoft/agent-academy label:operative-completed label:operative-badge-issued is:closed`

**Commander Badges** (when available):
- Requested (pending): `repo:microsoft/agent-academy label:commander-completed is:open`
- Awarded: `repo:microsoft/agent-academy label:commander-completed label:commander-badge-issued is:closed`

## Report Structure

### File Location
```
reports/YYYYMMDD-analytics-overview.html
```

### Required Sections

1. **Header**: Title and generation date
2. **Agent Academy Section**:
   - Stats cards (Total Sessions, Last 4 Weeks Sessions, Last 4 Weeks Users)
   - Weekly Trend line chart
   - Last 2 Weeks daily chart with projections
   - Performance by Course bar chart
   - Weekly data table
3. **Tabbed Courses Section**:
   - Tab buttons for each course
   - Each course panel includes:
     - Stats cards (Sessions, Users, Share of Total)
     - Weekly Trend line chart
     - Daily chart with projections
     - Weekly data table
     - Badge stats (Total Requests, Awarded, Pending)

### Theme: GitHub Dark Dimmed

Use these colors:
- Background: `#22272e`
- Surface/Cards: `#2d333b`
- Border: `#444c56`
- Primary Text: `#adbac7`
- Muted Text: `#768390`

Chart colors by section:
- **Agent Academy**: Blue `#539bf5`, Purple `#986ee2`
- **Recruit**: Green `#57ab5a`, Teal `#96d0ff`
- **Operative**: Red `#f47067`, Blue `#539bf5`
- **Commander**: Purple `#986ee2`, Green `#57ab5a` (when added)

### Chart Configuration

Use Chart.js from CDN:
```html
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
```

Chart options:
- Line charts with `fill: true` for area effect
- Remove point markers: `point: { radius: 0, hoverRadius: 4 }`
- Projection lines: `borderDash: [5, 5]`
- Hide projection entries from legend using filter function

### Projection Calculation

Daily projections should:
- Start from the last complete day (not partial current day)
- Use patterns from previous weeks (same day of week)
- Show as dotted lines with reduced opacity fill

## Sample Clarity Queries

### Overall Sessions
```
Total sessions for agent-academy.github.io for the last 4 complete weeks
```

### Weekly by Section
```
Sessions and unique users per week for pages containing "/recruit/" for the last 4 complete weeks
```

### Daily by Section
```
Daily sessions and unique users for pages containing "/operative/" for the last 2 complete weeks plus current partial week
```

## Badge Stats Display

Each course section should show:
```
Total Badge Requests: [awarded + pending]
Badges Awarded: [closed issues with badge-issued label]
Badges Requested (pending): [open issues with completed label]
```

## Footer

Include data source attribution:
```html
<footer>
    <p>Data sourced from Microsoft Clarity | Agent Academy</p>
</footer>
```

## Example Prompt

Use this prompt to generate a new report:

---

**Generate an Agent Academy analytics report for today.**

Please create an HTML report at `reports/YYYYMMDD-analytics-overview.html` with:

1. **Microsoft Clarity data** for Agent Academy:
   - Overall sessions and users (all time and last 4 complete weeks)
   - Weekly breakdown for overall, `/recruit/`, and `/operative/` paths (last 4 complete weeks)
   - Daily breakdown for last 2 complete weeks plus current partial week, with projections

2. **GitHub badge statistics** from microsoft/agent-academy:
   - Recruit: count issues with `recruit-completed` label (open = pending, closed with `recruit-badge-issued` or `recruit-badge-issued-gaic` = awarded)
   - Operative: count issues with `operative-completed` label (open = pending, closed with `operative-badge-issued` = awarded)

3. **Report features**:
   - GitHub Dark Dimmed theme
   - Line charts with area fill for trends
   - Bar chart comparing course performance
   - Tabbed interface for Recruit/Operative sections
   - Dotted projection lines for current week predictions
   - Badge statistics with Total/Awarded/Pending breakdown

---

## Adding New Courses

When Commander (or other courses) launch:

1. Add a new tab button in the tabs-header
2. Create a new tab-panel with the same structure as Recruit/Operative
3. Query Clarity for `/commander/` path data
4. Query GitHub for commander badge labels
5. Update the Performance by Course chart with real data (remove "coming soon")
6. Choose a new color pair for the course charts

## Maintenance Notes

- Clarity API requires the `CLARITY_AUTH_TOKEN` environment variable
- GitHub MCP tools use authenticated access via VS Code
- Week numbers are ISO week numbers (Week 1 starts first Monday of year)
- Projections are estimates based on historical patterns, not guarantees
