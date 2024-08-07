---
layout: section
background: black
theme: dracula
---

# Backend: Flask Application and SQLite

---
layout: default
---

# Project Setup

Install Flask and SQLite

```bash
pip install Flask
pip install Flask-Cors
```

Set up project directory

```plaintext
backend/
├── app.py
├── mood_tracker.db
```

Create a basic Flask application

```python
from flask import Flask
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

if __name__ == "__main__":
    app.run(debug=True)
```

---
layout: default
---

# Flask Application Structure

Overview of `app.py`
  - Importing libraries.
  - Initializing Flask and CORS.
  - Setting up routes.
  - Running the app in debug mode.

```python
from flask import Flask, request, jsonify
from flask_cors import CORS
import sqlite3

app = Flask(__name__)
CORS(app)
```

---
layout: default
---

# Setting Up SQLite Database

How to create `mood_tracker.db`:

```python
import sqlite3

conn = sqlite3.connect("mood_tracker.db")
cursor = conn.cursor()
cursor.execute("""
CREATE TABLE IF NOT EXISTS mood_entries (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    date TEXT NOT NULL UNIQUE,
    journal_entry TEXT,
    triggers TEXT,
    // rest of the variables
    )
""")
conn.commit()
conn.close()
```

---
layout: default
---

# Fetching a Journal Entry

<a href="http://localhost:5000/get_entry/2024-07-01" target="_blank">get_entry endpoint</a>

````md magic-move
```python {1|3-4|5-11}
@app.route("/get_entry/<date>", methods=["GET"])
def get_entry(date):
    conn = sqlite3.connect("mood_tracker.db")
    cursor = conn.cursor()
    cursor.execute("""
        SELECT
            journal_entry, triggers, sleep_duration,
            // rest of the variables
        FROM mood_entries
        WHERE date = ?
    """, (date,))
    entry = cursor.fetchone()
    conn.close()
```
```python {4-10|12}
def get_entry(date):
  // As Above
  if entry:
      return jsonify({
          "date": date,
          "journalEntry": entry[0],
          "triggers": entry[1],
          "sleepDuration": entry[2],
          // rest of the variables
      })
  else:
      return jsonify({"message": "No entry found for this date"}), 404
```
````

---
layout: default
---

# Fetching Monthly Data

<a href="http://localhost:5000/get_monthly_data/2024-07" target="_blank">get_monthly_data endpoint</a>

````md magic-move
```python {1|3-4|5-11|12-13}
@app.route("/get_monthly_data/<month>", methods=["GET"])
def get_monthly_data(month):
    conn = sqlite3.connect("mood_tracker.db")
    cursor = conn.cursor()
    cursor.execute("""
        SELECT
            date, journal_entry, triggers, sleep_duration,
            // rest of the variables
        FROM mood_entries
        WHERE strftime('%Y-%m', date) = ?
    """, (month,))
    entries = cursor.fetchall()
    conn.close()
```
```python {3-9|11}
def get_monthly_data(month):
    // As Above
    data = [{
        "date": entry[0],
        "journalEntry": entry[1],
        "triggers": entry[2],
        "sleepDuration": entry[3],
        // rest of the variables
    } for entry in entries]

    return jsonify(data)
```
````


---
layout: default
---

# Saving Journal Entries

`save_entry` endpoint:

````md magic-move
```python {1|3-9}
@app.route("/save", methods=["POST"])
def save_entry():
    data = request.json
    # Extract data from request
    date = data.get("date")
    journal_entry = data.get("journalEntry")
    triggers = data.get("triggers")
    sleep_duration = data.get("sleepDuration")
    // rest of the variables
```
```python {3-4|5-13|14-15|17}
def save_entry():
  // As above
  conn = sqlite3.connect("mood_tracker.db")
  cursor = conn.cursor()
  cursor.execute("""
      INSERT OR REPLACE INTO mood_entries (
          date, journal_entry, triggers, sleep_duration,
          // rest of the variables
      ) VALUES (?, ?, ?, ?, // rest of the variables)
  """, (
      date, journal_entry, triggers, sleep_duration,
      // rest of the variables
  ))
  conn.commit()
  conn.close()

  return jsonify({"status": "success"}), 201
```
````

---
layout: default
---

# Enabling CORS and Testing APIs

CORS (Cross-Origin Resource Sharing) allows your server to accept requests from different domains, enabling the API to be accessed from web applications hosted on other domains.

How to enable CORS in Flask:

```python
from flask_cors import CORS
app = Flask(__name__)
CORS(app)
```

How to test the APIs using tools like Postman or cURL:

```bash
# Example cURL command to test save_entry endpoint
curl -X POST -H "Content-Type: application/json" -d '{"date": "2023-08-01", "journalEntry": "Today was a good day.", "triggers": "none", "sleepDuration": 8,//rest of the variables}' http://localhost:5000/save
```
---
layout: default
---

# Assignment

Extend the Mood Tracker app to:
  1. Create a new endpoint to delete a journal entry by date.
  2. Use the following code snippet as a starting point:

Additional Challenge: Add validation to ensure the date exists before attempting to delete.
