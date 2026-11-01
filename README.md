# gradebook-merge

## Description

**gradebook-merge** is a Python command-line tool and library for merging Gradescope scores into a learning management system (LMS) gradebook file. It helps instructors verify student matches, review proposed grade changes, and prepare an updated gradebook for upload.

The command-line interface is named **`gbmerge`**. It provides commands for validating input files, merging grades, generating student match reports, and initializing configuration files.

## Table of Contents

1. [Description](#description)
2. [Install](#install)
3. [Usage](#usage)
4. [API](#api)
5. [Maintainers](#maintainers)
6. [Credits](#credits)

## Install

### Requirements

- **Python 3.10 or newer**
- No additional dependencies or input files are required to install the project
- You will provide the LMS gradebook and Gradescope export files when using it.

### Installation

**1. Clone the repository** and navigate to the project directory:

```bash
git clone https://github.com/skondaveti-sys/CS305_README.git
cd CS305_README
```

**2. Install the package:**

```bash
python -m pip install -e .
```

**3. (Optional) Install the development dependencies:**

```bash
python -m pip install -e ".[dev]"
```

**4. Verify the installation:**

```bash
gbmerge --help
```

## Usage

### Available Commands and Their Purposes

The `gbmerge` command-line interface provides the following operations:

| Command | Purpose |
|---|---|
| `gbmerge check` | **Validate input files** and check their compatibility before merging. |
| `gbmerge merge` | **Merge Gradescope scores** into the LMS gradebook file. |
| `gbmerge match-report` | **Generate a student matching report** to help identify and review matches between records. |
| `gbmerge init-config` | **Initialize a configuration file** for a particular grading workflow. |

### Typical Workflow

Follow these steps to prepare and merge grades:

1. **Prepare the input files:** Export the LMS gradebook and Gradescope scores.
2. **Initialize configuration:** Create a configuration file if your workflow requires one.
   ```bash
   gbmerge init-config
   ```
   This creates gbmerge.yml, which you can edit to customize grading policies, late penalties, and other settings. If the default settings work for your course, you can skip this step.
3. **Validate the inputs:** Check the files for compatibility and review student matching.
   ```bash
   gbmerge check --roster roster.csv --exports exports --assignment "Assignment Name"
   ```
   Replace the example filenames and assignment name with your own.
4. **Generate a match report:** Investigate questionable or uncertain student matches.
   ```bash
   gbmerge match-report --roster roster.csv --exports exports
   ```
   Check for unmatched students, unmatched submissions, or ambiguous matches that may need attention.
5. **Merge the grades:** Run the merge command with the appropriate options.
   ```bash
   gbmerge merge --roster roster.csv --exports exports --assignment "Assignment Name" --dry-run
    ```
   If the preview looks correct, run the command again without --dry-run to generate the updated gradebook.
6. **Review the output:** Inspect the updated gradebook carefully before uploading it to the LMS.

### Configuration

Generate `gbmerge.yml` using the initialization command:

```bash
gbmerge init-config
```
Review the configuration carefully before using it for a course. **Grading options must reflect the course's actual grading policies.** For example, do not enable a `drop-lowest` setting unless the course actually uses that grading rule.

## API

The `gbmerge` package exposes functions and classes for loading gradebooks, matching students, applying grading policies, and generating upload files.

### Main Classes

- **`MergeJob`** – Runs the complete gradebook merge workflow.
- **`Gradebook`** – Provides step-by-step control over loading, matching, scoring, and planning.
- **`Roster`**, **`GradescopeExport`** – Represent roster and Gradescope export data.
- **`MatchReport`** – Stores student matching results.
- **`Policy`** – Defines grading rules.
- **`ScoreSheet`** – Stores calculated scores.
- **`UploadPlan`** – Prepares grade changes for export.

### Loading and Configuration

- `load_roster(path)` – Loads a class roster.
- `load_export(path)` – Loads one Gradescope export.
- `load_exports(directory="exports")` – Loads exports from a directory.
- `load_config(path=None)` – Loads configuration settings.
- `find_config(start=".")` – Finds a configuration file.
- `detect_excel_damage(fieldnames, rows)` – Checks for possible spreadsheet formatting damage.

### Matching Students

- `match_students(roster, exports, ...)` – Matches roster entries to Gradescope submissions.
- `parse_match_on(value)` – Parses matching strategies.
- `explain_unmatched(report, roster)` – Explains unmatched students.

### Grading Policies

- `apply_policy(roster, report, policy=None, ...)` – Applies grading rules.
- `late_days(lateness_seconds, grace_minutes=0.0)` – Calculates billable late days.
- `apply_rounding(value, mode="half_up", places=2)` – Rounds a score.
- `drop_lowest_questions(question_scores, count)` – Drops the lowest question scores.
- `register_policy(name, fn=None)` – Registers a custom grading policy.
- `get_policy(name)` – Retrieves a registered policy.
- `available_policies()` – Lists available policies.

### Creating Upload Files

- `build_upload_plan(roster, sheet, assignment_column, ...)` – Builds a grade upload plan.
- `write_upload_csv(path, plan, ...)` – Writes the upload CSV.
- `write_audit_log(path, plan, ...)` – Writes an audit log.

### Extending Grading Policies

Custom policies can be registered using `register_policy`. A policy receives a `ScoreContext` and returns a `PolicyOutcome` or numeric score.

```python
from gbmerge import register_policy, PolicyOutcome

@register_policy("my_policy")
def my_policy(context):
    # Add custom grading logic here
    return PolicyOutcome(score=0)
from gbmerge import register_policy, PolicyOutcome

@register_policy("my_policy")
def my_policy(context):
    # Add custom grading logic here
    return PolicyOutcome(score=0)
```
Example
```python
from gbmerge import MergeJob, load_config

config = load_config()
job = MergeJob(
    roster="roster.csv",
    exports="exports",
    assignment="Assignment 1",
    config=config,
)

job.load()
job.match()
job.score()
plan = job.plan()
job.write(plan, out="upload.csv")
```
Errors
The package defines GbmergeError and specialized exceptions, including ConfigError, RosterError, ExportError, MatchError, PolicyError, and WriteError.

For command-line options, run:
```Bash
gbmerge --help
gbmerge merge --help
```

## Maintainers

This README is maintained by **Shritan Kondaveti(skondaveti-sys)** as part of the CS305 README assignment in the **CS305_README** GitHub repository.

## Credits

This repository is based on the original **readme-project-gradebook-merge** project.

Credit goes to the original project author, **Ana**.
