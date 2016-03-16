# Google Charts
Google chart tools are a set of powerful, simple to use, and free libraries to create simple HTML, SVG visualisations. Due to its simplicity, Google charts are easy to combine into an interactive dashboard with other tools. Configure an extensive set of options to match the look and feel of your website.

## Contents
-Before get started
-Things you need.
-Google Charts Overview
-Tutorial: Word Clouds and Maps.
-Word cloud
-GeoMap
-Assignment

## Before get started
- Things you need.
- In this tutorial you will need basic knowledge of HTML, Javascript and CSS.
- A text editor (Webstorm, Textwrangler, even feel free to use Jsbin).
- A Web browser with internet access to test the visualisation and load the library.
- Google Charts Overview
- Google charts is a big library that includes many tools to customize your visualizations and create personalized dashboards.

For more information please go to: https://developers.google.com/chart/interactive/docs/quick_start

# Tutorial: Word Clouds and Maps.

When using Google charts, maps and word clouds can look very difficult to implement. In this tutorial we are going to use Google Charts to recreate the Dogs Vs Cats visualisation, step by step.

In your editor of preference create a HTML Document and write the basic structure of an HTML document:
```html
<!DOCTYPE html>
<html>
<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>
<body>

</body>
</html>
```


To import the libraries write the following:
```html
<!DOCTYPE html>
<html>

<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>
<body>
</body>
</html>
```


This will indicate to our browser to load the word cloud and basic charts library.
Then, inside the body tag we need to place a few divs to indicate the place where we want to display our charts:

```html
<!DOCTYPE html>
<html>

<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>
<body>

  <h1>Who Is More Popular?</h1>
  <h1>DOGS VS CATS</h1>
  <h2>American Veterinary Medical Association (2013)</h2>

  <div id="wordcloud"></div>
  <div id="map"></div>

</body>
</html>
```

Google Charts work with pure javascript, so now we can start working with the word cloud, inside an <script> tag after the header.
```html
<!DOCTYPE html>
<html>

<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>

<script type="text/javascript">
  google.load('visualization', '1', {
      'packages': ['geochart']
    });
  google.setOnLoadCallback(draw);
</script>

<body>

  <h1>Who Is More Popular?</h1>
  <h1>DOGS VS CATS</h1>
  <h2>American Veterinary Medical Association (2013)</h2>

  <div id="wordcloud"></div>
  <div id="map"></div>

</body>
</html>
```

The google.load is a function that calls the packages we want to use in our visualization.
The google.setOnLoadCallback(draw); will call a function “draw” that we will set to display our charts.
Now we can create our draw function to visualise the charts.
```html
<!DOCTYPE html>
<html>

<head>
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>

<script type="text/javascript">
  google.load('visualization', '1', {
      'packages': ['geochart']
    });
  google.setOnLoadCallback(draw);

  function draw() {
    /*** Here goes our viz code ***/
  }
</script>

<body>

  <h1>Who Is More Popular?</h1>
  <h1>DOGS VS CATS</h1>
  <h2>American Veterinary Medical Association (2013)</h2>

  <div id="wordcloud"></div>
  <div id="map"></div>

</body>
</html>
```


The first thing we want to do is create a variable in javascript to store our data, with Google charts that can be achieved using the function new google.visualization.DataTable(); You can see this as a table where you can add rows and columns. We are going to add two columns and 10 rows for our word cloud.
```javascript
data.addColumn('string', 'Label');
data.addColumn('number', 'Value');
data.addRows(10);
```

The result is the following:
```html
<!DOCTYPE html>
<html>

<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>

<script type="text/javascript">
  google.load('visualization', '1', {
      'packages': ['geochart']
    });
  google.setOnLoadCallback(draw);

  function draw() {
      var data = new google.visualization.DataTable();
      data.addColumn('string', 'Label');
      data.addColumn('number', 'Value');
      data.addRows(10);
  }
</script>

<body>

  <h1>Who Is More Popular?</h1>
  <h1>DOGS VS CATS</h1>
  <h2>American Veterinary Medical Association (2013)</h2>

  <div id="wordcloud"></div>
  <div id="map"></div>

</body>
</html>
```

Now we can add some data to the visualization using the data.setValue(row,column, data);
```javascript
        data.setValue(0, 0, 'Florida');        data.setValue(0, 1, 4138);
        data.setValue(1, 0, 'California');     data.setValue(1, 1, 6865);
        data.setValue(2, 0, 'Texas');          data.setValue(2, 1, 5265);
...
```
Let’s add some data:
```html
<!DOCTYPE html>
<html>

<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>

<script type="text/javascript">
  google.load('visualization', '1', {
      'packages': ['geochart']
    });
  google.setOnLoadCallback(draw);

  function draw() {
      var data = new google.visualization.DataTable();
      data.addColumn('string', 'Label');
      data.addColumn('number', 'Value');
      data.addRows(10);
      data.setValue(0, 0, 'Florida');        data.setValue(0, 1, 4138);
      data.setValue(1, 0, 'California');     data.setValue(1, 1, 6865);
      data.setValue(2, 0, 'Texas');          data.setValue(2, 1, 5265);
      data.setValue(3, 0, 'New York');       data.setValue(3, 1, 3802);
      data.setValue(4, 0, 'Pennsylvania');   data.setValue(4, 1, 2942);
      data.setValue(5, 0, 'North Carolina'); data.setValue(5, 1, 2089);
      data.setValue(6, 0, 'Ohio');           data.setValue(6, 1, 2677);
      data.setValue(7, 0, 'Massachusetts');  data.setValue(7, 1, 1318);
      data.setValue(8, 0, 'Georgia');        data.setValue(8, 1, 2093);
      data.setValue(9, 0, 'Michigan');       data.setValue(9, 1, 2108);
  }
</script>

<body>

  <h1>Who Is More Popular?</h1>
  <h1>DOGS VS CATS</h1>
  <h2>American Veterinary Medical Association (2013)</h2>

  <div id="wordcloud"></div>
  <div id="map"></div>

</body>
</html>
```
Now we have some data but our visualisation is still not working, we need to tell to Google Charts where we want to put this.

```javascript
var wordcloud = document.getElementById('wordcloud');
new TermCloud(wordcloud).draw(data);
```
We can use getElementById to find our word cloud element inside <body> and then we can create the wordcloud using the draw function and passing the data.
```html
<!DOCTYPE html>
<html>

<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>

<script type="text/javascript">
  google.load('visualization', '1', {
      'packages': ['geochart']
    });
  google.setOnLoadCallback(draw);

  function draw() {
      var data = new google.visualization.DataTable();
      data.addColumn('string', 'Label');
      data.addColumn('number', 'Value');
      data.addRows(10);
      data.setValue(0, 0, 'Florida');        data.setValue(0, 1, 4138);
      data.setValue(1, 0, 'California');     data.setValue(1, 1, 6865);
      data.setValue(2, 0, 'Texas');          data.setValue(2, 1, 5265);
      data.setValue(3, 0, 'New York');       data.setValue(3, 1, 3802);
      data.setValue(4, 0, 'Pennsylvania');   data.setValue(4, 1, 2942);
      data.setValue(5, 0, 'North Carolina'); data.setValue(5, 1, 2089);
      data.setValue(6, 0, 'Ohio');           data.setValue(6, 1, 2677);
      data.setValue(7, 0, 'Massachusetts');  data.setValue(7, 1, 1318);
      data.setValue(8, 0, 'Georgia');        data.setValue(8, 1, 2093);
      data.setValue(9, 0, 'Michigan');       data.setValue(9, 1, 2108);
      var wordcloud = document.getElementById('wordcloud');
      new TermCloud(wordcloud).draw(data);
  }
</script>

<body>

  <h1>Who Is More Popular?</h1>
  <h1>DOGS VS CATS</h1>
  <h2>American Veterinary Medical Association (2013)</h2>

  <div id="wordcloud"></div>
  <div id="map"></div>

</body>
</html>
```
Now you should see something like this in your browser:

To add the map to the visualisation we need to use the same approach, in this case with a different component from Google Charts.

First we need to add the data, in this case we will use arrayToDataTable, which basically allow us to add a array of data to our visualisation. In this case we can see our data as two columns, the first is the state (location) and the second is the population (data),
```javascript
      var d = google.visualization.arrayToDataTable([
      ['State', 'Population'],
      ['Texas', -1598],
      ['California', 431],
      ['Kansas', -43],
      ['Iowa', 195]]);
```
Then we can add the data to our visualization:
```html
<!DOCTYPE html>
<html>

<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>

<script type="text/javascript">
  google.load('visualization', '1', {
      'packages': ['geochart']
    });
  google.setOnLoadCallback(draw);

  function draw() {
      var data = new google.visualization.DataTable();
      data.addColumn('string', 'Label');
      data.addColumn('number', 'Value');
      data.addRows(10);
      data.setValue(0, 0, 'Florida');        data.setValue(0, 1, 4138);
      data.setValue(1, 0, 'California');     data.setValue(1, 1, 6865);
      data.setValue(2, 0, 'Texas');          data.setValue(2, 1, 5265);
      data.setValue(3, 0, 'New York');       data.setValue(3, 1, 3802);
      data.setValue(4, 0, 'Pennsylvania');   data.setValue(4, 1, 2942);
      data.setValue(5, 0, 'North Carolina'); data.setValue(5, 1, 2089);
      data.setValue(6, 0, 'Ohio');           data.setValue(6, 1, 2677);
      data.setValue(7, 0, 'Massachusetts');  data.setValue(7, 1, 1318);
      data.setValue(8, 0, 'Georgia');        data.setValue(8, 1, 2093);
      data.setValue(9, 0, 'Michigan');       data.setValue(9, 1, 2108);
      var wordcloud = document.getElementById('wordcloud');
      new TermCloud(wordcloud).draw(data);

      var d = google.visualization.arrayToDataTable([
      ['State', 'Population'],
      ['Texas', -1598],
      ['California', 431],
      ['Kansas', -43],
      ['Iowa', 195],
      ['New York', 1207],
      ['Oregon', 268],
      ['Pennsylvania', 1059],
      ['Colorado',-158],
      ['Virginia',156],
      ['Arizona', -360],
      ['New Mexico', -170],
      ['Utah', 45],
      ['Nevada', 47],
      ['Montana', -5],
      ['Washington',235],
      ['Idaho', 36],
      ['Florida', 165],
      ['Minnesota', 330],
      ['Wisconsin', 372],
      ['Michigan', 384],
      ['North Dakota', 35],
      ['South Dakota', 70],
      ['Wyoming',19],
      ['Oklahoma', -286],
      ['Nebraska', 140],
      ['North Carolina',-298],
      ['South Carolina',-152],
      ['Missisipi', -178],
      ['Georgia',-317],
      ['Kentucky',-182],
      ['Maine', 198],
      ['Vermont',92],
      ['Lousiana', -238],
      ['Alabama', -158],
      ['Tennesse', -408],
      ['Arkansas',-237],
      ['Missouri',-325],
      ['Illinois',88],
      ['Indiana', 293],
      ['West Virginia', -20],
      ['Maryland',762],
      ['Massachusets', 743],
      ['Ohio', 1056],
      ['New Hampshire', 97],
      ['New Jersey', 128],
      ['Connecticut', 289],
      ['Rhode Island', 51]
      ]);

  }
</script>

<body>

  <h1>Who Is More Popular?</h1>
  <h1>DOGS VS CATS</h1>
  <h2>American Veterinary Medical Association (2013)</h2>

  <div id="wordcloud"></div>
  <div id="map"></div>

</body>
</html>
```



Google Charts allows to add a set of options to every chart, this options allow you to manipulate the color, the size of your chart, display mode and many other things.  To know and understand how options work in each visualisation please check the documentation.
```javascript
     var opts = {
        region: 'US',
        displayMode: 'regions',
        resolution: 'provinces',
        width: 640,
        height: 380,
        colors: ['#0a521e', '#3c8d3d', '#bebebe', '#1f67a7', '#1c335c']
      };
```
Let’s add this options to our code.
```html
<!DOCTYPE html>
<html>

<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>

<script type="text/javascript">
  google.load('visualization', '1', {
      'packages': ['geochart']
    });
  google.setOnLoadCallback(draw);

  function draw() {
      var data = new google.visualization.DataTable();
      data.addColumn('string', 'Label');
      data.addColumn('number', 'Value');
      data.addRows(10);
      data.setValue(0, 0, 'Florida');        data.setValue(0, 1, 4138);
      data.setValue(1, 0, 'California');     data.setValue(1, 1, 6865);
      data.setValue(2, 0, 'Texas');          data.setValue(2, 1, 5265);
      data.setValue(3, 0, 'New York');       data.setValue(3, 1, 3802);
      data.setValue(4, 0, 'Pennsylvania');   data.setValue(4, 1, 2942);
      data.setValue(5, 0, 'North Carolina'); data.setValue(5, 1, 2089);
      data.setValue(6, 0, 'Ohio');           data.setValue(6, 1, 2677);
      data.setValue(7, 0, 'Massachusetts');  data.setValue(7, 1, 1318);
      data.setValue(8, 0, 'Georgia');        data.setValue(8, 1, 2093);
      data.setValue(9, 0, 'Michigan');       data.setValue(9, 1, 2108);
      var wordcloud = document.getElementById('wordcloud');
      new TermCloud(wordcloud).draw(data);

      var d = google.visualization.arrayToDataTable([
      ['State', 'Population'],
      ['Texas', -1598],
      ['California', 431],
      ['Kansas', -43],
      ['Iowa', 195],
      ['New York', 1207],
      ['Oregon', 268],
      ['Pennsylvania', 1059],
      ['Colorado',-158],
      ['Virginia',156],
      ['Arizona', -360],
      ['New Mexico', -170],
      ['Utah', 45],
      ['Nevada', 47],
      ['Montana', -5],
      ['Washington',235],
      ['Idaho', 36],
      ['Florida', 165],
      ['Minnesota', 330],
      ['Wisconsin', 372],
      ['Michigan', 384],
      ['North Dakota', 35],
      ['South Dakota', 70],
      ['Wyoming',19],
      ['Oklahoma', -286],
      ['Nebraska', 140],
      ['North Carolina',-298],
      ['South Carolina',-152],
      ['Missisipi', -178],
      ['Georgia',-317],
      ['Kentucky',-182],
      ['Maine', 198],
      ['Vermont',92],
      ['Lousiana', -238],
      ['Alabama', -158],
      ['Tennesse', -408],
      ['Arkansas',-237],
      ['Missouri',-325],
      ['Illinois',88],
      ['Indiana', 293],
      ['West Virginia', -20],
      ['Maryland',762],
      ['Massachusets', 743],
      ['Ohio', 1056],
      ['New Hampshire', 97],
      ['New Jersey', 128],
      ['Connecticut', 289],
      ['Rhode Island', 51]
      ]);

      var opts = {
        region: 'US',
        displayMode: 'regions',
        resolution: 'provinces',
        width: 640,
        height: 380,
        colors: ['#0a521e', '#3c8d3d', '#bebebe', '#1f67a7', '#1c335c']
      };

  }
</script>

<body>

  <h1>Who Is More Popular?</h1>
  <h1>DOGS VS CATS</h1>
  <h2>American Veterinary Medical Association (2013)</h2>

  <div id="wordcloud"></div>
  <div id="map"></div>

</body>
</html>
```


Now the only thing we need to do is to tell to google charts where we want to visualize our map. Again we use the draw function.

```html
<!DOCTYPE html>
<html>

<head>
<link rel="stylesheet" type="text/css" href="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.css" />
  <script type="text/javascript" src="http://visapi-gadgets.googlecode.com/svn/trunk/termcloud/tc.js"></script>
  <script type="text/javascript" src="http://www.google.com/jsapi"></script>
</head>

<script type="text/javascript">
  google.load('visualization', '1', {
      'packages': ['geochart']
    });
  google.setOnLoadCallback(draw);

  function draw() {
      var data = new google.visualization.DataTable();
      data.addColumn('string', 'Label');
      data.addColumn('number', 'Value');
      data.addRows(10);
      data.setValue(0, 0, 'Florida');        data.setValue(0, 1, 4138);
      data.setValue(1, 0, 'California');     data.setValue(1, 1, 6865);
      data.setValue(2, 0, 'Texas');          data.setValue(2, 1, 5265);
      data.setValue(3, 0, 'New York');       data.setValue(3, 1, 3802);
      data.setValue(4, 0, 'Pennsylvania');   data.setValue(4, 1, 2942);
      data.setValue(5, 0, 'North Carolina'); data.setValue(5, 1, 2089);
      data.setValue(6, 0, 'Ohio');           data.setValue(6, 1, 2677);
      data.setValue(7, 0, 'Massachusetts');  data.setValue(7, 1, 1318);
      data.setValue(8, 0, 'Georgia');        data.setValue(8, 1, 2093);
      data.setValue(9, 0, 'Michigan');       data.setValue(9, 1, 2108);
      var wordcloud = document.getElementById('wordcloud');
      new TermCloud(wordcloud).draw(data);

      var d = google.visualization.arrayToDataTable([
      ['State', 'Population'],
      ['Texas', -1598],
      ['California', 431],
      ['Kansas', -43],
      ['Iowa', 195],
      ['New York', 1207],
      ['Oregon', 268],
      ['Pennsylvania', 1059],
      ['Colorado',-158],
      ['Virginia',156],
      ['Arizona', -360],
      ['New Mexico', -170],
      ['Utah', 45],
      ['Nevada', 47],
      ['Montana', -5],
      ['Washington',235],
      ['Idaho', 36],
      ['Florida', 165],
      ['Minnesota', 330],
      ['Wisconsin', 372],
      ['Michigan', 384],
      ['North Dakota', 35],
      ['South Dakota', 70],
      ['Wyoming',19],
      ['Oklahoma', -286],
      ['Nebraska', 140],
      ['North Carolina',-298],
      ['South Carolina',-152],
      ['Missisipi', -178],
      ['Georgia',-317],
      ['Kentucky',-182],
      ['Maine', 198],
      ['Vermont',92],
      ['Lousiana', -238],
      ['Alabama', -158],
      ['Tennesse', -408],
      ['Arkansas',-237],
      ['Missouri',-325],
      ['Illinois',88],
      ['Indiana', 293],
      ['West Virginia', -20],
      ['Maryland',762],
      ['Massachusets', 743],
      ['Ohio', 1056],
      ['New Hampshire', 97],
      ['New Jersey', 128],
      ['Connecticut', 289],
      ['Rhode Island', 51]
      ]);

      var opts = {
        region: 'US',
        displayMode: 'regions',
        resolution: 'provinces',
        width: 640,
        height: 380,
        colors: ['#0a521e', '#3c8d3d', '#bebebe', '#1f67a7', '#1c335c']
      };

      new google.visualization.GeoChart(document.getElementById('map')).draw(d, opts);

  }
</script>

<body>

  <h1>Who Is More Popular?</h1>
  <h1>DOGS VS CATS</h1>
  <h2>American Veterinary Medical Association (2013)</h2>

  <div id="wordcloud"></div>
  <div id="map"></div>

</body>
</html>
```


Now you should see your map and word cloud.



# 3. Assignment
Now we have an HTML/JavaScript version of the Dogs Vs Cats visualisation.
Finish the dashboard using CSS and HTML.
Here you can find a solution for this tutorial: http://output.jsbin.com/nuxexa,  feel free to compare it with yours and customize your HTML/CSS as you wish.

More Examples
Barcharts: http://jsbin.com/howefe/1/edit?html,output
Maps: http://jsbin.com/nibosi/1/edit?html,output
Treemaps: http://jsbin.com/darozi/edit?html,output
Word Clouds: http://jsbin.com/nifohay/2/edit?html,output
Bubble Charts: http://jsbin.com/xobemo/edit?html,output

Other Javascript libraries
ChartJs: http://www.chartjs.org/
D3Js: https://d3js.org/
