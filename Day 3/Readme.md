# Salesforce Interview Readiness Bootcamp - Day 5

# Salesforce Automation with Flows, Validation Rules, and Triggers

## 📌 Project Overview

This project focuses on automating a Placement Management System using Salesforce's declarative and programmatic automation tools. The objective was to understand when to use Validation Rules, Record-Triggered Flows, and Apex Triggers while building real-world business automation.

---

# 🚀 Learning Objectives

During this assignment, I learned:

- The purpose of Validation Rules in Salesforce.
- How Record-Triggered Flows automate business processes.
- The order of execution between Validation Rules, Flows, and Triggers.
- The differences between Workflow Rules, Process Builder, and Flow.
- When to choose Flow instead of Apex Trigger.
- How Before-Save and After-Save Flows work.
- How Salesforce automation improves efficiency and data quality.

---

# 🛠️ Business Scenario

The Placement Cell required the following automation:

- Automatically populate the Application Date when a student submits an application.
- Send an email notification to the Placement Officer.
- Prevent duplicate job applications.
- Reject applications when the student's CGPA is below the required minimum.
- Automatically create an Offer Letter record when an application status changes to **Selected**.

---

# 📂 Features Implemented

## ✅ Record-Triggered Flow

Created a Record-Triggered Flow that:

- Automatically sets the Application Date.
- Sends an email notification to the Placement Officer.
- Executes automatically whenever a new Application record is created.

---

## ✅ Validation Rules

Created Validation Rules to ensure data quality by:

- Preventing applications when the student's CGPA is below the Job's minimum CGPA.
- Preventing Application Dates after the Job Closing Date.
- Ensuring mandatory fields cannot be left blank.
- Preventing duplicate applications.

---

## ✅ Automation Design

Learned how to decide the appropriate automation tool for different requirements.

| Requirement | Best Solution |
|-------------|---------------|
| Reject duplicate applications | Validation Rule |
| Auto-fill Application Date | Record-Triggered Flow |
| Send Email Notification | Record-Triggered Flow |
| Reject low CGPA | Validation Rule |
| Create Offer Letter record | Record-Triggered Flow |

---

# 📖 Key Concepts Learned

### Validation Rules

Validation Rules are used to validate user input before a record is saved. They help maintain data quality by preventing invalid data from being stored.

---

### Record-Triggered Flow

A Record-Triggered Flow automatically executes when a record is created or updated. It can update records, send emails, create related records, and automate business processes without writing code.

---

### Before-Save Flow

Used to update fields before the record is saved.

Benefits:
- Faster execution
- No additional database update
- Best for field updates

---

### After-Save Flow

Used after the record has been saved.

Can be used to:

- Create related records
- Send emails
- Call Apex
- Update related records

---

### Validation Rules vs Flows vs Triggers

| Validation Rule | Flow | Apex Trigger |
|-----------------|------|--------------|
| Validates data | Automates business processes | Handles complex business logic |
| No code | Low-code | Full-code solution |
| Prevents invalid records | Updates records and sends emails | Supports advanced logic and integrations |

---

# 💻 Technologies Used

- Salesforce CRM
- Flow Builder
- Record-Triggered Flow
- Validation Rules
- Apex Triggers
- Lightning Experience

---

# 📸 Screenshots

Include screenshots of:

- Flow Canvas
- Start Element
- Assignment Element
- Email Action
- Successful Flow Execution
- Validation Rules
- Placement Management System

---

# 🎯 What I Learned

After completing this project, I can:

- Design Salesforce automation solutions.
- Build Record-Triggered Flows.
- Create Validation Rules for business requirements.
- Decide when to use Flow, Validation Rule, or Apex Trigger.
- Understand Salesforce Order of Execution.
- Improve data quality using declarative automation.
- Automate business processes without writing Apex code whenever possible.

---

# 🚀 Future Improvements

In future enhancements, I plan to:

- Integrate Apex with Flows for advanced automation.
- Add Approval Processes.
- Build reusable Subflows.
- Connect Flows with Lightning Web Components.
- Implement automated testing for Flows and Apex.

---

# 📚 Conclusion

This project strengthened my understanding of Salesforce automation by combining Record-Triggered Flows, Validation Rules, and Apex concepts in a real-world Placement Management System. It provided hands-on experience in designing scalable, efficient, and maintainable business processes while following Salesforce best practices.
