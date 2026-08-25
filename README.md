# AI Email Classification & Routing System

An AI-powered email classification and routing system that automatically analyzes incoming emails, determines the appropriate department, and routes messages based on classification confidence.
High-confidence emails can be routed automatically, while uncertain classifications are sent for human review before forwarding.

Tech Stack: `n8n` · `Gmail` · `Google Gemini` · `Airtable` · `JavaScript` · `AI Prompt Engineering`

---

## 📌 Problem

Organizations often receive emails intended for different departments, making manual sorting and forwarding repetitive, time-consuming, and prone to errors.
Without an automated system, staff may need to:

- Read incoming emails individually
- Determine which department should handle each message
- Identify urgent or high-priority requests
- Detect spam
- Forward emails manually
- Track what has already been processed

The goal of this project was to automate email classification and routing while maintaining **human oversight for uncertain classifications**.

---

## 🎯 Objectives

The system was designed to:

- Classify incoming emails using AI
- Detect the appropriate department
- Assign confidence scores
- Determine email priority
- Detect spam
- Automatically route classified emails
- Support human approval for uncertain classifications
- Maintain a searchable audit trail
- Prevent duplicate forwarding

---

## 💡 Solution

Incoming emails trigger an n8n workflow through Gmail.
The email content is prepared and sent to **Google Gemini**, which returns a structured JSON response containing:
- Department
- Reason
- Confidence score
- Priority
- Spam detection
Based on the classification result, the workflow either routes the email automatically or stores it in Airtable for administrator review.
Emails requiring review are marked as **Pending Review**. An administrator can adjust the department if necessary and mark the record as **Done**.
A separate scheduled workflow periodically searches Airtable for approved records where:

```
Status = Done
Forwarded = No
```

The workflow then retrieves the original email using its Gmail Message ID, forwards it to the appropriate department, and updates the Airtable record to prevent duplicate forwarding.

⸻

🏗️ Workflow Architecture

Email Intake & AI Classification
```
Incoming Email
      ↓
Gmail Trigger
      ↓
Prepare Email Data
      ↓
Google Gemini
      ↓
Structured JSON Response
      ↓
Parse AI Response
      ↓
Store Classification in Airtable

Classification Data

Google Gemini
      ↓
┌─────────────────────┐
│ Department          │
│ Reason              │
│ Confidence Score    │
│ Priority            │
│ Spam Detection      │
└─────────────────────┘
```
Routing & Human Review
```
AI Classification
      ↓
Classification Decision
      ↓
┌───────────────────┬────────────────────┐
│                   │                    │
High Confidence    Low Confidence       Spam
│                   │                    │
↓                   ↓                    ↓
Automatic Route    Pending Review       Spam Handling
                    ↓
              Administrator
                    ↓
             Review / Adjust
                    ↓
              Status = Done

Automated Forwarding

Scheduled Workflow
      ↓
Search Airtable
      ↓
Status = Done
Forwarded = No
      ↓
Retrieve Original Email
using Gmail Message ID
      ↓
Determine Department
      ↓
Forward Email
      ↓
Update Airtable
Forwarded = Yes
```
⸻

🛠️ Technologies Used

Technology	Purpose
n8n	Workflow automation and orchestration
Gmail	Email intake and original email forwarding
Google Gemini	AI email classification
Airtable	Classification records, human review, and audit trail
JavaScript	Data processing and workflow logic
AI Prompt Engineering	Structured classification and decision-making

⸻

🧠 Core Features

**AI-Powered Classification**

Uses Google Gemini to analyze incoming email content and determine the appropriate department.

**Department Detection**

Automatically identifies which department should handle each email.

**Confidence Scoring**

The AI provides a confidence score that can be used to determine whether an email should be routed automatically or reviewed by an administrator.

**Priority Detection**

Emails are assigned a priority level to help identify messages requiring greater attention.

**Spam Detection**

The AI evaluates incoming messages for spam classification.

**Human-in-the-Loop Review**

Low-confidence classifications are stored as Pending Review, allowing an administrator to verify or modify the classification before forwarding.

**Automated Routing**

Approved emails are automatically forwarded to the appropriate department.

**Airtable Audit Trail**

Classification results, review status, forwarding status, and other email metadata are stored in Airtable.

**Duplicate Forwarding Prevention**

The system tracks whether an email has already been forwarded, preventing duplicate processing.

**Original Email Forwarding**

The Gmail Message ID is stored so the system can retrieve and forward the original email rather than creating a completely new message.

⸻

🧩 Challenges Encountered

- Parsing structured AI responses reliably
- Managing confidence-based routing
- Designing a human approval workflow
- Preventing duplicate email forwarding
- Retrieving and forwarding the original Gmail message
- Handling limitations with Airtable triggers
- Replacing the Airtable trigger with a scheduled polling workflow
- Maintaining reliable state between classification, review, and forwarding

⸻

🔧 Improvements Made

- Added AI confidence scores
- Added spam detection
- Added priority classification
- Added a pending-review workflow
- Implemented duplicate forwarding prevention
- Stored Gmail Message IDs for forwarding original emails
- Added scheduled polling for approved records
- Added workflow documentation and demonstration materials

⸻

📊 Results

The completed system can:

- Monitor incoming emails automatically
- Classify emails using AI
- Determine the appropriate department
- Assign confidence and priority
- Detect spam
- Store classification results in Airtable
- Send uncertain classifications for human review
- Automatically forward approved emails
- Retrieve and forward original Gmail messages
- Prevent duplicate forwarding
- Maintain an audit trail of processed emails

The result is an automated email-routing system that significantly reduces manual sorting while maintaining human oversight where needed.

⸻

📸 Screenshots

n8n Email Classification Workflow

AI Classification Output

Airtable Email Log

Human Review / Approval

Automated Email Forwarding

⸻

🎥 Demo

A full walkthrough demonstrating email intake, AI classification, confidence-based review, Airtable logging, and automated forwarding is available below.

Demo: [Add your demo link here]

⸻

🔮 Future Improvements

- Slack or Microsoft Teams notifications
- Sentiment analysis
- AI-generated draft replies
- Attachment classification
- Multi-language support
- Advanced reporting dashboard
- Support for additional email providers

⸻

📚 Key Learnings

- AI prompt engineering
- Structured JSON parsing
- Human-in-the-loop workflow design
- Confidence-based automation
- Scheduled automation
- Gmail integrations
- Airtable database management
- Reliable automation patterns
- Duplicate-processing prevention
- Workflow optimization

⸻

👤 Author

Hammed Timmy

AI & Automation Builder

[LinkedIn⁠](https://www.linkedin.com/in/okanlawon-a-o/)
