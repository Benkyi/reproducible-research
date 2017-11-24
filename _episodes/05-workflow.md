---
layout: episode
title: "Workflow management and tracking tools"
teaching: 10
exercises: 10
questions:
  - "Are there any tools out there for managing and tracking projects based on numerical simulations or analysis?"
  - "How can such a tool be adopted to your workflows?"
objectives:
  - "Get familiar with the Sumatra tool for managing numerical simulations and analysis"
  - "Get familiar with the Snakemake tool for managing numerical simulations and analysis"
   
---

## Scientific workflows

The simplest computerized scientific workflows are scripts that call in data, programs, and other inputs and produce outputs that might include visualizations and analytical results. These may be implemented in programs such as R or MATLAB, or using a scripting language such as Python or Perl with a command-line interface.
There are many motives for differentiating scientific workflows from traditional business process workflows. 
These include:
* providing an easy-to-use environment for individual application scientists themselves to create their own workflows
* providing interactive tools for the scientists enabling them to execute their workflows and view their results in real-time
* simplifying the process of sharing and reusing workflows between the scientists.
* enabling scientists to track the provenance of the workflow execution results and the workflow creation steps.  
[From Wikipedia](https://en.wikipedia.org/wiki/Scientific_workflow_system)

## Provenance of data


## Directed acyclic graphs (DAGs)
Pipelines, ...


## What are workflow management and tracking systems?

### What tools are out there?

<!-- 
R, SAS, Matlab, as scripted analysis environments
Kepler, Taverna, VisTrails, and other dedicated workflow systems
Bash scripts
Python, perl, and other scripting languages
Pegasus, Condor, and related batch computing workflow systems
Make (but far less common, except in its traditional use in building code for models)
-->

- [Sumatra](http://sumatra.readthedocs.io/en/0.7.4/)
- [Snakemake](http://snakemake.readthedocs.io/en/stable/)
- [Ruffus](https://code.google.com/archive/p/ruffus/)
- [AiiDA](http://www.aiida.net/) (electronic structure calculations)
- [Kepler](https://kepler-project.org/)
- [Galaxy](https://galaxyproject.org/) (biology)
- [VisTrails](https://www.vistrails.org/index.php/Main_Page) (data exploration and visualization)
- [Pegasus](https://pegasus.isi.edu/)
- [HTCondor](https://research.cs.wisc.edu/htcondor/index.html)
- [make](https://www.gnu.org/software/make/)


### Sumatra
Sumatra: automated tracking of scientific computations
Sumatra is a tool for managing and tracking projects based on numerical simulation and/or analysis, with the 
aim of supporting reproducible research. It can be thought of as an automated electronic lab notebook for computational projects.

[adapted from https://github.com/yoavram/smt_test]
Sumatra manages your computational experiments: simulations, calculations, analysis and any program your going 
to be running many times to create lots of data. It keeps track of what exactly you ran, in terms of source code, 
parameters, environment configuration, dependencies, etc. It also stores when you ran it, how long it took, 
what was the input and output results. It lets you easily repeat configurations to be run again. 
And it let's you browse a library of your activity via your browser.

### Snakemake


## Best practices

- Make everything a project
- Use consistent directory structure:
```
.
|-- data
|   |-- README.md
|   |-- dataset.csv
|-- man
|   |-- manuscript.tex
|-- results
|   |-- table.csv
|   |-- fig.png
|-- src
|   |-- main.py
|   |-- calculate_stuff.py
|   |-- test_calculate_stuff.py
```

<!-- 
```
project
│   README.md
│   Makefile
│   requirements.txt
└───raw_data
│   │   README.md
│   └───experiment1
│   │   │   data.csv
│   └───experiment2
│       │   data.csv
└───processed_data
└───source
    │   main.py
    │   analysis.py
└───results
```
-->

## Exercise: Sumatra

## Exercise: Snakemake

