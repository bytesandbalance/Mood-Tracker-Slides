---
layout: section
background: black
theme: dracula
---

# Mood Tracker

---
layout: default
---

<a href="http://localhost:3001/track/2024-07-26" target="_blank">MoodTrackerPage</a>


**We'll build a detailed Mood Tracker page that includes:**
- Mood tracking with sliders
- Journal entries
- Various daily trackers (sleep, diet, activities)

---
layout: default
---


# Importing Dependencies

We start by importing necessary libraries and setting up some initial state.

```js
import React, { useState, useEffect } from 'react';
import { useParams } from 'react-router-dom';
import axios from 'axios';

import './App.css';

```

- **React Hooks**: `useState`, `useEffect`
- **Routing**: `useParams`
- **HTTP Requests**: `axios`
- **CSS Styling**: `./App.css`

---
layout: default
---

# State Management

Managing the state for the form data and loading status using `useState`.

```js {1|2|3-13|11|12}
const { date } = useParams();
const [hoveredMood, setHoveredMood] = useState(null);
const [formData, setFormData] = useState({
    journalEntry: '',
    triggers: '',
    sleepDuration: '',
    diet: '',
    physicalSymptoms: '',
    activities: '',
    energyLevel: 0,
    moodValues: MOODS.reduce((acc, mood) => ({ ...acc, [mood.name]: 0 }), {}),
    moodWeights: MOODS.reduce((acc, mood) => ({ ...acc, [mood.name]: 1 }), {}),
});
```

---
layout: default
---

# Understanding `reduce` in JavaScript

- **Purpose:** Accumulate values into a single result.

````md magic-move
```md
Simple Example:
```
```js
const total = [1, 2, 3].reduce((acc, val) => acc + val, 0); // Result: 6
```
```md
From MoodTrackerPage:
```
```js
const MOODS = [
    { name: 'happy', opposite: 'sad', emojis: ['😢', '😀'] },
    { name: 'calm', opposite: 'anxious', emojis: ['😰', '🧘'] },
    { name: 'motivated', opposite: 'lethargic', emojis: ['🥱', '💪'] },
    { name: 'focused', opposite: 'distracted', emojis: ['🤪', '🧐'] },
    { name: 'energetic', opposite: 'tired', emojis: ['😫', '⚡'] },
    { name: 'confident', opposite: 'insecure', emojis: ['😔', '😎'] },
    { name: 'grateful', opposite: 'ungrateful', emojis: ['😒', '🙏'] },
    { name: 'excited', opposite: 'bored', emojis: ['😑', '🤩'] },
    { name: 'content', opposite: 'discontent', emojis: ['😞', '😊'] },
    { name: 'loving', opposite: 'hateful', emojis: ['💔', '❤️'] },
];
```
```js
moodValues: MOODS.reduce((acc, mood) => ({ ...acc, [mood.name]: 0 }), {})
```
```js
{}
```
```js
{ happy: 0 }
```
```js
{ happy: 0, calm: 0 }
```
```js
{ happy: 0, calm: 0, motivated: 0 }
```
```js
{ happy: 0, calm: 0, motivated: 0, focused: 0 }
```
```js
{
  happy: 0,
  calm: 0,
  motivated: 0,
  focused: 0
  // other moods...
}
```
````

---
layout: default
---

# Quiz: Understanding State Management

### Question:

What does the `useState` hook do in a React component?

1. Renders HTML elements
2. Fetches data from an API
3. Manages and updates the component's state
4. Handles user events

---
layout: default
---

# Fetching Data

Fetching the existing mood tracker data from the backend when the component mounts using `useEffect`:

- `useEffect`: Used to perform side effects in the component, specifically to fetch data when the component mounts or when the `date` parameter changes. This ensures that we load the correct data for the selected date.


<a href="http://localhost:5000/get_entry/2024-07-01" target="_blank">First check out the backend</a>


---
layout: default
---


````md magic-move
```js {all|1}
useEffect(() => {
    const fetchEntry = async () => {
        try {
            const response = await axios.get(`http://localhost:5000/get_entry/${date}`);
            if (response.status === 200) {
                const data = response.data;
                setFormData({
                    journalEntry: data.journalEntry || '',
                    triggers: data.triggers || '',
                    sleepDuration: data.sleepDuration || '',
                    diet: data.diet || '',
                    physicalSymptoms: data.physicalSymptoms || '',
                    activities: data.activity || '',
                    energyLevel: data.energyLevel || 0,
                    moodValues: data.moodValues || {},
                    moodWeights: data.moodWeights || {},
                });
            }
        } catch (error) {
            console.error('Error fetching entry:', error);
        }
    };
    fetchEntry();
}, [date]);
```
```js {1}
const fetchEntry = async () => {
  try {
      const response = await axios.get(`http://localhost:5000/get_entry/${date}`);
      if (response.status === 200) {
          const data = response.data;
          setFormData({
              journalEntry: data.journalEntry || '',
              triggers: data.triggers || '',
              sleepDuration: data.sleepDuration || '',
              diet: data.diet || '',
              physicalSymptoms: data.physicalSymptoms || '',
              activities: data.activity || '',
              energyLevel: data.energyLevel || 0,
              moodValues: data.moodValues || {},
              moodWeights: data.moodWeights || {},
          });
      }
  } catch (error) {
      console.error('Error fetching entry:', error);
  }
};
```
```js {all|2|3|4|5-15|1-16|17-19|}
try {
    const response = await axios.get(`http://localhost:5000/get_entry/${date}`);
    if (response.status === 200) {
        const data = response.data;
        setFormData({
            journalEntry: data.journalEntry || '',
            triggers: data.triggers || '',
            sleepDuration: data.sleepDuration || '',
            diet: data.diet || '',
            physicalSymptoms: data.physicalSymptoms || '',
            activities: data.activity || '',
            energyLevel: data.energyLevel || 0,
            moodValues: data.moodValues || {},
            moodWeights: data.moodWeights || {},
        });
    }
} catch (error) {
    console.error('Error fetching entry:', error);
}
```
````
---
layout: default
---


# Understanding `useEffect` in React

- **`useEffect`** is a Hook in React that lets you perform side effects in function components.
- **Side effects** can include things like data fetching, subscriptions, or manually changing the DOM.
- **To Run Code on Component Updates**: Execute code when a component mounts, updates, or unmounts.
- **To Clean Up Resources**: Cleanup after a component is removed from the UI.

---
layout: default
---

# Simple Example: Mood Change

We want to update a message whenever the mood changes.


```jsx {all|4|5|7-10|15-16|17}
import React, { useState, useEffect } from 'react';

function MoodTracker() {
    const [mood, setMood] = useState('happy');
    const [message, setMessage] = useState('');

    useEffect(() => {
        // This runs when `mood` changes
        setMessage(`Your mood is now ${mood}!`);
    }, [mood]); // Dependency array

    return (
        <div>
            <h1>Mood Tracker</h1>
            <button onClick={() => setMood('happy')}>Happy</button>
            <button onClick={() => setMood('sad')}>Sad</button>
            <p>{message}</p>
        </div>
    );
}
```
---
layout: default
---

What Happens?

1. **Initial Render**: Displays the mood options and message.
2. **Mood Change**: When mood changes, `useEffect` runs and updates the message.

Key Points

- **Dependency Array**: `[mood]` ensures the effect runs only when `mood` changes.
- **Cleanup Function**: Not used here, but `useEffect` can return a cleanup function to handle resource cleanup.

---
layout: default
---

# Quiz: Understanding `useEffect`

**Question:**

When is the `useEffect` hook called in a React component?

1. Only when the component is first rendered
2. Only when the component is updated
3. When the component is first rendered and when specified state or props change
4. Only when the component is unmounted

---
layout: default
---

# Handling Input Changes

Updating the state as the user interacts with the form using `useState`.

````md magic-move
```js {1|2|3|4-7}
const handleSliderChange = (name, value) => {
    setFormData(prevData => ({
        ...prevData,
        moodValues: {
            ...prevData.moodValues,
            [name]: value
        }
    }));
};
```
```js {1|2|3|4-7}
const handleWeightChange = (name, event) => {
    setFormData(prevData => ({
        ...prevData,
        moodWeights: {
            ...prevData.moodWeights,
            [name]: parseInt(event.target.value, 10)
        }
    }));
};

// More handlers for other inputs...
```
````

---
layout: default
---

````md magic-move
```js
const [formData, setFormData] = useState({
    moodValues: {
        happy: 80,
        motivated: 30
    }
});
```


```js
const handleValueChange = (name, event) => {
    setFormData(prevData => ({
        ...prevData, // Copy all previous state properties
        moodValues: {
            ...prevData.moodValues, // Copy existing mood Values
            [name]: parseInt(event.target.value, 10) // Update specific mood Value
        }
    }));
};
```

```js
{
    moodValues: {
        happy: 80,
        motivated: 30
    }
}
```

```js
{
    moodValues: {
        happy: 80,
        sad: 55
    }
}
```
````


---
layout: default
---

# Rendering the Mood Sliders
- This part of the code iterates over the `MOODS` array and generates a slider for each mood.
````md magic-move
```js
return (
    <div className="app-container">
        <div className="mood-tracker">
            <h1>My Mood Tracker</h1>
            <p>Date: {new Date(date).toDateString()}</p>
            // We will fill this part
        </div>
    </div>
);
```
```js {all|1}
{MOODS.map(({ name, emojis: [leftEmoji, rightEmoji] }) => (
    <div
        key={name}
        className="mood-slider"
        onMouseEnter={() => setHoveredMood(name)}
        onMouseLeave={() => setHoveredMood(null)}
    >
        <span className="emoji">{leftEmoji}</span>
        <input
            type="range"
            id={name}
            min="0"
            max="100"
            value={formData.moodValues[name] || 0}
            onChange={(e) => handleSliderChange(name, e.target.value)}
        />
        {hoveredMood === name && (
            <span className="slider-value">{formData.moodValues[name] || 0}</span>
        )}
        // Skip rightEmoji
    </div>
))}
```
```js {1-6|7|8-15|16-18}
<div
    key={name}
    className="mood-slider"
    onMouseEnter={() => setHoveredMood(name)}
    onMouseLeave={() => setHoveredMood(null)}
>
    <span className="emoji">{leftEmoji}</span>
    <input
        type="range"
        id={name}
        min="0"
        max="100"
        value={formData.moodValues[name] || 0}
        onChange={(e) => handleSliderChange(name, e.target.value)}
    />
    {hoveredMood === name && (
        <span className="slider-value">{formData.moodValues[name] || 0}</span>
    )}
</div>
```
````

---
layout: default
---

# Understanding `map` in JavaScript

- **Purpose:** Transform each element in an array to a new array.
````md magic-move
```md
Simple Example:
```
```js
const doubled = [1, 2, 3].map(val => val * 2); // Result: [2, 4, 6]
```
```md
From MoodTrackerPage:
```
```js
const MOODS = [
    { name: 'happy', opposite: 'sad', emojis: ['😢', '😀'] },
    { name: 'calm', opposite: 'anxious', emojis: ['😰', '🧘'] },
    { name: 'motivated', opposite: 'lethargic', emojis: ['🥱', '💪'] },
    { name: 'focused', opposite: 'distracted', emojis: ['🤪', '🧐'] },
    { name: 'energetic', opposite: 'tired', emojis: ['😫', '⚡'] },
    { name: 'confident', opposite: 'insecure', emojis: ['😔', '😎'] },
    { name: 'grateful', opposite: 'ungrateful', emojis: ['😒', '🙏'] },
    { name: 'excited', opposite: 'bored', emojis: ['😑', '🤩'] },
    { name: 'content', opposite: 'discontent', emojis: ['😞', '😊'] },
    { name: 'loving', opposite: 'hateful', emojis: ['💔', '❤️'] },
];
```
```js
{MOODS.map(({ name, emojis: [leftEmoji, rightEmoji] }) => (
    <div
        key={name}
        className="mood-slider"
        onMouseEnter={() => setHoveredMood(name)}
        onMouseLeave={() => setHoveredMood(null)}
    >
        <span className="emoji">{leftEmoji}</span>
        <input
            type="range"
            id={name}
            min="0"
            max="100"
            value={formData.moodValues[name] || 0}
            onChange={(e) => handleSliderChange(name, e.target.value)}
        />
        {hoveredMood === name && (
            <span className="slider-value">{formData.moodValues[name] || 0}</span>
        )}
        // Skip rightEmoji
    </div>
))}
```
````

---
layout: default
---

```js
{MOODS.map(({ name, emojis: [leftEmoji, rightEmoji] }) => (
    <div
        key={name}
        className="mood-slider"
        onMouseEnter={() => setHoveredMood(name)}
        onMouseLeave={() => setHoveredMood(null)}
    >
        <span className="emoji">{leftEmoji}</span>
        <input
            type="range"
            id={name}
            min="0"
            max="100"
            value={formData.moodValues[name] || 0}
            onChange={(e) => handleSliderChange(name, e.target.value)}
        />
        {hoveredMood === name && (
            <span className="slider-value">{formData.moodValues[name] || 0}</span>
        )}
        // Skip rightEmoji
        // Skip moodWeights
    </div>
))}
```
<arrow v-click="[1]" x1="320" y1="80" x2="320" y2="180" color="#953" width="2" arrowSize="1" />
<arrow v-click="[2]" x1="400" y1="80" x2="195" y2="400" color="#953" width="2" arrowSize="1" />



---
layout: default
---

# Journal and Additional Trackers

Adding a journal section and additional daily trackers. Here's one example:

```js
<div className="journal-and-tracker">
    <div className="journal">
        <h2>Journal</h2>
        <textarea
            value={formData.journalEntry}
            onChange={handleJournalChange}
            placeholder="Write about your day..."
        />
        {/* More trackers can be added similarly */}
    </div>
</div>
```

- This section contains a journal entry textarea where the user can write about their day. Similar inputs can be added for other trackers like sleep, diet, and physical symptoms.

---
layout: default
---

# Saving the Entry

Submitting the form data to the backend.

````md magic-move
```js {1|3-9|10-12|13-16}
const handleSave = async () => {
    try {
        const response = await axios.post('http://localhost:5000/save', {
            date,
            journalEntry: formData.journalEntry,
            triggers: formData.triggers,
            sleepDuration: formData.sleepDuration,
            // rest of entries
        });
        if (response.status === 201) {
            alert('Entry saved successfully');
        }
    } catch (error) {
        console.error('Error saving entry:', error);
        alert('Error saving entry');
    }
};
```
```js
<div className="save-button-container">
    <button onClick={handleSave} className="save-button">
        Save
    </button>
</div>
```
````

- The `handleSave` function collects all the form data and sends it to the backend to be saved. If the save is successful, it alerts the user.


---
layout: default
---

# Assignment

Create a new feature to calculate the overall feeling based on mood values and weights.

1. **Component Structure:**
   - **Function Name:** `OverallFeeling`
   - **Props:** `moodValues`, `moodWeights`
   - **Return:** A `<div>` element with a header, a paragraph, and a button.

2. **Adding State:**
   - **State Hook:** Add a state variable called `overallFeeling` initialized to `0`.


3. **Calculate Overall Feeling:**
   - **Function:** Create a function to calculate the weighted average of mood values and weights.
   - **Update State:** Use the function to update the `overallFeeling` state when the button is clicked.


---
layout: default
---


4. **Rendering:**
   - **Display:** Render the `overallFeeling` state inside the paragraph element.
   - **Button:** Add an `onClick` event to the button to trigger the calculation.

5. **Integration:**
   - **App Component:** Import and render `OverallFeeling` inside the `App` component, passing `moodValues` and `moodWeights` as props.
