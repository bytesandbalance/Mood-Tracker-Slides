---
layout: section
background: black
theme: dracula
---

# Basics

---
layout: default
---

# Building a Mood Tracker with React
<a href="http://localhost:3001" target="_blank">App</a>

We'll build a fun and interactive mood tracker using React.

- **Concepts Covered:**
  - HTML Basics
  - CSS Styling
  - React Components
  - State Management
  - React Router
  - Calendar

---
layout: default
---

# What is HTML?

HTML stands for **HyperText Markup Language**. It's the standard language for creating and structuring web pages.

**HTML Code Example:**

```html {1|2-14|3-5|4|6-11|7|8-9|10}
<!DOCTYPE html>
<html>
<head>
    <title>Bytes&Balance</title>
</head>
<body>
    <h1>Welcome to Bytes&Balance</h1>
    <p>By visiting my Patreon page, you'll find a range of engaging and educational courses designed to help you master
        new skills and achieve your goals.</p>
    <a href="https://www.patreon.com/bytesandbalance">Visit Bytes&Balance</a>
</body>
</html>
```

- **HTML** is written as **JSX**, a syntax extension that allows you to write HTML-like code inside JavaScript files.

---
layout: default
---

<!DOCTYPE html>
<html>
<head>
    <title>Bytes&Balance</title>
</head>
<body>
    <h1>Welcome to Bytes&Balance</h1>
    <p>By visiting my Patreon page, you'll find a range of engaging and educational courses designed to help you master
        new skills and achieve your goals.</p>
    <p>Your support not only grants you access to exclusive content and resources but also helps me continue creating
        high-quality material.</p>
    <a href="https://www.patreon.com/bytesandbalance">Visit Bytes&Balance</a>
</body>
</html>

---
layout: default
---

# What is CSS?

CSS stands for **Cascading Style Sheets**. It is used to style and layout web pages.

**CSS Code Example:**

```css {all|1-6|8-13}
body {
  font-family: sans-serif;
  text-align: center;
  background-color: #222;
  color: #eee;
}

.calendar-container {
  padding: 20px;
  background-color: #444;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
}
```

- **CSS** is used to style React components. Styles can be applied globally or scoped to specific components.

---
layout: default
---


# Understanding React Components

Components are the building blocks of React applications.

**Example Component:**

```js
import React from 'react';

function BytesAndBlance() {
  return <h1>Coding with Creativity, Living with Balance!</h1>;
}

export default BytesAndBalance;
```

- **Functional Component:** A simple function that returns JSX (HTML-like syntax in JavaScript).
- **JSX:** Syntax extension to write HTML in JavaScript.


---
layout: default
---

**Using a Component:**

```js
import BytesAndBalance from './BytesAndBalance';

function App() {
  return (
    <div>
      <BytesAndBalance />
    </div>
  );
}

export default App;
```

**`<BytesAndBalance />`**: Renders the `BytesAndBalance` component.

---
layout: default
---

# What is State Management?

State management is about keeping track of information in an application.

**Imagine:**
- You have a diary where you write your daily mood.
- If you want to see or update your mood, you refer to this diary.

In a web app, **state** is like this diary. It keeps track of things like what date you’ve selected or what mood you’re currently tracking.

---
layout: default
---

**Example:**

```js {all|4|9}
import React, { useState } from 'react';

function MoodTracker() {
  const [mood, setMood] = useState('Happy');

  return (
    <div>
      <h1>Current Mood: {mood}</h1>
      <button onClick={() => setMood('Sad')}>Change Mood</button>
    </div>
  );
}

export default MoodTracker;
```

- **`useState` Hook:** A tool to manage state in React components. It helps keep track of the current mood and update it.

---
layout: default
---

# Quiz: Conceptual Understanding of React Components and State

**Question:**

Which of the following statements best describes the purpose of React components and state management in a React application?

1. React components are used to encapsulate the UI and logic of an application. State management within components enables the tracking and updating of dynamic data that affects the UI.

2. React components are mainly used to handle user input, while state management is used only for managing the application's styling.

3. React components are responsible for routing between different pages, and state management is used to manage the content of static HTML elements.

4. React components are used to define global styles for the application, while state management is used to handle API requests and responses.

---
layout: default
---


# What is Routing?

Routing is like having different pages or sections in a book that you can jump to.

**Imagine:**
- You have a book with chapters.
- If you want to read Chapter 2, you go directly to it from the Table of Contents.

In a web app, **routing** lets you navigate between different pages (like "Home", "Profile", or "Settings") without reloading the whole page.


---
layout: default
---

**Example:**

```js {all|7-12}
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import HomePage from './HomePage';
import ProfilePage from './ProfilePage';

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<HomePage />} />
        <Route path="/profile" element={<ProfilePage />} />
      </Routes>
    </Router>
  );
}

export default App;
```

- **`Routes` and `Route` Components:** Define how users navigate through different parts of the app. `Route` specifies what component to display based on the URL.

---
layout: default
---

# Creating the Main App Component (App.js)
The `App` component is the root of our application:

````md magic-move
```js
import React, { useState } from 'react';
import { BrowserRouter as Router, Route, Routes, useNavigate } from 'react-router-dom';
import CalendarPage from './CalendarPage';
import MoodTrackerPage from './MoodTrackerPage';
import MonthlyInsightPage from './MonthlyInsightPage';
```

```js
function App() {
  const [selectedDate, setSelectedDate] = useState(new Date());

  return (
    <Router>
      <Routes>
        <Route path="/" element={<CalendarPageWrapper setSelectedDate={setSelectedDate} />} />
        <Route path="/track/:date" element={<MoodTrackerPage />} />
        <Route path="/insight/:month" element={<MonthlyInsightPage />} />
      </Routes>
    </Router>
  );
}
```
```js {all|3}
function CalendarPageWrapper({ setSelectedDate }) {
  const navigate = useNavigate();
  return <CalendarPage setSelectedDate={setSelectedDate} navigate={navigate} />;
}
```
```js
function App() {
  const [selectedDate, setSelectedDate] = useState(new Date());

  return (
    <Router>
      <Routes>
        <Route path="/" element={<CalendarPageWrapper setSelectedDate={setSelectedDate} />} />
        <Route path="/track/:date" element={<MoodTrackerPage date={selectedDate} />} />
        <Route path="/insight/:month" element={<MonthlyInsightPage />} />
      </Routes>
    </Router>
  );
}

function CalendarPageWrapper({ setSelectedDate }) {
  const navigate = useNavigate();
  return <CalendarPage setSelectedDate={setSelectedDate} navigate={navigate} />;
}

export default App;
```

````
---
layout: default
---

# Calendar: Updating View Date and Navigating to Monthly Insight (CalendarPage.jsx)
<a href="http://localhost:3001" target="_blank">Calendar</a>


````md magic-move
```md
- activeStartDate is passed automatically by the react-calendar component when the view changes.
- It helps in updating the displayed month (viewDate).
```
```js {1|3-5|7-9|1-14}
const [viewDate, setViewDate] = useState(new Date()); // State to track the displayed month

const onActiveStartDateChange = ({ activeStartDate }) => {
    setViewDate(activeStartDate); // Update the displayed month when the calendar view changes
};

const getCurrentMonth = () => {
    return format(viewDate, 'yyyy-MM'); // Extract the displayed month in YYYY-MM format
};

const handleMonthlyInsight = () => {
    const month = getCurrentMonth();
    navigate(`/insight/${month}`);
};
```
````

- **`onActiveStartDateChange`**: Updates the `viewDate` state when the calendar's displayed month changes.
- **`handleMonthlyInsight`**: Navigates to the Monthly Insight page for the current viewed month.

---
layout: default
---

# Calendar: Selecting a Date and Navigating to Mood Tracker (CalendarPage.jsx)

```js {1|3-7}
const [date, setDate] = useState(new Date()); // State to track the selected date

const onChange = (date) => {
    setDate(date);
    setSelectedDate(date);
    navigate(`/track/${format(date, 'yyyy-MM-dd')}`); // Navigate to mood tracker page with the selected date
};
```

- **`onChange`**: Updates the `date` state when a new date is selected.
- **Navigates to**: The Mood Tracker page for the selected date in `yyyy-MM-dd` format.

---
layout: default
---

# Assignment: Enhance the `CalendarPage` Component

Extend the functionality of the `CalendarPage` component by adding the following features:

1. **Mark Special Dates**:
   - Create a list of special dates (Birthdays, Events, ...) with corresponding information.
   - Use the `tileContent` prop of the `react-calendar` component to highlight these dates.

2. **Tooltip on Hover**:
   - Display a tooltip when hovering over a special date.
   - Use a library like `react-tooltip` for this feature.
