---
layout: default
title: Results
---

## Subject Projects

Our experiments were run on the following open-source C/C++ projects:

|      | Domain | LOC | Commits | Authors | Revision |
|------|--------|----:|--------:|--------:|----------|
{% for project in site.data.projects -%}
| **{{project.name}}** | {{project.domain}} | {{project.loc}} | {{project.commits}} | {{project.authors}} | {{project.revision}} |
{% endfor %}

<br/>


## Central Code

These plots relate the number of insertions of each commit to its node degree in the commit interaction graph. 
The margins show kernel density estimations for the variables.
The horizontal and vertical lines mark the 80- or 20-percentile of their variable, meaning that small commits that modify central code fall into the upper-left quadrant.


**Example:**
In the paper, we discuss an example for such a commit from _opus_.
As another example, consider commit `a1f7f28` from _htop_.
This commit has the third-highest node degree while inserting only a moderate number of 75  lines in 2 files.
It introduces a set of functions that are intended to replace C's memory allocation functions.
However, these functions are not used anywhere at this point.
Only in the subsequent commit `b54d2dd` the original function calls are replaced with the new substitutes leading to the high node degree of the commit introducing the functions.
This commit also has a high node degree comparable to its predecessor, but it is almost twice as large, and it touches 42 different files.
This observation matches the scenario described in Figure 6 in the paper that we use to motivate our notion of central code.

<div class="box">
{% for project in site.data.projects %}
<div class="column">
<b>{{project.name}}</b>
{%- capture link -%}/images/{{-project.name-}}_0_central_code_scatter.svg{%- endcapture -%}
<a href="{{ link | relative_url }}"><img alt="{{-project.name-}}" src="{{ link | relative_url }}"/></a>
</div>
{% endfor %}
</div>

<br/>


## Author Interactions

These plots relate the number of commits of each author to the number of other authors they interact with. 
The margins show kernel density estimations for the variables.
Most projects have a small number of authors that are responsible for most commits.
However, there are also authors with only few commits that still interact with many other authors.

<div class="box">
{% for project in site.data.projects %}
<div class="column">
<b>{{project.name}}</b>
{%- capture link -%}/images/{{-project.name-}}_0_author_interaction_scatter.svg{%- endcapture -%}
<a href="{{ link | relative_url }}"><img alt="{{-project.name-}}" src="{{ link | relative_url }}"/></a>
</div>
{% endfor %}
</div>

<br/>


The following plot visualizes for each author the number of interacting authors that can _not_ be identified using purely file-based or function-based approaches, but only via data flow.

<a href="{{ "/images/aig_file_vs_blame_authors_box.svg" | relative_url }}"><img id="image" alt="file-based vs. blame bnteractions" src="{{ "/images/aig_file_vs_blame_authors_box.svg" | relative_url }}"/></a>


## Commit--Author Interactions

The following plot shows for each commit its number of interacting authors normalized by the number of distinct authors per project that have, at least, one commit participating in a commit interaction.
That is, it visualizes how many other authors are affected by a commit.

<a href="{{ "/images/caig_box.svg" | relative_url }}"><img id="image" alt="commit--author interactions" src="{{ "/images/caig_box.svg" | relative_url }}"/></a>


[comment]: <> (CSS for plot matrix)

<style type="text/css" media="screen">
body {
  font-family: Arial, sans-serif;
}
a {
  text-decoration: none
}
.box {
  display: flex;
  flex-wrap: wrap;
  padding: 0 4px;
}

.column {
  flex: 18%;
  max-width: 18%;
  min-width: 18%;
  padding: 0 4px;
  text-align: center;
}

.column img {
  /*margin-top: 8px;*/
  margin-bottom: 8px;
  vertical-align: middle;
  width: 100%;
}

#image {
    width: 100%;
}
</style>