{% import '../../hackathons/classmates/data.html' as data %}

# Report

There are {{ data.comments.length }} students who gave a self-introduction. As a
class, we brainstormed and came up with a long list of further questions we can
ask based on this data. Our team chose to tackle on the following:

# Who is not a Computer Science major?

{% lodash %}
var comments = _.pluck(data.comments, 'body')

var csComments = _.reject(comments, function(n) {
return _.includes(n.toLowerCase(), "computer science") || _.includes(n.toLowerCase(), "cs")
});

return _.map(csComments, function(comment) {
var names = comment.split('\r\n')[0]
return names.split(':')[1]
});
{% endlodash %}

{{result}} are all not Computer Science majors.


# How many people responded before the first day of class (August 24th)?

{% lodash %}
var dates = _.pluck(data.comments, 'created_at')

var commitTimes = _.map(dates, function(n) {
var date = n.split('T')[0]
return date.split('-')[2]
});

return (_.filter(commitTimes, function(n) {
return n<24
})).length

{% endlodash %}

{{result}} people responded before the first class.


# How many people are Applied Math majors?

{% lodash %}
var comments = _.pluck(data.comments, 'body')

var appm = _.filter(comments, function(n) {
return _.includes(n.toLowerCase(), "applied math") || _.includes(n.toLowerCase(), "appm")
});

return _.map(appm, function(comment) {
var names = comment.split('\r\n')[0]
return names.split(':')[1]
});
{% endlodash %}

{{result}} are Applied Math majors.

# How many people responded after class began on the 24th?

{% lodash %}
var dates = _.pluck(data.comments, 'created_at')

var dateFilter = _.filter(dates, function(n) {
return _.includes(n, "2015-08-24")
});

var commitTimes = _.map(dateFilter, function(n) {
var date = n.split('T')[1]
return date.split(':')[0]
});


return (_.filter(commitTimes, function(n) {
return n>16
})).length 
{% endlodash %}

{{result}} people responded after the beginning of the first class.