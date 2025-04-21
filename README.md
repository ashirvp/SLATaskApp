# SLATaskApp

SLATaskApp Project Documentation
Project Overview
I developed SLATaskApp, a Mendix-based application to streamline Service Level Agreement (SLA) management for an Internet Service Provider (ISP) company. Built using Mendix Studio Pro (version 10.0.0) and the Task & Planning app template, the app tracks SLA compliance and assigns tasks to responsible departments. I extended the template’s functionality to include a custom SLA Dashboard, replacing an outdated Excel-based process with a modern, user-friendly solution.

Duration: Approximately 4 hours
Platform: Mendix Studio Pro 10.0.0
Template: Task & Planning

Project Objectives
My goal was to create an app that:

Tracks whether SLAs are met for customer contracts, providing clear visibility for contract negotiations.
Assigns tasks to departments and monitors their SLA status.
Offers an intuitive SLA Dashboard to display task details and SLA outcomes.
Enables filtering of tasks to focus on missed SLAs for quick action.

Use Case
As an ISP, I needed a robust tool to monitor SLAs that specify service restoration times for customers. Previously managed via Excel, this process was inefficient. My app displays whether SLAs are achieved, identifies the responsible department for each task, and provides a centralized dashboard for task management. I chose the Task & Planning template for its task management foundation and customized it to meet SLA-specific requirements.
Development Process
1. Project Setup
I kicked off the project by setting up SLATaskApp in the Mendix Portal, selecting the Task & Planning template as the foundation. I installed Mendix Studio Pro 10.0.0 and dove into the development environment to explore its capabilities.

Steps:
Created SLATaskApp in the Mendix Portal and chose the Task & Planning template.
Disabled app security (set to Off) to simplify development and testing.
Familiarized myself with Studio Pro’s interface:
App Explorer: Organized pages, domain model, microflows, and settings.
Properties Pane: Adjusted element properties like layout and titles.
Toolbox: Added widgets and tools to enhance pages.
Menu Bar: Used for saving, running locally, and previewing the app.
Dockable Panes: Monitored errors, changes, and console logs.


Ran the app locally and tested the template by adding a task (“Develop Performance Presentation”) to confirm its functionality.



2. Creating the SLA Dashboard
I designed a new SLA Dashboard page to serve as the app’s central hub for viewing task and SLA information, accessible from the navigation menu.

Steps:
Created a new page named SLA_Dashboard using the List template and Tasks_TopBar layout for a consistent look.
Added a navigation menu item for the SLA Dashboard, placing it between Team and My Profile for easy access.
Encountered an initial error due to an unconfigured entity, which I planned to resolve in the domain model phase.



3. Extending the Domain Model
To support SLA tracking and department assignments, I extended the app’s domain model with new attributes, entities, and associations.

Steps:
Modified the Task entity:
Added SLADashboardStatus (Enumeration: SLA Achieved, SLA Missed) to track SLA outcomes.
Added CompletionDate (Date and Time) to record task completion.


Created a Department entity with a Name attribute (String) to store department details.
Established a one-to-many association between Department (1) and Task (*), allowing one department to handle multiple tasks.
Updated the TaskEdit page to include:
A CompletionDate date picker, duplicated from the existing DueDate field.
A Reference Selector widget to assign tasks to departments.





4. Connecting Data to Pages
I connected the SLA Dashboard to the domain model and built additional pages to manage departments, ensuring seamless data display and interaction.

Steps:
Linked the SLA Dashboard’s list view to the Task entity, configuring it to display Title, CompletionDate, SLADashboardStatus, and Department Name.
Added a delete button (trash icon) to allow users to remove unnecessary tasks.
Created a Department_Overview page (List template) to list all departments.
Built a Department_NewEdit page (Form vertical, popup layout) for adding and editing departments.
Configured an Add button on the Department_Overview page to create new Department objects, resolving an error by passing the correct object to the popup page.
Tested the app by:
Adding departments (e.g., Implementation, Technical Support).
Creating tasks (e.g., “Check network performance” assigned to Technical Support).
Verifying the SLA Dashboard displayed tasks correctly and supported deletions.





5. Adding Custom Logic
I customized the SelectDoneStatus microflow to automate SLA status updates based on task completion dates, adding logic to validate inputs and set outcomes.

Steps:
Analyzed the SelectDoneStatus microflow, triggered by the Done button on the TaskEdit page, which originally set the task status to Done.
Extended the microflow:
Added a Decision activity to check if CompletionDate and DueDate are filled, using the expression $Task/CompletionDate != empty and $Task/DueDate != empty.
Added a second Decision activity to compare CompletionDate ≤ DueDate.
Configured the microflow to set SLADashboardStatus to SLA Achieved (true) or SLA Missed (false).
Included a Show Message activity for the unhappy flow, alerting users to fill in both dates if missing.


Leveraged MxAssist Logic Bot to streamline microflow development with AI-driven recommendations.
Tested the microflow by updating tasks:
Set a task with CompletionDate before DueDate to confirm SLA Achieved.
Set another with CompletionDate after DueDate to verify SLA Missed.
Checked the SLA Dashboard to ensure accurate status updates.





6. Filtering Data
To meet user requirements for focusing on missed SLAs, I enhanced the SLA Dashboard with filtered views and sorted data.

Steps:
Added a Tab Container to the SLA Dashboard, creating Missed and All tabs.
Moved the existing list view to the All tab and duplicated it for the Missed tab.
Configured the Missed tab’s list view with a data source constraint: SLADashboardStatus = SLA Missed.
Sorted the Missed tab by CompletionDate (Descending) to show the most recent missed SLAs first.
Tested the app by:
Adding tasks with mixed SLA outcomes (some met, some missed).
Confirming the Missed tab displayed only SLA-missed tasks, sorted correctly.
Verifying the All tab showed all tasks without filtering.





Final Outcome
I successfully delivered SLATaskApp, a fully functional SLA management tool that:

Tracks SLA compliance with a custom SLA Dashboard, displaying task details and statuses.
Assigns tasks to departments and updates SLA outcomes automatically.
Filters tasks to highlight missed SLAs in a dedicated tab, sorted by recent completion dates.
Provides an intuitive interface for managing tasks and departments, improving efficiency over the previous Excel process.

Technical Details

Platform: Mendix Studio Pro 10.0.0
Template: Task & Planning
Security: Set to Off for development simplicity
Key Components:
Pages: SLA_Dashboard, Department_Overview, Department_NewEdit, TaskEdit
Domain Model: Extended Task entity, new Department entity, one-to-many association
Microflow: Extended SelectDoneStatus with decision and message activities
Widgets: List View, Tab Container, Reference Selector, Buttons, Date Picker


Tools Used:
Mendix Portal for app creation and management.
Studio Pro for development and local testing.
MxAssist Logic Bot for microflow optimization.



Challenges and Solutions

Challenge: The SLA Dashboard initially showed an error due to an unconfigured list view entity.
Solution: Connected the list view to the Task entity and verified data display.


Challenge: Ensuring accurate SLA status updates required precise microflow logic.
Solution: Added decision activities to validate dates and set statuses, with thorough testing to confirm outcomes.


Challenge: Users needed a way to focus on missed SLAs without losing access to all tasks.
Solution: Implemented a Tab Container with a constrained Missed tab and an unfiltered All tab.


Challenge: The Department_NewEdit page had an error due to missing object context.
Solution: Configured the Add button to create a new Department object before opening the popup.



Future Improvements
To enhance SLATaskApp, I plan to:

Enable Production security with user authentication and role-based access.
Add visualizations (e.g., charts or graphs) to the SLA Dashboard for SLA trend analysis.
Implement notifications to alert users about approaching SLA deadlines.
Explore Mendix integrations for connecting with external systems, such as customer management tools.
Optimize performance for larger datasets by refining queries and indexing.

Lessons Learned
This project deepened my understanding of Mendix’s low-code platform, particularly:

Leveraging templates to accelerate development while customizing for specific needs.
Building and extending domain models to support complex data relationships.
Using microflows to implement business logic with decision-based workflows.
Enhancing user experience through data filtering and intuitive navigation.

Conclusion
I built SLATaskApp from the ground up, transforming the Task & Planning template into a tailored SLA management solution. The app meets the ISP’s requirements by providing clear SLA tracking, department assignments, and filtered views for missed SLAs. The development process honed my skills in Mendix Studio Pro, from page design to microflow logic, and I’m excited to apply these skills to future projects. SLATaskApp is a solid foundation for further enhancements and demonstrates the power of low-code development for solving real-world business challenges.
