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
  - "Get familiar with the common workflog language (CWL) for managing numerical simulations and analysis"
   
---

## Scientific workflows

- Home-made workflows: scripts that call in data, programs and other inputs and produce outputs.
- Some best practices
  - make everything a project
  - use consistent directory structure
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

- Many unified frameworks exist for managing scientific workflows
  - provide user-friendly environment to create workflows
  - provide interactive tools to execute workflows and view results in real-time
  - simplify sharing and reusing workflows between researchers
  - enable researchers to track the provenance of workflow execution results and the workflow creation steps.  

## Provenance of data

- Provides a historical record of data, its origins and causal relationships.
- Can use it to ensure quality of data based on ancestral data, or find sources of errors.
- Allows automated recreation of data.
- Directed acyclic graphs (DAGs)
  - Useful representation of data and their provenance
  - Nodes can represent data, calculations, etc. - links represent their connections
  - Used in many workflow management systems  

![]({{ site.baseurl }}/img/dag.svg)




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

## What tools are out there?

- [Sumatra](http://sumatra.readthedocs.io/en/0.7.4/), manages and tracks numerical simulations.
- [Common Workflow Language](https://github.com/common-workflow-language/common-workflow-language), a specification for describing analysis workflows and tools which are portable and scalable across software and hardware environments.
- [Snakemake](http://snakemake.readthedocs.io/en/stable/), a workflow management system to create reproducible and scalable data analyses.
- [Ruffus](https://code.google.com/archive/p/ruffus/), a lightweight python module for running computational pipelines.
- [AiiDA](http://www.aiida.net/), a flexible and scalable informatics' infrastructure to manage, preserve, and disseminate the simulations, data, and workflows of modern-day computational science (electronic structure calculations).
- [Kepler](https://kepler-project.org/), GUI tool to help scientists, analysts, and programmers create, execute, and share models and analyses across a broad range of scientific and engineering disciplines.
- [VisTrails](https://www.vistrails.org/index.php/Main_Page), an open-source scientific workflow and provenance management system that provides support for simulations, data exploration and visualization (GUI).
- [Pegasus](https://pegasus.isi.edu/), workflow management system to automate, recover, and debug scientific computations (command line and browser interface tool automating).
- [make](https://www.gnu.org/software/make/), not only for compiling code!


## Sumatra

- A tool for managing and tracking projects based on numerical simulations/analysis, aiming to supporting reproducible research. 
- An automated electronic lab notebook for computational projects.
- Similarities to Git, and is connected to Git or other VCS tools.
- Keeps track of what was run: source code, input parameters, environment configuration, dependencies, etc.
- Stores when something was run, how long it took, what were input and output results.
- Easy to repeat calculations.
- Let's you browse a librariy of your activity via the browser.


### Type-along exercise

1. Clone this sample repository [insert repo url]
 - Sumatra needs to interact with a version control system (Git, Subversion, Mercurial, Bazaar).
 - Files in repository:

    <table style="width:50%;">
    <tr>
     <th style="text-align: center; border: 1px solid black; padding: 3px; width:15%"> File </th>
     <th style="text-align: center; border: 1px solid black; padding: 3px; width:35%"> Purpose </th>
    </tr>
    <tr>
     <td style="text-align: left; border: 1px solid black; padding: 3px;"> simulate.py </td>
     <td style="text-align: left; border: 1px solid black; padding: 3px;"> Generate "simulation data" </td>
    </tr>
    <tr>
     <td style="text-align: left; border: 1px solid black; padding: 3px;"> simulate_with_parameters.py </td>
     <td style="text-align: left; border: 1px solid black; padding: 3px;"> Read input parameter from file and generate "simulation data" </td>
    </tr>
    <tr>
      <td style="text-align: left; border: 1px solid black; padding: 3px;"> analysis.py </td>
      <td style="text-align: left; border: 1px solid black; padding: 3px;"> Calculate some statistics on simulation data </td>
    </tr>
    <tr>
      <td style="text-align: left; border: 1px solid black; padding: 3px;"> param.dat </td>
      <td style="text-align: left; border: 1px solid black; padding: 3px;"> Input parameter file </td>
    </tr>
    </table>

2. Initialize Sumatra repository:  
   ```
   $ smt init my-project
   ```
   This creates a directory `.smt/` which, similar to `.git` in Git, keeps track of Sumatra history.   
   ```
   $ ls .smt
   project    records.db
   ```
   The `project` file contains information on the project, including the default executable and paths to input files, output data, 
   and the record store. The record store `records.db`, containing a database with information on calculations, 
   is by default a SQLite database (if django is installed).

   #### Optional configuration steps
   To store paths to input or output relative to the working directory or some other directory
   (useful if running computations for the same project on multiple computers,
   or if one needs to relocate the project directory), one can specify this as follows:
   ```
   $ smt configure --input .   # relative to working directory
   ```
   or, for output data:
   ```
   $ smt configure --datapath /path/to/data
   ```

   The record store can be changed to a different location at the initialization stage by
   ``` 
   $ smt init --store =~/sumatra.db my-project
   ```
   or at a later stage using `smt configure` after `smt init` (this will copy existing content from `.smt/records.db`):
   ``` 
   $ smt configure --store =~/sumatra.db
   ```

   Sharing a record store with remote collaborators is possible by setting up a server running the 
   [Sumatra Server](https://bitbucket.org/apdavison/sumatra_server/wiki/Home):
   ```   
   $ smt init --store=https://username:password@hostname/ my-project
   ```
   Sumatra will then send records to the server, from where collaborators can access them 
   through an account on the server, or if the project is set to public. 

   There's also an option to automatically make an archive copy of output data 
   relieving you of the need to do so. To activate this, you need to choose a base directory in which to store your archives,
   e.g.:
   ```
   $ smt configure --archive ./archive
   ```
   One can also specify an URL at which your datafiles will be mirrored, e.g.:
   ```
   $ smt configure --mirror https://dl.dropboxusercontent.com/u/xyzxyz/
   ```

3. Run calculations

   Running a mock simulation with the given Python scripts would normally be done by 
   ```
   $ python simulate.py 1000
   ```  
   which generates a datafile in `Data/simulation_output.pkl` with 1000 random samples from a normal distribution, followed by
   ```
   $ python analyze.py Data/simulation_output.pkl
   ```
   which calculates the mean, standard deviation and kurtosis of the normal distribution, and prints the mean to the file 
   `Data/statistics.txt`.

   To instead run the simulation using Sumatra, we do
   ```
   $ smt run --executable=python --main=simulate.py 1000

   Record label for this run: '20171201-145336'
   Data keys are [simulation_output.pkl(ccc40965da14f707c29868c05f15128356954f33 [2017-12-01 14:53:42])]
   ```
   Let's run the analysis on the simulation data right away:
   ```
   $ smt run --executable=python --main=analysis.py Data/simulation_output.pkl
   
   Record label for this run: '20171201-145353'
   Data keys are [statistics.txt(d947cca73167742d5a17473898e261b99c116fb4 [2017-12-01 14:53:59])]
   ```

   How do we inspect the project's history? Sumatra provides commands similar to `git log`:
   ```
   $ smt list

   20171201-145336
   20171201-145353   
   ```
   or 
   ```
   $ smt list --long
   ```
   which gives long output containing which script (main file) was used, arguments, output data, which Git commit, etc.

   What happens if we modify `simulate.py` and try to run again?
   ```
   # modify simulate.py
   $ smt run --executable=python --main=simulate.py 1000
   Code has changed, please commit your changes
   ```
   Sumatra annotates each calculation with the commit hash, and it will not allow us to run a script which has uncommitted changes!

   We might want to annotate a particular run, and Sumatra supports this through the `smt comment` command (cf. Git commit message!)
   ```
   $ smt comment 20171201-145353 "finally the correct result"
   ```
   this changes the Outcome field of the calculation.  
   Tags can also be useful:
   ```
   $ smt tag simulation 20171201-145336
   $ smt tag analysis 20171201-145353
   $ smt tag foobar # this tags the latest run
   ```




<!-- 
## Exercise: Common workflow language

   > This material has been adapted from [an online tutorial](http://www.commonwl.org/user_guide/)

-->
