# AI Client Intake & Request Routing System

> An AI-powered automation system that analyzes client requests, extracts structured information, and routes each request to the appropriate workflow based on predefined rules.

---

## 🎯 Problem

### The Context

Businesses receive client requests containing information about the required service, budget, and expected timeline. These requests may arrive as free-text messages, making them difficult to process consistently.

### The Problem

Client requests may contain missing, incomplete, or ambiguous information. Processing every request manually takes time, while automatically accepting incomplete requests can lead to incorrect decisions.

### Why It Matters

A structured intake process helps organize client information, reduce repetitive manual work, and ensure that requests requiring clarification are reviewed before proceeding.

---

## 💡 Solution

I designed an AI-powered workflow that receives client requests through Google Forms, analyzes their content using AI, and routes them according to predefined validation rules.

What does the system do?

1. Collects client information and requests through Google Forms.
2. Uses AI to extract the service type, budget, timeline, and request summary.
3. Determines whether the request is complete or requires human review.
4. Stores the results in Google Sheets and sends an appropriate email notification.

---

## 👤 Users

**Primary Users:**

- Businesses receiving client service requests.
- Teams responsible for reviewing and processing client inquiries.

**User Need:**

Users need a consistent way to collect client requests, identify missing information, organize records, and direct each request to the appropriate person or team.

---

## 🧠 How I Designed the Solution

I approached the project as a process-design problem rather than simply connecting automation tools.

I separated the responsibilities into three parts:

- **AI — Understand:** Analyze the client's message and extract relevant information.
- **Automation / Logic — Control:** Apply predefined rules and determine the appropriate route.
- **Human — Judge:** Review requests when required information is missing or ambiguous.

I also designed the workflow to distinguish between a valid request and a request that needs review, making the decision process easier to test and maintain.

The overall approach follows:

**Understand → Design → Build → Test → Refine**

---

## ⚙️ How It Works

```text
Client
  ↓
Google Forms
  ↓
New Form Response Trigger
  ↓
Unstructured Client Request
  ↓
AI by Zapier
  ↓
Structured Output
  ↓
Request Status
  ↓
  ┌──────────────────┐
  │                  │
VALID            NEEDS_REVIEW
  │                  │
  ↓                  ↓
Web Team          Human Review
  │                  │
  └────────┬─────────┘
           ↓
     Google Sheets
           ↓
      Email Notification
```

---

## 🤖 Role of AI

AI by Zapier analyzes the client's request and extracts the information needed by the workflow.

AI is responsible for:

- Identifying the requested service.
- Extracting the stated budget and timeline.
- Summarizing the client's request.
- Identifying missing or ambiguous information.
- Producing structured fields that the automation can use.

### What AI Should NOT Do

- Invent missing information or estimate a budget that the client did not provide.
- Convert vague expressions such as "soon" into a specific deadline.
- Independently decide that an incomplete request is valid.

The workflow uses predefined rules to determine the request status and route it accordingly.

---

## 🔄 Automation

The following tasks are automated:

- Triggering the workflow when a new form response is submitted.
- Passing the client request to the AI analysis step.
- Organizing extracted information into structured fields.
- Determining the request status using predefined conditions.
- Routing valid requests and requests requiring review.
- Saving request records in Google Sheets.
- Sending email notifications based on the selected route.

---

## 🗂️ Data

### Input

The workflow receives the following information through Google Forms:

- `client_name`
- `email`
- `company`
- `request_text`

The request text is unstructured data because clients can describe their needs in natural language.

### Output

The AI analysis and automation produce the following information:

- `service_type`
- `request_summary`
- `timeline`
- `budget`
- `missing_information`
- `request_status`
- `routing`

The workflow also records:

- `requires_human`
- `processed_at`

The resulting records are stored in Google Sheets for tracking and review.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Google Forms | Collecting client information and requests |
| Zapier | Connecting steps and controlling workflow execution |
| AI by Zapier | Analyzing requests and extracting structured information |
| Google Sheets | Storing and tracking processed requests |
| Email | Notifying the responsible team or reviewer |

---

## 🔑 Key Design Decisions

### Decision 1 — Separate AI Analysis from Workflow Logic

**Decision:**

AI extracts information, while Zapier applies predefined rules to route the request.

**Why:**

Separating these responsibilities makes the workflow easier to understand, test, and debug. It also prevents the AI from controlling the entire process without explicit rules.

### Decision 2 — Use Two Request Statuses

**Decision:**

Use `VALID` for complete requests and `NEEDS_REVIEW` for requests with missing or ambiguous required information.

**Why:**

A clear status makes routing more consistent and allows the workflow to handle incomplete requests without silently treating them as valid.

### Decision 3 — Include Human Review

**Decision:**

Route requests that do not satisfy the validation rules to `human_review`.

**Why:**

Some requests require clarification or human judgment. Sending them for review is safer than proceeding with assumptions.

### Decision 4 — Store Processing Results

**Decision:**

Save the original request and its extracted information in Google Sheets.

**Why:**

Keeping a record makes it easier to track requests, compare outputs, investigate errors, and review the automation's decisions.

---

## 🧪 Testing

**Note:** The following are planned test cases and expected results. Actual results and pass/fail statuses should be filled in after running each test and checking the workflow outputs.

### Test 1 — Complete Request

**Input:**

```text
We need a website for our company.
Our budget is $5000.
We need it next month.
```

**Expected Result:**

- `service_type = website`
- `timeline = next month`
- `budget = $5000`
- `missing_information = NONE`
- `request_status = VALID`
- `routing = web_team`
- `requires_human = false`

**Actual Result:**

To be recorded after execution.

**Status:** Pending

---

### Test 2 — Missing Budget

**Input:**

```text
We need a website for our company.
We need it next month.
```

**Expected Result:**

- `service_type = website`
- `timeline = next month`
- `budget = null`
- `missing_information = budget`
- `request_status = NEEDS_REVIEW`
- `routing = human_review`
- `requires_human = true`

**Actual Result:**

To be recorded after execution.

**Status:** Pending

---

### Test 3 — Ambiguous Timeline

**Input:**

```text
We need a website soon.
Our budget is $5000.
```

**Expected Result:**

- `service_type = website`
- `timeline = null`
- `budget = $5000`
- `missing_information = timeline`
- `request_status = NEEDS_REVIEW`
- `routing = human_review`

**Actual Result:**

To be recorded after execution.

**Status:** Pending

---

### Test 4 — Multiple Missing Fields

**Input:**

```text
We need a website for our company.
```

**Expected Result:**

- `service_type = website`
- `timeline = null`
- `budget = null`
- `missing_information = timeline, budget`
- `request_status = NEEDS_REVIEW`
- `routing = human_review`

**Actual Result:**

To be recorded after execution.

**Status:** Pending



## ⚠️ Challenges & Failures

### What Didn't Work as Expected?

Potential challenges identified during the design include:

- Client requests may contain missing or ambiguous information.
- AI may extract information incorrectly if the instructions are unclear.
- Incorrect field mapping may cause data to be stored in the wrong columns.
- Routing conditions may not behave as expected if status values do not match.

### How Did I Address These Challenges?

The workflow design addresses these risks by:

- Defining explicit extraction rules and instructing AI not to invent information.
- Using clear status values for routing decisions.
- Separating AI analysis from automation logic.
- Testing different input scenarios.
- Debugging the workflow layer by layer to identify the first incorrect result.

Actual failures and fixes should be documented here after testing the implementation.

---

## 📚 What I Learned

### Technical Lesson

I learned how to connect form submissions, AI analysis, conditional routing, spreadsheet records, and email notifications into a single automation workflow.

I also learned the importance of structured data and consistent field mapping.

### Problem-Solving Lesson

I learned to approach automation systematically: understand the process, identify its inputs and decisions, design the workflow, test expected outcomes, and debug the first point of failure instead of changing everything at once.

### AI Lesson

I learned that AI is useful for interpreting unstructured text, but it should not replace explicit business rules or human judgment.

A reliable workflow combines AI for understanding, logic for control, and human review for uncertain cases.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- Add more test cases for unusual, incomplete, and ambiguous requests.
- Improve error handling and notifications when an automation step fails.
- Add a dashboard for tracking request statuses and processing history.
- Introduce duplicate-request detection.
- Add a follow-up process for collecting missing client information.
- Evaluate the accuracy of AI extraction against manually verified examples.

---

## 🔗 Project Links

**Live Demo:** Not available yet

**Workflow:** Add the Zapier workflow link if sharing is enabled.

**Repository:** Add the project repository link if available.

---

## 👩‍💻 Author

**Zainab Maher**

**LinkedIn:** Add profile link

**GitHub:** https://github.com/ZainabMaher

---

## Project Summary

This project demonstrates how AI and workflow automation can work together to process client requests in a structured and controlled way.

Rather than allowing AI to make every decision, the system uses AI to extract information, predefined logic to route requests, and human review to handle incomplete or ambiguous cases.

**Understand → Design → Build → Test → Refine**

*Tools implement the design. They do not replace the design.*
