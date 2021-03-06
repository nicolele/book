{% data src="fcq.clean.json" %}
{% enddata %}

# Report

As a class, we brainstormed and came up with a long list of further questions we
can ask based on the FCQ data. Out of these questions, our team chose to tackle on
the following questions. Each member on our team is reponsible for one question.

# What department has the lowest average GPA? by Nicole Woytarowicz

{% lodash %}
var subjects = _.groupBy(data, 'Subject')
var departments = _.pick(_.mapValues(subjects, function(d){
    return (_.sum(_.pluck(d, "AVG_GRD")))/(d.length)
}), function(x){
    return x > 0
})

var worst = _.min(departments)

return {Department: (_.invert(departments))[worst], Average_GPA: worst}
{% endlodash %}

{{ result | json }}

# Which classes(with specific professors) damaged the most students (sort by:D + DF + F + WDRAW rating)? by Denis Kazakov

{% lodash %}
var clean = _.filter(data, function(n){
    return n.PCT.D != ""
})

var map = _.map(clean, function(n){
    return {course: n.CourseTitle, ratio: n.PCT.C + n.PCT.D + n.PCT.F, name: _.pluck(n.Instructors, "name")}
})

return _.sortBy(map, function(n){
    return n.ratio
}).reverse()
{% endlodash %}

<table>
{% for n in result %}
<tr>
<td>{{n.course}}</td>
<td>{{n.ratio}}</td>
<td>{{n.name}}</td>
</tr>
{% endfor %}
</table>

# Which classes have the maximum Hours spent (13-15) per week? by Parker Illig

{% lodash %}
var result = _.groupBy(data, function(d){
var dept = d.Subject
var num = d.Course
var combine = dept +  " " + num    
return combine
})
var classes = _.mapValues(result, function(d){
var wk = _.first(_.pluck(d, 'Workload.Hrs_Wk'))
return _.includes(wk, '13-15')
})
return _.pick(classes, function(x){
return x==true
})
{% endlodash %}

Here's a table for the results
<table>
{% for key, value in result %}
<tr>
<td>{{key}}</td>
</tr>
{% endfor %}
</table>


# (Question 4) by (Name)

{% lodash %}
return "[answer]"
{% endlodash %}

# What should my major be if I want a high GPA? by Caleb Hsu

{% lodash %}
var subjects = _.groupBy(data, 'Subject_Label')

var avgA = _.mapValues(subjects, function(s) {
return _.sum(_.pluck(s, 'PCT.A')) / s.length
})

var highest =  _.last(_.sortBy(_.pairs(avgA), function(d) {
return d[1]
}))

return highest[0]
{% endlodash %}

I should take classes in the {{result}} department if I want to boost my GPA.