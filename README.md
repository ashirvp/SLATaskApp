# SLATaskApp

SLATaskApp is a Mendix-based application I developed to manage Service Level Agreements (SLAs) for an Internet Service Provider (ISP). Built using Mendix Studio Pro (version 10.0.0) and the **Task & Planning** app template, the app tracks SLA compliance and assigns tasks to responsible departments. I extended the template with a custom SLA Dashboard, replacing an inefficient Excel-based process with a streamlined, user-friendly solution.

## Project Overview

- **Platform**: Mendix Studio Pro 10.0.0
- **Template**: Task & Planning
- **Duration**: ~4 hours
- **Purpose**: Monitor SLA compliance, assign tasks to departments, and provide a dashboard for task and SLA management.

### Objectives

- Track whether SLAs are met for customer contracts to support pricing and negotiations.
- Assign tasks to departments and display their SLA status.
- Create an SLA Dashboard to visualize task details and SLA outcomes.
- Enable filtering to focus on missed SLAs for quick resolution.

### Use Case

As an ISP, I needed a tool to monitor SLAs defining service restoration times for customers, previously tracked in Excel. SLATaskApp displays SLA compliance, identifies responsible departments, and centralizes task management. I used the **Task & Planning** template for its task management features and customized it for SLA-specific needs.

## Features

- **SLA Dashboard**: Displays tasks with their title, completion date, SLA status (Achieved/Missed), and department, with tabs for **All** tasks and **Missed** SLAs.
- **Task Management**: Create, edit, and delete tasks with due dates, completion dates, and department assignments.
- **Department Management**: Add and view departments, with tasks linked via a one-to-many association.
- **Custom Logic**: Microflow to set SLA status based on completion vs. due dates, with validation for missing dates.
- **Data Filtering**: Filter missed SLAs and sort by recent completion dates for prioritized action.

## Development Process

### 1. Setup
I created **SLATaskApp** in the Mendix Portal using the **Task & Planning** template and set up Mendix Studio Pro 10.0.0.

- Disabled security (set to **Off**) for development.
- Explored Studio Pro’s interface (App Explorer, Properties Pane, Toolbox, Menu Bar, Dockable Panes).
- Tested the template by adding a task (“Develop Performance Presentation”).

### 2. SLA Dashboard
I built an **SLA Dashboard** page for task and SLA visualization.

- Created **SLA_Dashboard** (List template, Tasks_TopBar layout).
- Added a navigation menu item between **Team** and **My Profile**.
- Resolved an initial entity error in the next phase.

### 3. Domain Model
I extended the domain model to support SLA tracking.

- **Task Entity**:
  - Added **SLADashboardStatus** (Enumeration: SLA Achieved, SLA Missed).
  - Added **CompletionDate** (Date and Time).
- **Department Entity**: Created with **Name** (String).
- Added a one-to-many association (Department 1 : Task *).
- Updated **TaskEdit** page with **CompletionDate** date picker and **Reference Selector** for departments.

### 4. Data Connection
I connected data to pages and added department management.

- Linked **SLA_Dashboard** list view to **Task**, showing **Title**, **CompletionDate**, **SLADashboardStatus**, and **Department Name**.
- Added a delete button (trash icon) for tasks.
- Created **Department_Overview** (List template) and **Department_NewEdit** (Form vertical, popup) pages.
- Configured an **Add** button to create **Department** objects.
- Tested with departments (e.g., Implementation, Technical Support) and tasks (e.g., “Check network performance”).

### 5. Custom Logic
I extended the **SelectDoneStatus** microflow to automate SLA status.

- Added a **Decision** to validate **CompletionDate** and **DueDate** (`$Task/CompletionDate != empty and $Task/DueDate != empty`).
- Added a second **Decision** to check **CompletionDate** ≤ **DueDate**.
- Set **SLADashboardStatus** to **SLA Achieved** (true) or **SLA Missed** (false).
- Included an error message for missing dates.
- Used **MxAssist Logic Bot** for microflow suggestions.
- Tested with tasks to confirm SLA status updates.

### 6. Data Filtering
I enhanced the SLA Dashboard with filtered views.

- Added a **Tab Container** with **Missed** and **All** tabs.
- Constrained **Missed** tab to **SLADashboardStatus = SLA Missed**.
- Sorted **Missed** tab by **CompletionDate** (Descending).
- Verified **Missed** tab showed only SLA-missed tasks, while **All** showed all tasks.

## Technical Details

- **Security**: Off (development mode)
- **Pages**: SLA_Dashboard, Department_Overview, Department_NewEdit, TaskEdit
- **Domain Model**: Extended Task, new Department, one-to-many association
- **Microflow**: Extended SelectDoneStatus
- **Widgets**: List View, Tab Container, Reference Selector, Buttons, Date Picker

## Challenges & Solutions

- **Error on SLA Dashboard**: Resolved by linking list view to **Task** entity.
- **Accurate SLA Status**: Added microflow decisions and tested extensively.
- **Filtering Missed SLAs**: Used Tab Container to separate **Missed** and **All** views.
- **Department Page Error**: Fixed by creating **Department** object before opening popup.

## Future Improvements

- Enable **Production** security with user roles.
- Add charts to visualize SLA trends.
- Implement deadline notifications.
- Integrate with external systems (e.g., CRM).
- Optimize for large datasets with query refinements.

## Installation & Setup

1. Install [Mendix Studio Pro 10.0.0](https://www.mendix.com/evaluation-guide/studio-pro).
2. Clone this repository or import the `.mpk` file into Mendix.
3. Open **SLATaskApp** in Studio Pro.
4. Run locally and view in a browser.
5. Test by adding tasks and departments, and navigating the SLA Dashboard.

## Usage

- **Add Departments**: Use **Manage Department** to create departments (e.g., Technical Support).
- **Create Tasks**: Add tasks via the homepage, assigning departments and dates.
- **Monitor SLAs**: Check the **SLA Dashboard** for task statuses, using **Missed** tab for priority tasks.
- **Edit/Delete**: Update tasks on **TaskEdit** page or delete via the dashboard.

## Lessons Learned

- Accelerated development with Mendix templates.
- Mastered domain model extensions and associations.
- Implemented business logic via microflows.
- Improved UX with filtering and navigation.

## Conclusion

I built **SLATaskApp** to address the ISP’s SLA management needs, transforming the **Task & Planning** template into a powerful tool. The app delivers clear SLA tracking, department assignments, and filtered dashboards, surpassing the old Excel process. This project sharpened my Mendix skills, and I’m eager to explore advanced features in future low-code projects.

