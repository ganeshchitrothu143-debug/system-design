# One-page review

Before each session, spend 5 minutes recalling the last request flow, 10 minutes on the new problem, 15 minutes implementing, 5 minutes debugging or checking and 5 minutes explaining what you learned. Repeat the request trace from memory two days later.

| Step | What you own | What to give AI | Evidence to check |
|---|---|---|---|
| Design | User, problem and rules | Sketch, three outcomes, one failure | You can explain who does what |
| UI | Screen states and messages | Template file, labels, sample data | Empty, normal and failed states differ |
| Data | What must survive restart | Schema, DB path, sample row | Rows survive setup and restart |
| API | What success and failure mean | Route, fields, status codes | Valid write, invalid input, missing ID |
| Integration | Which action changes which record | User journey, known IDs | Same titles still resolve independently |
| Release | Where and how it runs | Dependencies, startup and storage | Smoke test at the release address |

Use this prompt structure for each task: “We are building [outcome]. Read [files]. Implement only [one change]. Given [input], expect [observable result]. Preserve [rules]. Explain the plan first. After editing, show the changed lines, how to run the check and what you actually verified.”

Before accepting a change, read the diff, trace one normal request, predict one failure and run both checks. Save the smallest passing change before starting the next one.

**Explain it back.** Why can two issues share a title but need different IDs? What should the browser do when the database write fails? How would you prove that the deployed app uses the intended database?
