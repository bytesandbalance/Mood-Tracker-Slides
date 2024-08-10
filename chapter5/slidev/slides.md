---
layout: section
background: black
theme: dracula
---

# Monthly Insight

---
layout: default
---

# Overview

<a href="http://localhost:3001/insight/2024-07" target="_blank">MonthlyInsightPage</a>

1. **State and Effect Hooks**
   - `useState` is used to store the `monthlyData` retrieved from the server.
   - `useEffect` is used to fetch the monthly data from an API endpoint when the `month` parameter changes. It then triggers the drawing of various charts.

2. **Drawing Charts**
   - The component has functions to draw different types of charts using D3.js:
     - `drawMoodChart`: Displays a bar chart for mood data.
     - `drawEnergyLineChart`: Displays a line chart for energy levels.
     - `drawPieChart`: Displays pie charts for diet, activity, and physical symptoms.
     - `drawSleepDurationChart`: Displays a bar chart for sleep duration.


---
layout: default
---

# Data Fetching

```js {all|1|13|2|5|6|7-9|10}
useEffect(() => {
    axios.get(`http://localhost:5000/get_monthly_data/${month}`)
        .then(response => {
            setMonthlyData(response.data);
            drawMoodChart(response.data);
            drawEnergyLineChart(response.data);
            drawPieChart(response.data, 'diet', '#dietChart');
            drawPieChart(response.data, 'activity', '#activityChart');
            drawPieChart(response.data, 'physicalSymptoms', '#physicalSymptomsChart');
            drawSleepDurationChart(response.data);
        })
        .catch(error => console.error('Error fetching monthly data:', error));
}, [month]);
```

- Fetches data based on the `month` URL parameter.
- Updates `monthlyData` and calls various functions to render charts.


---
layout: default
---

# Drawing the Mood Chart
````md magic-move
```js
// Clear any existing chart
const drawMoodChart = (data) => {
//
    d3.select('#moodChart').selectAll('*').remove();

    // The rest of the code
};
```
```js
Example: const total = [1, 2, 3].reduce((acc, val) => acc + val, 0); // Result: 6
```
```js
// Aggregate mood values and weights
const aggregatedMoodValues = data.reduce((acc, entry) => {
    for (let mood in entry.moodValues) {
        if (!acc[mood]) {
            acc[mood] = { totalValue: 0, totalWeight: 0 };
        }
        acc[mood].totalValue += entry.moodValues[mood] * entry.moodWeights[mood];
        acc[mood].totalWeight += entry.moodWeights[mood];
    }
    return acc;
}, {});
```
```js
const doubled = [1, 2, 3].map(val => val * 2); // Result: [2, 4, 6]
```
```js
// Calculate weighted averages
const chartData = Object.keys(aggregatedMoodValues).map(key => ({
    mood: key.charAt(0).toUpperCase() + key.slice(1),
    value: aggregatedMoodValues[key].totalValue / aggregatedMoodValues[key].totalWeight
}));
```
```js
// Set dimensions and margins for the chart
const margin = { top: 20, right: 30, bottom: 60, left: 50 },
    width = 800 - margin.left - margin.right,
    height = 400 - margin.top - margin.bottom;
```
```js
// Append SVG object to the div
const svg = d3.select("#moodChart")
    .append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
    .attr("class", "chart-svg")
    .append("g")
    .attr("transform", `translate(${margin.left},${margin.top})`);
```
```js
// X axis
const x = d3.scaleBand()
    .domain(chartData.map(d => d.mood))
    .range([0, width])
    .padding(0.1);

svg.append("g")
    .attr("transform", `translate(0,${height})`)
    .call(d3.axisBottom(x).tickSize(0).tickPadding(10))
    .selectAll("text")
    .attr("class", "axis-label")
    .style("text-anchor", "end")
    .attr("transform", "rotate(-45)");

svg.append("text")
    .attr("class", "axis-label")
    .attr("x", width / 2)
    .attr("y", height + margin.bottom - 10)
    .attr("text-anchor", "middle")
    .text("Mood");
```
```js
// Y axis
const y = d3.scaleLinear()
    .domain([0, d3.max(chartData, d => d.value)])
    .nice()
    .range([height, 0]);

svg.append("g")
    .call(d3.axisLeft(y).ticks(5))
    .selectAll("text")
    .attr("class", "axis-label");

svg.append("text")
    .attr("class", "axis-label")
    .attr("transform", "rotate(-90)")
    .attr("x", -height / 2)
    .attr("y", -margin.left + 15)
    .attr("text-anchor", "middle")
    .text("Weighted Average");
```
```js
// Bars
svg.selectAll(".bar")
    .data(chartData)
    .enter().append("rect")
    .attr("class", "bar")
    .attr("x", d => x(d.mood))
    .attr("y", d => y(d.value))
    .attr("width", x.bandwidth())
    .attr("height", d => height - y(d.value))
    .attr("fill", "steelblue")
    .on("mouseover", function (event, d) {
        d3.select(this).attr("fill", "orange");
    })
    .on("mouseout", function (event, d) {
        d3.select(this).attr("fill", "steelblue");
    });
```
````

---
layout: default
---


# Drawing the Energy Line Chart

````md magic-move
```js
const drawEnergyLineChart = (data) => {
    d3.select('#energyChart').selectAll('*').remove();

    // The rest of the code
};
```
```js
const lineData = data.map(entry => ({
    date: new Date(entry.date),
    energyLevel: entry.energyLevel
}));
```
```js
const margin = { top: 20, right: 30, bottom: 60, left: 50 },
    width = 800 - margin.left - margin.right,
    height = 400 - margin.top - margin.bottom;
```
```js
const svg = d3.select("#energyChart")
    .append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
    .attr("class", "chart-svg")
    .append("g")
    .attr("transform", `translate(${margin.left},${margin.top})`);
```
```js
const x = d3.scaleTime()
    .domain(d3.extent(lineData, d => d.date))
    .range([0, width]);

svg.append("g")
    .attr("transform", `translate(0,${height})`)
    .call(d3.axisBottom(x).tickFormat(d3.timeFormat("%Y-%m-%d")).tickSize(0).tickPadding(10))
    .selectAll("text")
    .attr("class", "axis-label")
    .style("text-anchor", "end")
    .attr("transform", "rotate(-45)");

svg.append("text")
    .attr("class", "axis-label")
    .attr("x", width / 2)
    .attr("y", height + margin.bottom - 10)
    .attr("text-anchor", "middle")
    .text("Date");
```
```js
const y = d3.scaleLinear()
    .domain([0, d3.max(lineData, d => d.energyLevel)])
    .nice()
    .range([height, 0]);

svg.append("g")
    .call(d3.axisLeft(y).ticks(5))
    .selectAll("text")
    .attr("class", "axis-label");

svg.append("text")
    .attr("class", "axis-label")
    .attr("transform", "rotate(-90)")
    .attr("x", -height / 2)
    .attr("y", -margin.left + 15)
    .attr("text-anchor", "middle")
    .text("Energy Level");
```
```js {1-3|5-10}
const line = d3.line()
    .x(d => x(d.date))
    .y(d => y(d.energyLevel));

svg.append("path")
    .datum(lineData)
    .attr("fill", "none")
    .attr("stroke", "steelblue")
    .attr("stroke-width", 2)
    .attr("d", line);
```
````
---
layout: default
---

# Drawing Pie Charts

````md magic-move
```js
const drawPieChart = (data, key, selector) => {
    d3.select(selector).selectAll('*').remove();

    // The rest of the code
};
```
```js
const aggregatedData = data.reduce((acc, entry) => {
    if (!acc[entry[key]]) {
        acc[entry[key]] = 0;
    }
    acc[entry[key]] += 1;
    return acc;
}, {});

const chartData = Object.keys(aggregatedData).map(key => ({
    label: key,
    value: aggregatedData[key]
}));
```
```js
const width = 600,
    height = 600,
    radius = Math.min(width, height) / 2;
```
```js
const svg = d3.select(selector)
    .append("svg")
    .attr("width", width)
    .attr("height", height)
    .attr("class", "chart-svg")
    .append("g")
    .attr("transform", `translate(${width / 2},${height / 2})`);
```
```js
const color = d3.scaleOrdinal(d3.schemeCategory10);
```
```js {1-3|5-7|9-15|17-23}
const pie = d3.pie()
    .value(d => d.value)
    .sort(null);

const arc = d3.arc()
    .innerRadius(0)
    .outerRadius(radius);

svg.selectAll('arc')
    .data(pie(chartData))
    .enter().append('path')
    .attr('d', arc)
    .attr('fill', d => color(d.data.label))
    .attr('stroke', '#ffffff')
    .attr('stroke-width', 1);

svg.selectAll('text')
    .data(pie(chartData))
    .enter().append('text')
    .attr('transform', d => `translate(${arc.centroid(d)})`)
    .attr('dy', '0.35em')
    .style('text-anchor', 'middle')
    .text(d => d.data.label);
```
````

---
layout: default
---

# JSX Structure

The `return` statement renders the component with various chart containers:

```js
return (
    <div>
        <h1>Monthly Insight for {month}</h1>
        <div className="chart-container">
            <div className="chart-wrapper">
                <div className="chart-title">Mood Chart</div>
                <div id="moodChart"></div>
            </div>
            // The other charts
        </div>
    </div>
);
```
- Each chart has its own container `div` with an `id` that matches the selector used in the `drawPieChart` and other chart drawing functions.

---
layout: default
---

# Assignment: Add Hover Effects to Pie Chart

Enhance the existing pie chart to include hover effects that display additional information about each slice, such as the percentage of the total.

1. **Integrate Tooltip**:
   - Add a tooltip that will display the label and percentage of the slice being hovered over.

2. **Add Hover Effects**:
   - Change the appearance of the slice on hover (e.g., slightly expand the slice or change its color).
   - Display the tooltip with the relevant information.

3. **Modify the Existing Code**:
   - Update the existing `drawPieChart` function to include these enhancements.
