# General description

This n8n workflow automates the processing of test reports for car components, updating a database in a Google Drive folder with the new findings.

1.	Email arrives with new report in md file (template: input_template.md) and photos of each new issue.
2.	Extract issues from the test report (ChatGPT).
3.	For each issue, analyze the corresponding photo and generate a short description, research for causes, consequences and possible measures that should be taken to prevent it -from a development perspective- (ChatGPT).
4.	Check database for existing issues
5.	Compare which issues in the report already exist in the database (ChatGPT). Examples of the semantic matching:
    * Correct matching: “rust in the wheel arches” and “wheel arches present corrosion” (same part and issue, different formulation).
    * Incorrect matching: “cracked headlight” and “cracked windshield”, or “dented exhaust pipe” and “corrosion in exhaust pipe” (part or issue do not match).
6.	Update database:
    * For new issues: generate a new folder in the database and a new report.
    * For existing issues: update the old report with the new findings
7.	Relevant stakeholders notified about the new analysis (Slack).

# Requirements
* OpenAI API key.
* Google account with configured Cloud and OAuth2 Client.
* Slack account with configured API and an App.

# Assumptions
* Access through dedicated address that receives only this inputs (example: test_reports@company.com).
* The issue descriptions in the report are detailed enough for a meaningful classification (type of damage and affected part should be qualitatively identifiable).

# Possible next steps
* Filter out non-related emails. Would enable using the tool from a personal address.
* Filter out vague or unrelated descriptions like “damage to part X” or "test interruption because of rig malfunction" (ask for further detail or manual classification).