# Frontend Masters: Data Visualization for React Developers
[Course Slides](https://slides.com/shirleywu/deck-11)

[Observable Notebook](https://beta.observablehq.com/@sxywu/data-visualization-for-react-developers-starter)

## Basic chart types

### Data Types
- Categorical (ex: movie genres)
- Ordinal (t-shirt sizes, like categorical w/ implied order)
- Quantitative (temperatures)
- Temporal (dates)
- Spatial (cities, geodata)


### Basic Charts

**Bar Chart**

For categorical comparisons

**Domain**: categorical (ex: movie genres)
**Range**: quantitative  (number of movies in that genre)

**Histogram**

For categorical distributions

**Domain**: quantitative bins (ex: movie metascore by 10s, ie, 10,20,30, etc)
**Range**: frequency of quantitative bin (# of movies in each score bin)

**Scatterplot**

For correlation
- Generally better for data exploration rather than a final display chart type

2 attributes and the relationship between the quantitative values
- Ex: Votes for a movie on imdb and their rating

**Line Charts**

For temportal trends

**Domain**: Temporal
**Range**: Quantitative

**Tree**
For hierarchy, uni-directional relationships

- Parent-child relations
- Good for multiple tiers of category

**Node-link diagram**

For connection

Relationship between multiple entities
- Good for cyclical links

**Chloropleth (shaded maps)**

For spatial trends

**Domain**: spatial regions
**Range**: quantitative

Best for:
- Regional patterns
- Only one variable
- Relative data (normalize across the population, otherwise you're showing population)

Not good for:
- Subtle differences in data


**Pie Charts**

For hierarchical part-to-whole

Best for:
- When values are around 25%, 30%, or 75%
- 3 or 4 values

Not good for:
- Comparing fine differences
- Multiple totals


**Note**: For best practices on different chart types, reference [Datawrapper Academy](https://academy.datawrapper.de)

### Chart Examples

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

## D3: Going from Data to SVG Shapes

Two intimidating factors to D3:
1. The "enter, update, exit" pattern
2. The sheer size/surface area of the API is so large

Scales and Shapes
- Going from raw data to x/y coordinates and path/shape elements