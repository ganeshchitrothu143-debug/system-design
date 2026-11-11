# Turn a complaint into a design

**Prerequisites.** A browser is the program that displays a page. A frontend is the screen and the code that reacts to clicks. A backend is a running program that receives requests and enforces rules. A database keeps records after programs stop. A request is a message asking for work. A response reports the result. Think of the frontend as the report form, the backend as the clerk and the database as the register.

**Think first.** If you wrote the report only on the form, what would the next person see? If the clerk could not write to the register, when should they tell you the report was saved?

Write three outcomes: “I can list issues,” “I can report one,” and “I can resolve one.” Convert each into a check. For example, “After resolving issue 3 and refreshing, issue 3 still says Resolved.” The initial scope is one private workspace with sample data, one page and no user accounts.

Sketch a page with a heading, a labeled title input, a Report button, a message area and a list. Each list row shows the title, status and a Resolve button when open. Draw four versions: empty, populated, saving and save failed. During a failure, keep the input text and show a message. A failed list request needs its own message because “no issues” is a successful answer.

**Ask AI.** “Act as a design reviewer. Here is my sketch and my three outcomes. Walk through a normal save and a failed save. Point to one missing rule and give me a hint before suggesting a fix. Do not write code.”

**Review.** Can you trace the action from input to saved record and back to the screen? Decide what evidence the screen needs before saying “Saved.” A server success response after the database write is the evidence we’ll use.

