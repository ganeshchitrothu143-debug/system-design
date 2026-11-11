# Store and read real records

**Prerequisites.** A table holds rows. Each row describes one issue. An ID gives a row a unique identity even if two reports have the same title. A database schema defines the allowed columns and rules. SQL is the language for asking the database to read or change rows. SQLite stores this app’s table in one disk file.

Ask AI to turn the design in the system design chapter into schema.sql.



Choose a database path relative to app.py so launching from another working directory cannot silently create a different database. Ask AI to make a separate `init_db.py` that runs schema.sql using Python’s sqlite3. Run `ENV-PY init_db.py` before starting Flask. For this project, initialization should preserve existing rows. A later change to an existing table would need a separate migration, an explicit script for changing the schema.

Update the GET route to read `SELECT id, title, status FROM issues ORDER BY id DESC`. A template loop repeats the row markup for every issue. Use Jinja, Flask’s template language, to show the title with `{{ issue.title }}`. Keep its default escaping so a title containing markup displays as text.

**Ask AI.** “Implement just database initialization and reading the issue list. Read schema.sql and app.py. Use sqlite3 with a new connection for each operation and close it afterward. Use sqlite3.Row for named fields. Pass the rows to the existing template as issues. Remove the hardcoded example. Show ‘No issues yet’ only when the query succeeds and returns zero rows. Give me the commands to initialize and run, and a disposable sample insert for my local database.”

**Review.** Run initialization twice. Insert an example between runs and confirm it still appears. Check that the template uses the query results. If the screen shows zero issues unexpectedly, print the resolved database path and compare it with the file you populated.

