# Gradebook Merge

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
- An LMS gradebook file in a supported format
- A Gradescope export file in a supported format

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
3. **Validate the inputs:** Check the files for compatibility and review student matching.
4. **Generate a match report:** Investigate questionable or uncertain student matches.
5. **Merge the grades:** Run the merge command with the appropriate options.
6. **Review the output:** Inspect the updated gradebook carefully before uploading it to the LMS.

### Configuration

The repository includes **`config-example.yml`** as a starting point for configuration.

Review the configuration carefully before using it for a course. **Grading options must reflect the course's actual grading policies.** For example, do not enable a `drop-lowest` setting unless the course actually uses that grading rule.

## API

The project provides both a **Python API** and the **`gbmerge` command-line interface**.

The main API entry point is `MergeJob`. The package also supports functionality related to:

- Student matching
- Grading policies
- Upload planning
- Output generation
- Audit logging

### Command-Line Help

To view all available commands and general options, run:

```bash
gbmerge --help
```

To view the options for the merge operation, run:

```bash
gbmerge merge --help
```

### Python API Reference

The implementation is located in **`src/gbmerge/`**.

Refer to the source files in this directory for the exact class constructors, function signatures, parameters, and return values.

## Maintainers

This README is maintained by **Shritan Kondaveti** as part of the CS305 README assignment in the **CS305_README** GitHub repository.

## Credits

This repository is based on the original **readme-project-gradebook-merge** project.

Credit goes to the original project author, **Tim Richards**.
