# Deploy and verify

**Prerequisites.** Deployment means installing and running a release in its intended environment. A release is a specific version of the source and dependencies. Waitress is the server that runs our Flask app for this release. A smoke test is a short check of the most important behavior after deployment. A rollback returns the app code to a previous working version.

This first release is **private and local**. It uses a dedicated release folder and a fresh database on your computer. That makes the setup repeatable without a cloud account.

1. In the development environment, run `ENV-PY -m pip freeze` and save the output as requirements.txt. Keep it with app.py, init_db.py, schema.sql and templates/. Copy those source files into a fresh release folder, keeping the same directory structure.
2. Open a terminal in the release folder, create a fresh virtual environment as in Session 2 and run `ENV-PY -m pip install -r requirements.txt`. Run `ENV-PY init_db.py`. Check that the database file is in the release folder and leave it there between restarts.
3. From the activated environment run `waitress-serve --host=127.0.0.1 --port=8080 app:app`. On Windows you can use `.\.venv\Scripts\waitress-serve.exe` in place of waitress-serve, and on macOS/Linux use `.venv/bin/waitress-serve`. The first app in app:app names app.py. The second names the Flask variable inside it.
4. Open http://127.0.0.1:8080. Run the create → resolve → refresh check, restart Waitress, then verify the row still exists. Record the URL, run command, database path and results in your build notes.
5. For a future release, keep the previous source and dependency list. Stop the server before copying the SQLite file for a backup. Practice restoring the previous code against a **copy** of the release data. Check schema compatibility before any actual rollback.

**Ask AI.** “Review my private release instructions. Check that the web server binds to 127.0.0.1, dependencies come from requirements.txt, and database initialization preserves rows. Give me a smoke-test checklist. Explain how to diagnose an occupied port and a missing database. Do not claim the release passed until I provide the results.”

If you later want other people to use it, plan a host that runs the server and preserves the database across deployments. Add authenticated access and HTTPS before exposing the shared issue list. The local release teaches the same install → initialize → run → verify sequence.

Official references: [Flask quickstart](https://flask.palletsprojects.com/en/stable/quickstart/) · [Flask database tutorial](https://flask.palletsprojects.com/en/stable/tutorial/database/) · [Waitress deployment](https://flask.palletsprojects.com/en/stable/deploying/waitress/)

---


## Host the finished demo on PythonAnywhere

A host is a computer operated by a provider. A virtual environment there has its own installed Python packages. WSGI is the interface the host uses to load your Flask app. PythonAnywhere is the suggested beginner route for this SQLite app. Check the current [pricing page](https://www.pythonanywhere.com/pricing/) and choose Beginner/free if available. The account dashboard is the source for limits and any expiry or renewal date. If unavailable, use the local release above until you choose a host with persistent storage.

1. Open [PythonAnywhere](https://www.pythonanywhere.com/), choose the Beginner account during signup, pick a username and finish any verification. Open the dashboard. Your username is part of the app URL.
2. Push **your completed learning app** to a separate repository when you build it. For the first host exercise, open **Files**, make an issue-tracker folder under your home directory and upload the source files individually. Recreate templates/ inside it and upload index.html there. Upload requirements.txt. Start with a fresh demo database.
3. Open **Web → Add a new web app**, accept the offered domain, select **Manual configuration** and choose an available Python version. In a Bash console change to your issue-tracker folder. Run pythonX.Y -m venv ~/.virtualenvs/issue-tracker using the same version as the Web tab. Use ~/.virtualenvs/issue-tracker/bin/python to run pip install -r requirements.txt (via -m pip) and then init_db.py. Check that the file exists in the expected project directory.
4. In **Web**, enter /home/YOUR_USERNAME/.virtualenvs/issue-tracker as the virtualenv path. Open the WSGI configuration linked there. Following the [manual Flask setup](https://help.pythonanywhere.com/pages/Flask/), add your project directory to the import path and expose the Flask app object from app.py as application. Ask AI to explain the two settings and tailor the small WSGI edit to your redacted path. The host loads that object, so keep server startup out of the import path.
5. Click **Reload**, open the HTTPS address displayed in **Web** and create and resolve a fictional issue. Reload again and confirm the same row remains. If the page fails, open the **error log** from **Web**. A missing Flask module suggests the wrong virtualenv, an import error suggests the project path, and a missing table suggests initialization or database path. Check one hypothesis at a time.
6. Record the URL, release version, date, database path and smoke-test results. Before changing versions, export or back up the demo data using a consistent SQLite backup. To roll back, restore the previous source and compatible dependencies, reload and repeat the checks. Practice against a copy before restoring data.

**Ask AI:** “Use my release checklist and sanitized error log. Identify the first failing layer. Suggest one safe check. Do not change settings or delete data.” The owner handoff is a short demo, the release checklist and a note explaining how to diagnose a failed save.
