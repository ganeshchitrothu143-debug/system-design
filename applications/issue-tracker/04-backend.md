# Save an issue

**Prerequisites.** A form sends named values to the server. POST means the browser is submitting work that can change data. Validation checks whether input follows a rule. A commit makes a database write durable. A SQL placeholder such as ? passes the value separately from the instruction. A redirect tells the browser to load a different address.

1. Give the input a label, the name title and a Report submit button. Set the form to POST to /issues.
2. In the POST handler, read title and trim surrounding whitespace. Accept 1–100 characters. On invalid input, return the page with an error, the original text and HTTP 400, the code for an invalid request.
3. Insert using `INSERT INTO issues (title) VALUES (?)` with `(title,)` as the separate parameter tuple. Commit before reporting success. The schema supplies the open status.
4. Return a 303 redirect to /. The browser follows with GET, so refreshing the resulting page reloads the list. If saving fails, log the technical error on the server and return a readable failure message with the draft preserved. If reading also fails, show the list as unavailable.

**Ask AI.** “Implement only report creation using the existing schema and template. Follow the four steps above. Show me the insert, commit and redirect in the diff. Explain what happens if validation or writing fails. Provide one positive and two negative checks. Treat any code you did not run as unverified.”

**Review.** A diff shows added and removed lines. Read the handler in order and point out the line that prevents an invalid title from reaching SQL. Submit a normal title, a title made of spaces and a title with an apostrophe. Confirm a successful refresh does not create a second row. A 303 handles refresh after success. It does not guarantee that two independent submissions create only one record.

