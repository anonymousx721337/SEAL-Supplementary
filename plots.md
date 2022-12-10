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

The metrics for bison, grep, and gzip include submodules.

<br/>


## Central Code

These plots relate the number of insertions of each commit to its node degree in the commit interaction graph. 
The margins show kernel density estimations for the variables.
The horizontal and vertical lines mark the 80- or 20-percentile of their variable, meaning that small commits that modify central code fall into the upper-left quadrant.
The red crosses highlight commit 5e4b182 of htop and commit 348e694 of opus that discussed as examples in section 5 in the paper.

> You can click on an image to view a larger version.

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

The following plots visualize changes between CI-based and file-based author interactions.
Each column represents an individual author.
Orange boxes depict links to other authors that are produced by the file-based approach but are not inferred by CI, as there exists no data-flow indicating a connection between the two authors.
Blue boxes depict additional links that CI discovers through data-flow information that a file-based approach does not.

<div class="box">
{% for project in site.data.projects %}
<div class="column">
<b>{{project.name}}</b>
{%- capture link -%}/images/{{-project.name-}}_0_aig_file_vs_blame_authors.svg{%- endcapture -%}
<a href="{{ link | relative_url }}"><img alt="{{-project.name-}}" src="{{ link | relative_url }}"/></a>
</div>
{% endfor %}
</div>

<br/>

Here, we can see changes between CI-based and call-graph-based author interactions. 
Again, each column represents an individual author.
Orange boxes depict links to other authors that are produced by the call-graph-based approach, but not by the CI based approach, as there is no data flow indicating a connection between the two authors.
Blue boxes depict additional links that CI discovers through data-flow information that a call-graph-based approach does not.

<div class="box">
{% for project in site.data.projects %}
<div class="column">
<b>{{project.name}}</b>
{%- capture link -%}/images/{{-project.name-}}_0_aig_callgraph_vs_blame_authors.svg{%- endcapture -%}
<a href="{{ link | relative_url }}"><img alt="{{-project.name-}}" src="{{ link | relative_url }}"/></a>
</div>
{% endfor %}
</div>

<br/>


## Commit--Author Interactions

The following plot shows for each commit its number of interacting authors normalized by the number of distinct authors per project that have, at least, one commit participating in a commit interaction.
That is, it visualizes how many other authors are affected by a commit.

<a href="{{ "/images/caig_box.svg" | relative_url }}"><img id="image" alt="commit--author interactions" src="{{ "/images/caig_box.svg" | relative_url }}"/></a>


[comment]: <> (CSS for plot matrix)

<style media="screen">
.box {
  display: flex;
  flex-wrap: wrap;
  padding: 0 4px;
}

.column {
  border-bottom:1px solid gray;
  flex: 20%;
  max-width: 20%;
  min-width: 20%;
  padding: 4px 4px;
  margin-bottom: 1ex;
  text-align: center;
}

.column img {
  margin-bottom: 8px;
  vertical-align: middle;
  width: 100%;
}
</style>
