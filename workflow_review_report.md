# Workflow Review Report

Reviewer: Adin Suhastra

Sample type: Self-made n8n-style workflow QA sample

Scenario: Lead capture -> validation -> scoring -> routing -> follow-up draft -> human approval -> reporting

## Workflow Summary

The reviewed workflow is a fictional lead capture automation. It receives a sample lead, checks whether the lead data is usable, assigns a simple priority score, routes the lead into Hot / Warm / Cold categories, prepares a follow-up draft, pauses for human approval, and produces a reporting output.

The review compares two files:

- `sample_workflow_before.json`
- `sample_workflow_after.json`

The before version intentionally contains safe demo issues. The after version shows how the workflow could be made clearer, safer, and easier to maintain.

## Issues Found

### 1. Unclear Node Names

Risk level: Low

The before workflow uses names like `Step 1`, `Check`, and `Do Thing`, which make it harder for another person to understand the workflow quickly.

Recommended fix:
Use descriptive names such as `Manual Trigger - Demo Lead Intake`, `Validate Lead Fields`, and `Score Lead Priority`.

### 2. Missing Input Validation

Risk level: Medium

The before workflow assumes the lead includes name, email, company, source, and message fields. It does not check whether required values are missing or malformed.

Recommended fix:
Add a validation step that checks required fields and routes invalid leads to a review queue instead of continuing.

### 3. Weak Lead Scoring Explanation

Risk level: Low to Medium

The before workflow assigns a category without documenting the scoring rules.

Recommended fix:
Document simple scoring rules such as:

- business email present
- clear service interest
- company provided
- high-intent keywords in message

### 4. No Human Approval Checkpoint

Risk level: High

The before workflow prepares a follow-up draft but does not include a clear approval step before any message could be sent.

Recommended fix:
Add a `Human Approval Required` step and keep the output as a draft only.

### 5. Limited Error Handling

Risk level: Medium

The before workflow has no clear error path for missing fields, duplicate leads, or unsupported lead categories.

Recommended fix:
Add error notes and review routing for invalid or uncertain leads.

### 6. Reporting Output Is Not Structured

Risk level: Low

The before workflow output is hard to audit because it does not provide a structured summary.

Recommended fix:
Use a predictable output format with lead ID, status, category, score, follow-up draft, approval status, and review notes.

## Before / After Comparison

| Area | Before | After |
|---|---|---|
| Node names | Generic and unclear | Specific and readable |
| Input validation | Missing | Required fields checked |
| Scoring | Undocumented | Simple scoring notes included |
| Routing | Basic category only | Hot / Warm / Cold with review path |
| Human approval | Missing | Approval checkpoint included |
| Error handling | Weak | Invalid leads routed to review |
| Reporting | Loose summary | Structured reporting output |
| Safety | Follow-up could be misread as send-ready | Draft-only, approval required |

## Final Review Status

Status: Improved for demo readiness

The after version is clearer, safer, and more maintainable as a portfolio sample. It is not production-ready and should not be connected to real lead sources, email tools, CRMs, or messaging systems without additional review.

## Production Readiness Notes

Before any real deployment, this workflow would need:

- real n8n implementation testing
- credential storage review
- opt-in and outreach compliance review
- duplicate detection
- logging and monitoring
- retry handling
- rate limiting
- human approval before outreach
- sample test cases using non-sensitive data
