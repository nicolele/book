# Q: Which programming language is the top favorite among the students in our class?

## Data

* Manually gather data and make a table in Markdown


| Language | # of Students |
| -- | -- |
| Python | 7 |
| JavaScript | 3 |
| Ruby | 1 |
| C | 3 |
| Haskell | 1 |
| C++ | 3 |


## Answer

Python

## Visualization

* Create a barchart using SVG

{% svg %}

<!-- extend this into a barchart -->
<rect x="0" width="20" height="70" style="fill:rgb(0,0,0);stroke-width:0;stroke:rgb(0,0,0)"/>

<text x="0" y="80" font-family="sans-serif" font-size="10px">Python</text>

<rect x="35" width="20" height="30" style="fill:rgb(0,0,0);stroke-width:0;stroke:rgb(0,0,0)"/>

<text x="35" y="40" font-family="sans-serif" font-size="10px">JS</text>

<rect x="70" width="20" height="10" style="fill:rgb(0,0,0);stroke-width:0;stroke:rgb(0,0,0)"/>

<text x="70" y="20" font-family="sans-serif" font-size="10px">Ruby</text>

<rect x="105" width="20" height="30" style="fill:rgb(0,0,0);stroke-width:0;stroke:rgb(0,0,0)"/>

<text x="105" y="40" font-family="sans-serif" font-size="10px">C</text>

<rect x="140" width="20" height="10" style="fill:rgb(0,0,0);stroke-width:0;stroke:rgb(0,0,0)"/>

<text x="140" y="20" font-family="sans-serif" font-size="10px">Haskell</text>

<rect x="175" width="20" height="30" style="fill:rgb(0,0,0);stroke-width:0;stroke:rgb(0,0,0)"/>

<text x="175" y="40" font-family="sans-serif" font-size="10px">C++</text>

{% endsvg %}
