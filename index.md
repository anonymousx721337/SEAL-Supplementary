---
layout: default
title: SEAL
---

This website provides supplementary material for the paper "SEAL: Integrating Program Analysis and Repository Mining", submitted to TOSEM.
The paper describes an _integrated_ approach that combines low-level program analysis with high-level repository information and allows us to efficiently address software engineering problems that span multiple levels of abstraction, from low-level data flow to high-level organizational information.
On this page, we provide access to the used tools and data and describe how to reproduce our results of the paper.


## Tools

SEAL is implemented in a tool called [VaRA](https://vara.readthedocs.io/en/vara-dev/research_tool_docs/vara/vara.html) which is [available on github](https://github.com/se-sic/VaRA).
A detailed description on how to reproduce our data using VaRA can be found [here]({{ "/reproducing.html" | relative_url }}).
We also provide the raw data in our [replication package]({{ "/index.html#replication-package" | relative_url }}) alongside with instructions how to generate the plots on this website below.


## Experiments

To demonstrate the wide applicability of {{site.data.constants.approach}} and how it can be used to make existing data-flow analyses commit-aware, we conducted an evaluation consisting of four different study problems.
The links lead to plots visualizing the results for the three problems that we evaluated on {{site.data.constants.num_projects}} open-source projects.
The raw data used to generate these plots can be found in the replication package linked below.

_**P1:** Which fraction of commits affects central code?_ ([Results]({{ "/plots.html#central-code" | relative_url }}))

_**P2:** Which authors interact via commit interactions and what are the characteristics of the arising socio-technical structure?_ ([Results]({{ "/plots.html#author-interactions" | relative_url }}))

_**P3:** How many authors interact via commit interactions?_ ([Results]({{ "/plots.html#commitauthor-interactions" | relative_url }}))


## Replication Package

The replication package containing the raw data used to generate all plots on this web page and in the paper can be downloaded by clicking [here]({{ "/SEAL_replication_package.tar.xz" | relative_url }}).

To reproduce the plots from this website, we first need to install the [VaRA-Tool-Suite](https://vara.readthedocs.io/en/vara-dev/), an experimentation framework designed to allow easy reproduction of research results.
The tool suite is also open-source and [available on github](https://github.com/se-sic/VaRA-Tool-Suite).

The VaRA-Tool-Suite can be installed as follows:

1. First, we need to install some system dependencies (example for Debian 11)

   ```bash
   sudo apt install python3-dev python3-venv python3-tk python3-psutil psutils python3-pip ruby curl time libyaml-dev git graphviz-dev
   ```
   
2. Next, we create and activate a python virtual environment (optional)

   ```bash
   # create virtualenv
   python3 -m venv /where/you/want/your/virtualenv/to/live
   # activate virtualenv
   source /path/to/virtualenv/bin/activate
   ```
   
3. We can now simply install varats via pip

   ```bash
   # update pip
   pip3 install --upgrade pip
   # install wheel (needed by some dependencies)
   pip3 install wheel
   # install VaRA-Tool-Suite
   pip3 install varats==11.1.4
   ```
   
4. Then, we need to prepare a working directory.

   ```bash
   # create working directory, for example in ~/varats
   export VARATS_ROOT='~/varats'
   mkdir -p $VARATS_ROOT
   cd $VARATS_ROOT
   # create config files and initialize working directory
   vara-gen-bbconfig
   ```
   
5. Extract the replication package to the working directory and select it

   ```bash
   # download the replication package
   wget https://anonymousx721337.github.io/SEAL-Supplementary/SEAL_replication_package.zip
   # extract replication backage
   tar -xvf SEAL_replication_package.tar.xz
   # select replication package (enter number next to "SEAL" in list)
   vara-pc select
   ```
   
6. Reproduce plots (this step can take some time)

   ```bash
   vara-art generate
   ```
   
   The plots are written to ```$VARATS_ROOT/artefacts/seal```.

For more information on the tool suite and its capabilities, we refer to its [documentation](https://vara.readthedocs.io/en/vara-dev/#vara-ts-docs).
