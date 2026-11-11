# Set up and build the first screen

**Prerequisites.** A terminal runs written commands. A project folder holds the app files. HTML describes what appears in the browser. A virtual environment keeps this project’s Python packages separate. Flask is a Python package that connects a browser address to a Python function. A route is that connection.

Install Python 3 and open a terminal inside a new folder named issue-tracker. On Windows use PowerShell. Run:

```powershell
py --version
py -m venv .venv
.\.venv\Scripts\python.exe -m pip install Flask waitress
```

On macOS or Linux, use `python3` instead of `py` and `.venv/bin/python` instead of the Windows environment path. In later commands, **ENV-PY** means the full environment path above. Replace it before running.

Create an `app.py` file and a `templates` folder. Create `templates/index.html` with the heading and a fixed example issue. Create the route in app.py using the AI task below.



The decorator, the line beginning with @, connects a GET request at / to index(). GET means the browser is asking to read a page. The function loads the HTML template and returns the page. Run `ENV-PY -m flask --app app run` and open http://127.0.0.1:5000. This address points to your computer. Press Ctrl+C in the terminal to stop the server.

**Ask AI.** “Create only templates/index.html for my Flask route. Use plain HTML with a heading and one example issue, Projector won’t turn on. Explain the heading and list tags. Return the file and the browser check.”

**Review.** Open the file and locate the text you see on screen. Change it yourself, refresh and explain the result. If the route fails, check the terminal error and confirm the folder is named templates.

