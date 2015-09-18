{% data src="fcq.clean.json" %}
{% enddata %}

# Warmup

Next, complete the following warmup exercises as a team.

## How many unique subject codes?

{% lodash %}
return (_.compact(_.uniq(_.pluck(data, 'Subject')))).length
{% endlodash %}

They are {{ result }} unique subject codes.

## How many computer science (CSCI) courses?

{% lodash %}
var subjects = _.groupBy(data, 'Subject')

var subjectCounts = _.mapValues(subjects, function(d){
    return d.length
});

return subjectCounts.CSCI
{% endlodash %}

There are {{ result }} computer science courses.

## What is the distribution of the courses across subject codes?

{% lodash %}
var subjects = _.groupBy(data, 'Subject')

return _.mapValues(subjects, function(d){
    return d.length
});
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 100 courses?

{% lodash %}
// TODO: replace with code that computes the actual result
var grps = _.groupBy(data, 'Subject')
var ret = _.pick(_.mapValues(grps, function(d){
    return d.length
}), function(x){
    return x > 100
})
return {"IPHY": 134,"MATH": 232,"MCDB": 117,"PHIL": 160,"PSCI": 117}
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What subset of these subject codes have more than 5000 total enrollments?

{% lodash %}
var subjects = _.groupBy(data, 'Subject')
return _.pick(_.mapValues(subjects, function(d){
    return _.sum(_.pluck(d, "N.ENROLL"))
}), function(x){
    return x > 5000
})
{% endlodash %}

<table>
{% for key, value in result %}
    <tr>
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
{% endfor %}
</table>

## What are the course numbers of the courses Tom (PEI HSIU) Yeh taught?

{% lodash %}
// TODO: replace with code that computes the actual result
// YEH, PEI HSIU
var tomClasses = _.filter(data, function(d) {
    return _.includes(_.pluck(d.Instructors, "name"), "YEH, PEI HSIU")
});

return _.pluck(tomClasses, "Course")
{% endlodash %}

They are {{result}}.
