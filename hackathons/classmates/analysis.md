# Analysis

{% import './data.html' as data %}

After completing the warmup exercises, your task is to do four more slightly
more challenges analyses.

## How many students like sushi as their favorite food?

{% lodash %}

var comments = _.pluck(data.comments, 'body')

var sushiComments = _.filter(comments, function(n) {
    return _.includes(n.toLowerCase(), "sushi")
});


return _.size(sushiComments)

{% endlodash %}

The answer is {{result}}.

## Who are the students liking Python the most?

{% lodash %}
var comments = _.pluck(data.comments, 'body')

var pythonComments = _.filter(comments, function(n) {
    return _.includes(n.toLowerCase(), "python")
});

return _.map(pythonComments, function(comment) {
    var names = comment.split('\r\n')[0]
    return names.split(':')[1]
});

{% endlodash %}

Their names are {{result}}.

## Are there more Javascript lovers or Java lovers?

{% lodash %}
var comments = _.pluck(data.comments, 'body')

var allJavas = _.filter(comments, function(n) {
    return _.includes(n.toLowerCase(), "java")
});

var javaComments = _.reject(allJavas, function(n) {
    return _.includes(n.toLowerCase(), "script")
});

var jsComments = _.filter(allJavas, function(n) {
    return _.includes(n.toLowerCase(), "javascript")
});


if (_.size(jsComments) > _.size(javaComments)) {
    return "JavaScript";
}
else if (_.size(jsComments) < _.size(javaComments)) {
    return "Java";
}
else {
    return "They're equal";
}

{% endlodash %}

The answer is {{result}}.

## Who like the same food as `kjblakemore`?

{% lodash %}
var comments = _.pluck(data.comments, 'body')
var kjblakemore = _.pluck((_.pluck(data.comments, 'user')), 'login')

console.log(kjblakemore)

return "nothing"
{% endlodash %}

Their names are {{result}}.
