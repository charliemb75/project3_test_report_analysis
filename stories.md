# User stories

| ID    | User Story                                                                                                                                       | Priority | Acceptance Criteria                                                                                                          |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | ---------------------------------------------------------------------------------------------------------------------------- |
| US-01 | As a testing engineer, I want incoming report emails to be automatically detected and parsed so that I do not manually process test reports.     | High     | Workflow detects emails with `.md` attachments and issue photos; files are downloaded to the workflow context.               |
| US-02 | As a system user, I want issues extracted from markdown test reports so that defects can be processed automatically.                             | High     | Workflow extracts structured issue data (component, defect type, severity, notes) from the report using ChatGPT.             |
| US-03 | As a development engineer, I want issue photos analyzed so that I receive technical descriptions, causes, consequences, and preventive measures. | High     | Each issue photo produces a structured AI analysis containing description, causes, consequences, and mitigation suggestions. |
| US-03 | As a development engineer, I want existing issue reports updated with new findings so that historical defect tracking is maintained.           | Medium   | Existing reports are updated with appended findings and linked evidence. 
| US-04 | As a database manager, I want the workflow to identify whether an issue already exists so that duplicate records are avoided, and to create new folders and reports for any new issues    | High     | Existing issue records are searched and matched semantically against newly extracted issues.                                 |
| US-05 | As a project stakeholder, I want semantic comparison between issues so that differently worded but identical defects are recognized correctly.   | High     | Workflow correctly matches semantically equivalent defects while avoiding false positives.                                   |
| US-05 | As a project stakeholder, I want Slack notifications when new analyses are completed so that I stay informed about relevant findings.                    | Medium   | Slack notifications contain issue summary, status (new/existing), and report links.                                          |

# Sprint plan
| Sprint   | Task ID | Related Story | Task Description                                                 | Estimate (Story Points) | Dependencies | Definition of Done                                                                      |
| -------- | ------- | ------------- | ---------------------------------------------------------------- | ----------------------- | ------------ | --------------------------------------------------------------------------------------- |
| Sprint 1 | T-01    | US-01         | Configure n8n email trigger and attachment retrieval             | 3                       | None         | Workflow successfully receives emails and downloads markdown files + images.            |
| Sprint 1 | T-02    | US-01         | Validate attachment format and naming conventions                | 2                       | T-01         | Invalid files are rejected with error logging.                                          |
| Sprint 1 | T-03    | US-02         | Build ChatGPT prompt for extracting issues from markdown reports | 5                       | T-01         | Structured issue JSON is returned consistently from sample reports.                     |
| Sprint 1 | T-04    | US-02         | Parse and normalize extracted issue data                         | 3                       | T-03         | Extracted issue data is stored in a normalized format.                                  |
| Sprint 2 | T-05    | US-03         | Connect image analysis step to ChatGPT Vision                    | 5                       | T-04         | Workflow processes issue photos and returns structured technical analysis.              |
| Sprint 2 | T-06    | US-03         | Generate development-focused recommendations for each issue      | 3                       | T-05         | Causes, consequences, and preventive measures are included in results.                  |
| Sprint 2 | T-07    | US-04         | Implement centralized workflow logging                           | 3                       | T-01         | Logs capture workflow status, failures, and AI outputs.                                 |
| Sprint 3 | T-08    | US-04         | Connect workflow to issue database in Google Drive               | 5                       | T-04         | Workflow can retrieve and search stored issue records.                                  |
| Sprint 3 | T-09    | US-05         | Implement semantic issue matching logic using ChatGPT            | 8                       | T-08         | Matching correctly identifies equivalent issues from test examples.                     |
| Sprint 3 | T-10    | US-05         | Add validation rules to prevent false-positive matches           | 5                       | T-09         | Incorrect matches are rejected in test scenarios.                                       |
| Sprint 4 | T-11    | US-03         | Create automated folder/report generation for new issues         | 5                       | T-09         | New issues create structured folders and reports automatically.                         |
| Sprint 4 | T-12    | US-03         | Implement report update process for existing issues              | 5                       | T-09         | Existing reports append new findings correctly.                                         |
| Sprint 4 | T-13    | US-08         | Integrate Slack notification workflow                            | 3                       | T-11, T-12   | Stakeholders receive notifications with issue summaries and links.                      |
| Sprint 4 | T-14    | US-04         | Add retry/error handling for failed workflow steps               | 3                       | T-07         | Workflow retries transient failures and logs unrecoverable errors.                      |
| Sprint 5 | T-15    | All           | End-to-end integration testing                                   | 8                       | T-01 to T-14 | Full workflow tested successfully using sample reports and images.                      |
| Sprint 5 | T-16    | All           | Documentation and deployment preparation                         | 3                       | T-15         | Repository includes setup instructions, architecture notes, and finalized `stories.md`. |

# Dependencies
| Task | Depends On        |
| ---- | ----------------- |
| T-02 | T-01              |
| T-03 | T-01              |
| T-04 | T-03              |
| T-05 | T-04              |
| T-06 | T-05              |
| T-08 | T-04              |
| T-09 | T-08              |
| T-10 | T-09              |
| T-11 | T-09              |
| T-12 | T-09              |
| T-13 | T-11, T-12        |
| T-14 | T-07              |
| T-15 | T-01 through T-14 |
| T-16 | T-15              |
