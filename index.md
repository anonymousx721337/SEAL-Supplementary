---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Overview
---

This Web site provides supplementary material for the paper "SEAL: Integrating Program Analysis and Repository Mining", submitted to ESEC/FSE 2022.
The paper describes an _integrated_ approach that combines low-level program analysis with high-level repository information and allows us to efficiently address software engineering problems that span multiple levels of abstraction, from low-level data flow to high-level organizational information.
On this page, we provide access to the used tools and data and describe how to reproduce our results of the paper.


## Tools

Providing a link to our tool would be author revealing and will be available after the double-blind review.


## Experiments

To demonstrate the wide applicability of {{site.data.constants.approach}} and how it can be used to make existing data-flow analyses commit-aware, we conducted an evaluation consisting of four different study problems.
Here, we provide plots visualizing the results for the three problems that we evaluated on {{site.data.constants.num_projects}} open-source projects.
The raw data used to generate these plots can be found in the replication package linked below.

_**P1:** Which fraction of commits affects central code?_ ([Results]({{ "/plots.html#central-code" | relative_url }}))

_**P2:** Which authors interact via commit interactions and what are the characteristics of the arising socio-technical structure?_ ([Results]({{ "/plots.html#author-interactions" | relative_url }}))

_**P3:** How many authors interact via commit interactions?_ ([Results]({{ "/plots.html#commitauthor-interactions" | relative_url }}))


## Replication Package

The replication package containing the raw data used to generate all plots on this web page and in the paper can be downloaded [here]({{ "/SEAL_replication_package.zip" | relative_url }}).

Instructions on how to use the replication package to reproduce our results depend on the used tools and, therefore, would be author revealing and will be available after the double-blind review.