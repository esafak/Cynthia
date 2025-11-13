# Proactive Project Management Web App - Specification

## 1. Overview

A proactive project management application that uses predictive analytics to alert users **before** problems occur, rather than reacting after issues have happened. Built with Oracle Redwood Design System.

### Key Differentiator
**Proactive vs Reactive**: The app forecasts issues and provides early warnings:
- Alert when tasks are trending toward being late (before they're overdue)
- Predict budget overruns based on current burn rate and trends (before budget is exhausted)

---

## 2. User Personas

### Project Manager (PM)
- **Usage**: Daily, detailed project management
- **Scope**: Manages 5-10 projects simultaneously
- **Needs**:
  - Multi-project overview with health indicators
  - Drill-down into individual projects
  - Configure alert thresholds per project
  - Budget forecasting and cost tracking
  - Team workload visibility

### Team Member
- **Usage**: Daily task updates
- **Scope**: Works on 1-3 projects maximum
- **Needs**:
  - View assigned tasks
  - Update task progress (% and time)
  - Simple, focused interface
  - See their contribution to project health

### Executive
- **Usage**: Weekly high-level review
- **Scope**: Portfolio overview across all projects
- **Needs**:
  - Dashboard with key metrics
  - Project health scores
  - Budget vs actual across portfolio
  - Trend analysis

---

## 3. Core Data Model

### Project
- **Attributes**:
  - Name
  - Description
  - Status (Planning, Active, On Hold, Completed)
  - Planned Start Date
  - Planned End Date
  - Total Budget (fixed + time-based)
  - Project Manager (owner)
  - Team Members (assigned resources)
  - Health Score (calculated)

### Task
- **Attributes**:
  - Title
  - Description
  - Status (To Do, In Progress, Blocked, Done)
  - Planned Start Date
  - Planned Finish Date
  - Estimated Effort (hours)
  - Actual Time Logged (hours)
  - Percentage Complete (0-100%)
  - Assigned To (team member)
  - Priority (High, Medium, Low)
  - Project (parent)

### Resource/Team Member
- **Attributes**:
  - Name
  - Role
  - Hourly Rate (for cost calculation)
  - Email
  - Active Projects (list)

### Budget/Costs
- **Fixed Costs**:
  - Description
  - Category (Materials, Licenses, External Vendors, Other)
  - Amount
  - Date Incurred
  - Project

- **Time-Based Costs** (Auto-calculated):
  - Resource Hourly Rate × Hours Logged
  - Calculated per task, rolled up to project

### Alert Thresholds (Configurable per PM)
- **Task Alert**:
  - Days Before Due (default: 3 days)
  - Completion Threshold (default: < 50%)

- **Budget Alert**:
  - Forecast Overrun % (default: 25%)

---

## 4. Predictive Alert Logic

### Task Due Date Alert
**Trigger**: Task is trending toward being late
**Conditions**:
- Current date is within X days of planned finish date (default: 3 days)
- AND Percentage complete < Y% (default: 50%)
- AND Task status ≠ Done

**Alert Message**: "Task '[Task Name]' due in 2 days but only 30% complete"

**Advanced Logic** (future enhancement):
- Calculate velocity: % complete / days elapsed
- Project completion date based on velocity
- Alert if projected completion > planned finish date

### Budget Overrun Alert
**Trigger**: Project is trending toward budget overrun
**Conditions**:
- Calculate burn rate: (total costs to date) / (days elapsed)
- Project total cost at completion: burn rate × total project days
- If projected cost > budget × (1 + threshold%), trigger alert

**Alert Message**: "Project 'ABC' forecasted to exceed budget by 28% based on current burn rate"

**Calculation Example**:
- Budget: $100,000
- Days elapsed: 30 out of 90
- Costs to date: $45,000
- Burn rate: $45,000 / 30 = $1,500/day
- Projected total: $1,500 × 90 = $135,000
- Overrun: 35% → **Alert triggered** (threshold 25%)

### Task Not Started Alert
**Trigger**: Task past planned start date but not started
**Conditions**:
- Current date > planned start date
- Status = "To Do"
- % complete = 0%

**Alert Message**: "Task '[Task Name]' was scheduled to start 2 days ago but hasn't been started"

### Effort Overrun Alert
**Trigger**: Task effort exceeding estimate
**Conditions**:
- Actual time logged > estimated effort × 0.9 (90% threshold)
- Status ≠ Done

**Alert Message**: "Task '[Task Name]' has used 12 of 10 estimated hours"

---

## 5. Calculated Metrics

### Project Health Score
Composite score (0-100) based on:
- **Schedule Health** (40%): % of tasks on track vs late/at-risk
- **Budget Health** (40%): Projected cost vs budget
- **Completion Health** (20%): % of tasks completed on time

**Scoring**:
- 80-100: Green (Healthy)
- 60-79: Yellow (At Risk)
- 0-59: Red (Critical)

### Task Health
- **On Track**: % complete ≥ expected based on timeline, within effort estimate
- **At Risk**: Trending toward late or over effort (alert conditions)
- **Overdue/Over Budget**: Past due date or over effort estimate

### Budget Variance
- **Formula**: ((Actual + Projected Costs) - Budget) / Budget × 100
- Positive = over budget, Negative = under budget

---

## 6. UI Screens (Oracle Redwood Design System)

### Screen 1: Dashboard (Multi-Project Overview)
**Purpose**: Show all projects with health indicators and alerts

**Components**:
- **Header**:
  - App title
  - User profile
  - Notification bell (alert count)

- **Alert Panel** (Top):
  - Prioritized list of alerts across all projects
  - Color-coded by severity (red, yellow, blue)
  - Click to navigate to related project/task

- **Project Cards Grid**:
  - Card per project showing:
    - Project name
    - Health score (visual indicator: green/yellow/red)
    - Progress bar (% complete)
    - Budget status ($ actual vs $ budget)
    - Active alerts count
    - Quick stats (tasks due this week, at-risk tasks)

- **Key Metrics** (Top summary):
  - Total projects
  - Projects at risk
  - Total budget vs actual
  - Tasks due this week

**Redwood Elements**:
- Cards with elevation
- Progress bars
- Status badges
- Alert banners
- Icon buttons

---

### Screen 2: Project Detail (Single Project)
**Purpose**: Detailed view of one project with comprehensive insights

**Components**:
- **Project Header**:
  - Project name
  - Status badge
  - Health score (large visual)
  - Date range
  - PM and team avatars

- **Alerts Section**:
  - Project-specific alerts
  - Collapsible panel

- **Key Metrics Row**:
  - Tasks (total, complete, at-risk, overdue)
  - Budget (allocated, spent, forecasted)
  - Timeline (days elapsed, days remaining)
  - Team (member count, workload)

- **Tabs**:
  1. **Tasks Tab**:
     - Filterable/sortable task list
     - Columns: Title, Assignee, Status, Due Date, Progress %, Hours (actual/est), Health
     - Inline editing for % complete

  2. **Timeline Tab** (future):
     - Gantt chart view

  3. **Budget Tab**:
     - Link to detailed budget page

  4. **Team Tab**:
     - Team member cards
     - Workload per person

- **Insights Panel** (Right sidebar):
  - Trend charts (budget burn, completion velocity)
  - Forecast projections
  - Risk indicators

**Redwood Elements**:
- Tabs component
- Data table with sorting/filtering
- Charts (line, bar)
- Progress indicators
- Avatar groups
- Collapsible panels

---

### Screen 3: Budget Detail Page
**Purpose**: Comprehensive budget tracking and cost forecasting

**Components**:
- **Budget Header**:
  - Project name breadcrumb
  - Total budget
  - Actual costs to date
  - Forecasted total
  - Variance ($ and %)

- **Budget Health Indicator**:
  - Large visual gauge showing % of budget used vs % of project complete
  - Green/yellow/red status

- **Cost Breakdown**:
  - **Fixed Costs Table**:
    - Columns: Description, Category, Amount, Date
    - Add new fixed cost button
    - Total fixed costs

  - **Time-Based Costs Table**:
    - Grouped by resource
    - Columns: Resource, Hours Logged, Rate, Total Cost
    - Drill-down to task-level time entries
    - Total labor costs

- **Forecast Chart**:
  - Line chart showing:
    - Budget (horizontal line)
    - Actual costs (line to date)
    - Projected costs (dotted line extending to end date)
    - Burn rate trend
  - X-axis: Timeline
  - Y-axis: Cost ($)

- **Alerts Section**:
  - Budget-related alerts
  - Recommendations (e.g., "Reduce scope by 15% to stay within budget")

- **Cost Analysis Cards**:
  - Burn rate ($/day)
  - Projected completion cost
  - Budget remaining
  - Days of budget remaining at current burn rate

**Redwood Elements**:
- Data tables with totals
- Line charts with multiple series
- Gauge/radial progress
- Alert banners
- Cards with metrics
- Action buttons

---

## 7. Design System: Oracle Redwood

### Visual Style
- **Colors**:
  - Primary: Oracle Red (#C74634)
  - Success: Green (#3A8026)
  - Warning: Yellow (#F5C344)
  - Error: Red (#C74634)
  - Info: Blue (#2B5A9E)
  - Neutral: Grays (#F8F8F8, #E0E0E0, #666666)

- **Typography**:
  - Font family: Oracle Sans
  - Headings: Bold, hierarchical sizing
  - Body: Regular, 14px base

- **Spacing**:
  - 8px grid system
  - Consistent padding/margins

### Components to Use
- **Layout**: Header, sidebar, content area
- **Navigation**: Tabs, breadcrumbs, navigation list
- **Data Display**: Tables, cards, lists, badges, avatars
- **Charts**: Line, bar, donut, gauge (Oracle JET Charts)
- **Forms**: Inputs, selects, datepickers, sliders
- **Feedback**: Alerts, progress bars, status indicators
- **Actions**: Buttons, icon buttons, menus

### Responsive Design
- Desktop-first (primary use case)
- Tablet support (landscape)
- Mobile support (future phase)

---

## 8. Technical Considerations

### Data Requirements
- Real-time updates for task progress
- Historical data for trend analysis
- Configurable alert thresholds (stored per PM/project)

### Calculations
- Budget forecasting runs on task update
- Health scores recalculated on project data change
- Alert checks run periodically (every hour) and on data updates

### Permissions (Future)
- PM: Full access to their projects
- Team Member: View projects, edit assigned tasks
- Executive: Read-only dashboard access

---

## 9. Future Enhancements

- **Timeline/Gantt View**: Visual project schedule with dependencies
- **Team Workload View**: Resource allocation across projects
- **What-if Analysis**: Scenario planning (add resources, adjust scope)
- **Automated Reports**: Weekly summary emails
- **Mobile App**: Native iOS/Android
- **Integrations**: Calendar, Slack, JIRA
- **Advanced Forecasting**: Machine learning for more accurate predictions
- **Task Dependencies**: Critical path analysis
- **Time Tracking Integration**: Timesheets

---

## 10. Success Metrics

- **Proactive Alert Accuracy**: % of alerts that prevent actual issues
- **Early Problem Detection**: Average days between alert and would-be issue
- **User Adoption**: Daily active users (PM and team members)
- **Time Savings**: Reduced time spent in status meetings
- **Budget Accuracy**: Improved forecast accuracy vs actual costs

---

## 11. MVP Scope Summary

### Must-Have for Prototype
✅ Dashboard with multi-project overview and alerts
✅ Project detail page with insights and task list
✅ Budget detail page with forecasting
✅ Predictive alerts (task due date, budget overrun)
✅ Task tracking (time + percentage)
✅ Cost tracking (fixed + time-based)
✅ Health scores
✅ Oracle Redwood design system

### Phase 2
- Settings page (configure thresholds)
- Timeline/Gantt view
- Team workload management
- Advanced forecasting algorithms
- Report generation

---

**Document Version**: 1.0
**Last Updated**: 2025-11-13
**Status**: Ready for UI Prototype Development
