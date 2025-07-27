# Execute Checklist Task

## Purpose

To execute a specified checklist and provide a structured validation report. This task loads a checklist file, guides the user through each item, and generates a completion report.

## Task Execution

### 1. Load Checklist

- If a specific checklist is provided as parameter, load that checklist
- If no checklist specified, list available checklists from `{root}/checklists/` directory
- Validate that the checklist file exists and is readable

### 2. Execute Checklist Items

- Present each checklist section systematically
- For each item, evaluate against current project state
- Mark items as:
  - ✅ COMPLETE - Item is fully satisfied
  - ⚠️ PARTIAL - Item is partially complete or needs attention
  - ❌ MISSING - Item is not addressed or incomplete
  - N/A - Item is not applicable to current project

### 3. Generate Completion Report

- Provide overall completion percentage
- List critical issues that need attention
- Offer specific recommendations for improvement
- Suggest next steps based on findings

### 4. Present Results

- Display structured report to user
- Highlight any blocking issues
- Provide actionable next steps
- Save report if requested

## Usage Examples

```
execute-checklist pm-checklist
execute-checklist story-draft-checklist
execute-checklist architect-checklist
```

## Notes

- This task should not cause loops by reading the same file repeatedly
- Focus on providing actionable feedback rather than exhaustive analysis
- Keep the process efficient and user-friendly