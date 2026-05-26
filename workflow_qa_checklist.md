# Workflow QA Checklist

Use this checklist to review a small n8n-style automation workflow before it is treated as ready.

## Trigger Clarity

- Is the trigger clearly named?
- Is the trigger source documented?
- Is it clear whether the workflow starts manually, by webhook, by schedule, or by app event?
- Is there a safe testing mode?

## Input Validation

- Are required fields defined?
- Are missing fields handled?
- Are malformed emails, blank names, or empty messages handled?
- Are duplicate records considered?
- Is invalid input routed to review instead of silently continuing?

## Error Handling

- Is there a clear error path?
- Are failed nodes easy to identify?
- Are retry rules documented?
- Are unknown categories routed to review?
- Is there a fallback output for incomplete records?

## Credential Safety

- Are credentials excluded from exported workflow files?
- Are API keys, tokens, passwords, and secrets absent?
- Are placeholder credentials clearly marked as placeholders?
- Is there no personal data in sample files?

## Naming Clarity

- Do node names explain what each step does?
- Are generic names like `Step 1`, `Code`, `Check`, or `Do Thing` replaced with specific names?
- Can another reviewer understand the workflow from the node names alone?

## Node Documentation

- Does each important node have a short purpose note?
- Are business rules documented?
- Are scoring or routing assumptions explained?
- Are manual review points clearly labeled?

## Duplicate Steps

- Are there unnecessary repeated validation steps?
- Are there multiple nodes doing the same transformation?
- Can repeated logic be simplified or documented?

## Human Approval Checkpoint

- Is there a clear pause before any external message is sent?
- Is follow-up text treated as a draft, not an automatic send?
- Is the reviewer responsible for approval identified?
- Is the approval status included in the final output?

## Output Format

- Is the output structured and predictable?
- Does it include lead ID, validation status, score, category, draft, and review notes?
- Can the output be exported, audited, or copied into another tool?

## Test Data

- Is all test data fictional?
- Are edge cases included?
- Are missing-field examples included?
- Are invalid-input examples included?
- Are expected outputs documented?

## Privacy and Safety Concerns

- Does the workflow avoid scraping?
- Does it avoid sensitive personal data?
- Does it avoid automated outreach without human approval?
- Does it comply with platform and client rules?
- Does it keep human responsibility visible?

## Final Decision

Mark the workflow as one of:

- Ready for demo only
- Needs review before real implementation
- Blocked due safety/privacy issue
- Ready for controlled internal test
- Ready for production only after senior review
