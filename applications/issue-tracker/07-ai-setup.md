# Set up and use an AI coding assistant

Pick one tool for the first build. Chat is enough: give it the design section and the current file, then apply and run the suggested change yourself. An editor assistant can propose file edits in place. In both cases you own the design, checks and release.

| Option | Account setup | Where to use it |
|---|---|---|
| ChatGPT Free | Open [ChatGPT](https://chatgpt.com/), choose Sign up if needed and complete the sign-in flow. Use the free option. | Discuss requirements, ask for a hint, review pasted code or compare test results. [Free plan FAQ](https://help.openai.com/en/articles/9275245-chatgpt-free-tier-faq) |
| Claude Free | Open [Claude](https://claude.ai/), create an account or sign in and complete the prompts. Choose Free. | Ask for a second explanation or a review of a small diff. [Plan details](https://support.claude.com/en/articles/11049762-choose-a-claude-plan) |
| GitHub Copilot Free | Sign into GitHub, check Copilot eligibility and choose Free if offered. Install the official GitHub Copilot extension in VS Code, then sign in with the same GitHub account. | Open Chat and start by asking what the selected file does. Review suggested edits before applying. [Plans](https://docs.github.com/en/copilot/get-started/plans) |

Free usage is limited and account screens can change. If you reach a limit, save your design decision and keep testing manually. This tracker needs no model API key.

For each change give AI the user outcome, exact files, one task, constraints, an example and checks. Example: “Read the schema and the Resolve form. Change only the resolve handler. Use the row ID from the URL. If two rows have the same title, only the selected ID changes. Show me your plan, then the diff, then how I can verify it.”

Review the changed lines, trace input to output, and run a normal and a failure case. If AI claims tests passed, ask for the command and actual output. Give it redacted errors and fictitious data. Keep passwords and private reports out of prompts.
