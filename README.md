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

<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>
<hr>




# YAML-Crash-Course
This repo has the beginner friendly info about YAML file format. Enough to get started working with YAML files.

### 1. **Human-Readable Format:**
   - YAML (YAML Ain't Markup Language) is designed to be easy for humans to read and write. It uses indentation to define structure, making it similar in appearance to Python or plain text.

### 2. **Key-Value Pairs:**
   - YAML primarily uses key-value pairs, where the key and value are separated by a colon and a space. Example:
     ```yaml
     name: John Doe
     age: 30
     ```

### 3. **Hierarchy Through Indentation:**
   - YAML uses indentation (spaces, not tabs) to represent nested structures, like dictionaries or lists. Proper indentation is crucial as it defines the structure of the data.
     ```yaml
     address:
       street: 123 Main St
       city: Anytown
     ```

### 4. **Lists:**
   - Lists in YAML are denoted by a hyphen followed by a space. Each item in the list is placed on a new line.
     ```yaml
     fruits:
       - Apple
       - Orange
       - Banana
     ```

### 5. **Comments:**
   - Comments in YAML start with a `#` and can be placed anywhere in the document.
     ```yaml
     # This is a comment
     name: John Doe  # Inline comment
     ```

### 6. **Data Types:**
   - YAML supports various data types including strings, numbers, booleans, nulls, and complex types like lists and dictionaries. Strings don’t need to be quoted unless they contain special characters.
     ```yaml
     age: 30         # Integer
     married: true   # Boolean
     children: null  # Null
     ```

### 7. **Multiline Strings:**
   - YAML allows for multiline strings using `|` (preserves newlines) or `>` (folds newlines into spaces).
     ```yaml
     description: |
       This is a
       multiline string
     ```

### 8. **Anchors & Aliases:**
   - Anchors (`&`) and aliases (`*`) allow you to reuse content. An anchor defines a value, and an alias refers back to it.
     ```yaml
     default: &default_settings
       timeout: 30
       retries: 3

     server1:
       <<: *default_settings
       host: server1.example.com
     ```

### 9. **YAML vs JSON:**
   - YAML is a superset of JSON, meaning any valid JSON is also valid YAML. However, YAML is more user-friendly due to its readability and concise syntax.

### 10. **File Extensions and Usage:**
   - YAML files typically have the `.yaml` or `.yml` extension and are commonly used for configuration files, data exchange between languages, and more in DevOps, CI/CD pipelines, and other contexts.

These pointers should provide a solid foundation for understanding and working with YAML.






-------------------------------------------------------------------------------

params.yaml setup:
``` 
1> import yaml
2> add func:
def load_params(params_path: str) -> dict:
    """Load parameters from a YAML file."""
    try:
        with open(params_path, 'r') as file:
            params = yaml.safe_load(file)
        logger.debug('Parameters retrieved from %s', params_path)
        return params
    except FileNotFoundError:
        logger.error('File not found: %s', params_path)
        raise
    except yaml.YAMLError as e:
        logger.error('YAML error: %s', e)
        raise
    except Exception as e:
        logger.error('Unexpected error: %s', e)
        raise
3> Add to main():

# data_ingestion
params = load_params(params_path='params.yaml')
test_size = params['data_ingestion']['test_size']

# feature_engineering
params = load_params(params_path='params.yaml')
max_features = params['feature_engineering']['max_features']

# model_building
params = load_params('params.yaml')['model_building']

-------------------------------------------------------------------------------

-------------------------------------------------------------------------------

dvclive code block:
1> import dvclive and yaml:
from dvclive import Live
import yaml
2> Add the load_params function and initiate "params" var in main
3> Add below code block to main:
with Live(save_dvc_exp=True) as live:
    live.log_metric('accuracy', accuracy_score(y_test, y_test))
    live.log_metric('precision', precision_score(y_test, y_test))
    live.log_metric('recall', recall_score(y_test, y_test))

    live.log_params(params)
  
```