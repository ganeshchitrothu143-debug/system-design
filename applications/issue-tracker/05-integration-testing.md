# Resolve and test the whole journey

**Prerequisites.** A route parameter is a value in the address. In /issues/3/resolve, 3 identifies the row. An end-to-end test uses the same path as the user, starting at the browser and reaching the actual database. An HTTP 404 means the requested record was not found.

Add a Resolve form next to each open issue. Submit POST to /issues/<id>/resolve. In Flask use an integer route parameter. Run `UPDATE issues SET status = 'resolved' WHERE id = ?` with the ID passed separately. If the update matches zero rows, return 404. Commit and redirect on success. Repeating a successful resolve leaves the same final state. Use a separate database file for automated tests so test writes cannot change demo data.

**Ask AI.** “Implement only resolving an issue. Use the existing database path and template. Explain how the button identifies the row. Add a test using a temporary database that creates two issues, resolves only the first, and verifies both statuses. Check missing ID and repeated resolution. Report the command, actual output and what remains untested.”

**Review and debug.** Manually create two issues with the same title, resolve the second, refresh, then stop and restart the server. Exactly the selected row should remain resolved. If the wrong one changed, inspect the browser’s Network tab for the POST address, then the backend’s parsed ID, then query the rows. Before asking AI for a fix, supply the steps to reproduce, expected result, actual result and relevant error or request data. Ask for one likely cause and the smallest check that can confirm it.

