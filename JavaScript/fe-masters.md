## Chart Examples

Different ways to model the same weather day.

Data shape
``` javascript
{
    date: Timestamp,
    high: number,
    low: number,
    avgTemp: number
}
```
1. Bar Chart
    - 365 `<rect/>`'s (bars)
    - domain: each day of the year
    - range: high point is the high temp for each day
        - height = high - low
        - color/shading of bar = avg. temp for the day

2. Line Chart 
    - 2 `<path />`s
        - d: line commands that connect points
        - for each point:
            - x: date
            - y: temperature
            - fill: red for high temps, blue for low temps

3. Radial Chart (polar graph)
    - 365 `<path />`s
        - d: line + curve commands to make slices (bars rotated around origin)
        - for each slice (bar):
            - angle: day
            - inner radius: low temp
            - outer radius: high temp
            - shading: average temp
        - same as the bar chart but radial instead of linear domain
    - Good use case for radial data
        - Anytime you have a slice of repetitive cyclical data (an hour, a month, a year, etc)