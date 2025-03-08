# dvc_aws

## Building Pipeline:
* Create a GitHub repo and clone it in local (Add experiments).
* Add src folder along with all components(run them individually).
* Add data, models, reports directories to .gitignore file
* Now git add, commit, push
<br>
## Setting up dcv pipeline (without params)

* Create dvc.yaml file and add stages to it.
* dvc init then do "dvc repro" to test the pipeline automation. (check dvc dag)
* Now git add, commit, push
<br>
## Setting up dcv pipeline (with params)

*  add params.yaml file
*  Add the params setup (mentioned below)
*  Do "dvc repro" again to test the pipeline along with the params
*  Now git add, commit, push
<br>
## Expermients with DVC:

* pip install dvclive
* Add the dvclive code block (mentioned below)
* Do "dvc exp run", it will create a new dvc.yaml(if already not there) and dvclive directory (each run will be considered as an experiment by DVC)
* Do "dvc exp show" on terminal to see the experiments or use extension on VSCode (install dvc extension)
* Do "dvc exp remove {exp-name}" to remove exp (optional) | "dvc exp apply {exp-name}" to reproduce prev exp
* Change params, re-run code (produce new experiments)
* Now git add, commit, push
