google-charts-node
---
[![npm](https://img.shields.io/npm/v/google-charts-node)](https://www.npmjs.com/package/google-charts-node)

This package allows you to render Google Charts on the server as PNG images.

It is based on the [Google Visualization API](https://developers.google.com/chart/interactive/docs/reference) and is made possible through the use of [puppeteer](https://github.com/puppeteer/puppeteer), which uses the Chromium browser for "headless" rendering.

For a more detailed walkthrough, see [Server-side image rendering for Google Charts](https://quickchart.io/documentation/google-charts-image-server/) on QuickChart.

## Installation

This project is [available on NPM](https://www.npmjs.com/package/google-charts-node).

```
npm install google-charts-node
```

## Example

```js
const GoogleChartsNode = require('google-charts-node');

// Define your chart drawing function
function drawChart() {
  const data = google.visualization.arrayToDataTable([
    ['City', '2010 Population',],
    ['New York City, NY', 8175000],
    ['Los Angeles, CA', 3792000],
    ['Chicago, IL', 2695000],
    ['Houston, TX', 2099000],
    ['Philadelphia, PA', 1526000]
  ]);

  const options = {
    title: 'Population of Largest U.S. Cities',
    chartArea: {width: '50%'},
    hAxis: {
      title: 'Total Population',
      minValue: 0
    },
    vAxis: {
      title: 'City'
    }
  };

  const chart = new google.visualization.BarChart(container);
  chart.draw(data, options);
}

// Render the chart to image
const image = await GoogleChartsNode.render(drawChart, {
  width: 400,
  height: 300,
});
```

This produces the following image:

![Google Charts Image](https://i.imgur.com/ABS8FSR.png)

The only requirements of your `drawChart` function are that you must:
- Define a `chart` variable or return your chart.
- Use the provided `container` variable to render your chart.

## Usage

### render(drawChartFunction, options) -> Buffer

The library exposes a single function, render.

**drawChartFunction** is a Function or Javascript string that is evaluated in order to draw the chart.  You should put your regular `drawChart` Google Charts function here.

**options** is a dictionary containing some settings and parameters:
- **width**: Width of chart canvas (default `100%`)
- **height**: Height of chart canvas (default `100%`)
- **packages**: Array of Google Charts packages to import (default `['corechart']`)
- **mapsApiKey**: Google Maps API key (used only for geochart and map charts)

## More examples

See the `examples/` directory for more examples of different charts.
