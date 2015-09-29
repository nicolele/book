# Report
{% data src="birdstrike.json" %}{% enddata %}


Use only Javascript and SVG to produce a data analysis / visualization report.

# Authors

This report is prepared by
* [Nicole Woytarowicz](https://github.com/nicolele)
* [Satchel Spencer](https://github.com/satchelspencer)
* [Patrick Murphy](https://github.com/johnmurph27)

<a name="top"/>
<div id="autonav"></div>

# How does bird size relate to the amount of damage?

{% viz %}

{% title %}

How does bird size relate to the cost of the incident?

{% solution %}

var sizeCosts = _(data).map(function(incident){
return {
cost : parseInt(incident['Cost: Total $'].toString().replace(',', '')),
size : incident['Wildlife: Size']
}
}).filter(function(incident){
return incident.cost && incident.size;
}).value();

var maxCost = _(sizeCosts).pluck('cost').max();
var sizes = ['Small', 'Medium', 'Large'];

var result = _.map(sizeCosts, function(sizeCost){
return template({
y : (sizes.indexOf(sizeCost.size)*20)+10,
x : (sizeCost.cost*(620/maxCost))+80
});
})

_.each(sizes, function(size, i){
result.push("<text y='"+((i*20)+15)+"'>"+size+"</text>"); 
});

return result.join('\n\n');

{% template %}
<circle cx="${x}" cy="${y}" r="5" style="fill:rgba(0,0,0,0.5);"/>
{% endviz %}

# What month has the most bird strikes?

{% viz %}

{% title %}

What month has the most bird strikes?
{% solution %}
var months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'November']
var dates = _.groupBy(data, function(item){
return item['FlightDate'].split('/')[0] })


console.log(dates)
var counts = _(dates).map(function(group, name){
return {
name : months[name-1]+ ' ' + group.length,
count : group.length
};
}).value();

var max = _(counts).pluck('count').max();
function computeWidth(d, i) {
return d.count*(500/max);
}

var result = _.map(counts, function(count, i){
return template({
y : 25*i,
width : count.count*(600/max),
name : count.name
});
})

return result.join('')


{% template %}

<rect y="${y}" height="20" width="${width}" style="fill:red;"/>
<text y="${y+15}" x="${width+10}">${name}</text>

{% endviz %}




# How much of the collected wildlife was sent to the Smithsonian?
{% viz %}

{% title %}

How much of the collected wildlife was sent to the Smithsonian?

{% solution %}
var collected = _.filter(data, function(d){
    return d["Remains of wildlife collected?"] == "TRUE"
})

var smiths = _.groupBy(collected, function(d) {
    return d["Remains of wildlife sent to Smithsonian"]
});

// TODO: modify the code below to produce a nice vertical bar charts

function computeX(d, i) {
return 0
}

function computeHeightCollected(d, i) {
return _.size(collected)
}

function computeHeight(d, i) {
return _.size(smiths)*2
}

function computeColor(d, i) {
return 'red'
}

function computeSentColor(d, i) {
return 'blue'
}

var viz = _.map(smiths, function(d, i){
return {
    x: computeX(d, i),
    height: computeHeight(d, i),
    collectedColor: computeColor(d, i),
    collectedHeight: computeHeightCollected(d, i),
    sentColor: computeSentColor(d, i)
}
})
console.log(viz)

var result = _.map(viz, function(d){
    return template({d: d})
})
return result.join('\n')

{% template %}

<rect
    x="0"
    width="20"
    height="${d.collectedHeight}"
    style="fill:${d.collectedColor};
    stroke-width:1;
    stroke:rgb(0,0,0)" />


<rect
    x="0"
    width="20"
    height="${d.height}"
    style="fill:${d.sentColor};
    stroke-width:1;
    stroke:rgb(0,0,0)" />

{% endviz %}
