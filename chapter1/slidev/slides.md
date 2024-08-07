---
layout: section
background: black
theme: dracula
---

# Prerequisites

---
layout: default
---

# Getting started with GitHub

<a href="https://docs.github.com/en/get-started/start-your-journey
" target="_blank">start-your-journey</a>

---
layout: default
---

# Getting Started with GitPod

**1. Sign Up**
- Go to [GitPod](https://www.gitpod.io) and sign up with your GitHub, GitLab, or Bitbucket account.

**2. Install the Browser Extension (Optional)**
- Get the GitPod extension for Chrome or Firefox to add a quick launch button to your repos.

**3. Launch a Workspace**
- Click the GitPod button on any repo or add `gitpod.io/#` before a repo URL. Example: `https://gitpod.io/new/#github.com/pflashgary/Early-STEM-Mood-Tracker`.


---
layout: default
---

# Basic Workflow

1. **Open a Repo**: Open any GitHub repo in GitPod.
2. **Make Changes**: Edit files in the GitPod editor and use the terminal for commands.
3. **Commit Changes**:
   ```sh
   git add .
   git commit -m "Your message"
   git push
   ```
4. **Run Apps**: Run your projects directly in GitPod. Ports will be forwarded automatically.

---
layout: default
---

# Cool Features

- **Prebuilds**: Add a `.gitpod.yml` file to your repo for prebuilt environments.
  ```yaml
  tasks:
    - init: npm install
      command: npm start
  ```
- **Port Forwarding**: GitPod gives you URLs for your running apps.
- **Live Share**: Collaborate in real-time with [others](https://www.gitpod.io/docs/configure/workspaces/collaboration).

---
layout: default
---

# Getting Started with VS Code in GitPod

1. **Launch a GitPod Workspace**
   - Open any GitHub repo in GitPod by adding `gitpod.io/#` before the repo URL, like this: `https://gitpod.io/new/#github.com/pflashgary/Early-STEM-Mood-Tracker`.

2. **Explore the VS Code Interface in GitPod**
   - **File Explorer**: Shows your project files on the left.
   - **Editor**: The main area where you write your code.
   - **Terminal**: Access it from the bottom or using the `Ctrl+` ` (backtick) shortcut to run commands.
   - **Source Control**: Manage your Git operations directly in the sidebar.

---
layout: default
---

3. **Basic Features**
   - **Extensions**: Enhance your coding experience by adding extensions from the Extensions view (`Ctrl+Shift+X`).
   - **Search**: Use the search function (`Ctrl+Shift+F`) to find text within your project.
   - **Command Palette**: Access the command palette with `Ctrl+Shift+P` to run various commands.
   - **Debugging**: Set breakpoints and run the debugger from the Debug view on the left sidebar.

4. **VS Code Documentation**: [Get Started](https://code.visualstudio.com/docs)
   - A comprehensive guide covering the basics of VS Code.

---
layout: default
---

# Getting Started with Bash Scripting in GitPod

**1. Launch a GitPod Workspace**
- Open any GitHub repo in GitPod by adding `gitpod.io/#` before the repo URL, like this: `https://gitpod.io/new/#github.com/pflashgary/Early-STEM-Mood-Tracker`.

**2. Open the Terminal**
- Access the terminal in GitPod by clicking the terminal icon or using the shortcut `Ctrl+` ` (backtick).

---
layout: default
---

# Basic Bash Commands

Here are some fundamental Bash commands to get started:
- `ls`: List directory contents.
- `cd`: Change directory.
- `pwd`: Print working directory.
- `mkdir`: Create a new directory.
- `rm`: Remove files or directories.
- `cp`: Copy files or directories.
- `mv`: Move or rename files or directories.
- `echo`: Display a line of text.

---
layout: default
---

# Writing Your First Bash Script

1. **Create a New Script File**:
   - In the terminal, create a new file:
     ```sh
     touch bytes_and_balance.sh
     ```

2. **Open the Script in the Editor**:
   - Open `bytes_and_balance.sh` in the GitPod editor and add the following content:
     ```sh
     #!/bin/bash
     echo "Hello, Bytes&Balance!"
     ```

3. **Make the Script Executable**:
   - In the terminal, make your script executable:
     ```sh
     chmod +x bytes_and_balance.sh
     ```

---
layout: default
---

4. **Run the Script**:
   - Execute your script in the terminal:
     ```sh
     ./bytes_and_balance.sh
     ```
---
layout: default
---

# Basic Bash Scripting Concepts

- **Variables**:
  ```sh {monaco-run}
  name="Bytes&Balance"
  echo "Hello, $name!"
  ```

- **Conditional Statements**:
  ```sh {monaco-run}
  if [ -f "bytes_and_balance.sh" ]; then
      echo "File exists."
  else
      echo "File does not exist."
  fi
  ```

- **Loops**:
  ```sh {monaco-run}
  for i in {1..5}; do
      echo "Welcome $i times"
  done
  ```

---
layout: default
---

# Useful Links for Learning Bash

- **Bash Guide**: [Bash Beginner’s Guide](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
  - A comprehensive guide for beginners.
- **Bash Reference Manual**: [GNU Bash Manual](https://www.gnu.org/software/bash/manual/bash.html)
  - Detailed reference for Bash scripting.
- **Interactive Tutorial**: [Learn Shell](https://www.learnshell.org/)
  - An interactive online tutorial for learning shell scripting.

---
layout: default
---

# Getting Started with Javascript

Here are some fundamental Javascript concepts and syntax to get started:

**1. Variables**
- javascript uses `var`, `let`, and `const` to declare variables.
  ```ts {monaco-run}
  let name = 'Bytes&Balance';
  const greeting = 'Hello';
  var age = 20;
  ```

**2. Data Types**
- Common data types include strings, numbers, booleans, arrays, and objects.
  ```ts {monaco-run}
  let str = 'Hello, Bytes&Balance!';
  let num = 42;
  let isActive = true;
  let arr = [1, 2, 3];
  let obj = { name: 'Bytes&Balance', age: 2 };
  ```
---
layout: default
---

**3. Functions**
- Functions can be declared using function declarations or arrow functions.
  ```ts {monaco-run}
  function greet(name) {
    return `Hello, ${name}!`;
  }

  const greetArrow = (name) => {
    return `Hello, ${name}!`;
  };
  ```

**4. Conditionals**
- Use `if`, `else if`, and `else` for conditional statements.
  ```ts {monaco-run}
  let num = 10;

  if (num > 0) {
    console.log('Number is positive');
  } else if (num < 0) {
    console.log('Number is negative');
  } else {
    console.log('Number is zero');
  }
  ```

---
layout: default
---

**5. Loops**
- Common loops include `for`, `while`, and `do...while`.
  ```ts {monaco-run}
  for (let i = 0; i < 5; i++) {
    console.log(`Iteration ${i}`);
  }

  let count = 0;
  while (count < 5) {
    console.log(`Count is ${count}`);
    count++;
  }
  ```

**6. Arrays and Objects**
- Access and manipulate array elements and object properties.
  ```ts {monaco-run}
  let arr = ['Byte', '&', 'Balance'];
  console.log(arr[1]); // Outputs: banana

  let obj = { name: 'Bytes&Balance', age: 2 };
  console.log(obj.name); // Outputs: Bytes&Balance
  ```
---
layout: default
---

# Mood Tracker Project

- This project is designed to help you learn full-stack development by building a mood tracking application.
- The project is divided into frontend and backend components, with a basic setup provided to help you get started.

---
layout: default
---

# Branches

<a href="http://localhost:3001
" target="_blank">Mood Tracker App Dev vs Main</a>

The main branches are:

- **`main`**: Contains the final product with all features implemented.
- **`dev`**: Contains a basic setup with minimal components. You will branch off from this branch to work on your individual features.

---
layout: default
---


# Frontend: Basic Components in the `dev` Branch

1. **`App.js`**: The root component that sets up routing between different pages.
2. **`CalendarPage.js`**: Displays a calendar and provides a button to navigate to the Monthly Insight page.
3. **`MonthlyInsightPage.jsx`**: A placeholder component for displaying monthly insights.
4. **`MoodTrackerPage.jsx`**: A placeholder component for tracking mood entries.

---
layout: default
---


# Backend: Basic Components in the `dev` Branch

1. **`app.py`**: Provides a basic API with a single endpoint for retrieving mood entries by date.
2. **`database.py`**: Sets up the SQLite database and creates the necessary table.
3. **`mood_generator.py`**: Generates sample data for populating the database (not required for your contributions).

---
layout: default
---

# How to Contribute

1. **Clone the Repository**: Clone to your local machine:
    ```bash
    git clone https://github.com/your-username/mood-tracker.git
    ```
2. **Create a New Branch**: Create a new branch for your feature or fix. Start your branch name with your name followed by a description of the feature:
    ```bash
    git checkout -b your-name/feature-description
    ```
    For example, if your name is Lorentz and you are adding a new mood chart component, you might name your branch `Lorentz/mood-chart-component`.
3. **Implement Your Changes**: Make your changes or add new features to the code.

---
layout: default
---

4. **Commit Your Changes**: Commit your changes with a descriptive message:
    ```bash
    git add .
    git commit -m "Add feature: description of the feature"
    ```
5. **Push**: Push your changes to GitHub:
    ```bash
    git push origin your-name/feature-description
    ```
6. **Submit a Pull Request**: Go to the original repository and create a pull request from your branch. Provide a clear description of the changes you’ve made.

---
layout: default
---

# Setting Up the Frontend

1. **Navigate to the Frontend Directory**:
    ```bash
    cd frontend
    ```
2. **Install Dependencies**:
    ```bash
    npm install
    ```
3. **Run the Development Server**:
    ```bash
    npm start
    ```
---
layout: default
---

# Setting Up the Backend

1. **Navigate to the Backend Directory**:
    ```bash
    cd backend
    ```
2. **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```
3. **Set Up the Database**:
    ```bash
    python database.py
    ```
4. **Run the Flask Application**:
    ```bash
    python app.py
