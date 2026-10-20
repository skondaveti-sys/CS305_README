Gradebook Merge

Description

gradebook-merge is a Python command-line tool and library for merging Gradescope scores into a learning management system gradebook file. It helps instructors check student matches, review proposed grade changes, and prepare an updated gradebook for upload.

The command-line interface is gbmerge. It provides commands for checking input files, merging grades, generating student match reports, and initializing configuration.

Table of Contents

1. Description

2. Install

3. Usage

4. API

5. Maintainers

6. Credits

Description

gradebook-merge works on the process of transferring Gradescope scores into a learning management system (LMS) gradebook upload file.

The project provides tools to:

- Check input files: Validate gradebook and Gradescope data before merging.

- Match students: Compare student records across the two sources.

- Merge scores: Prepare an updated gradebook file using the configured grading rules.

- Generate match reports: Reviews how students were matched between files.

- Configure merge jobs: Initializes a configuration file for a particular workflow.


The command-line program is named gbmerge. The package also provides a Python API.

Install

Requirements: Python 3.10 or newer and Gradebook and Gradescope export files in supported formats.

Installation:

Clone this repository and navigate to the project directory:

git clone https://github.com/skondaveti-sys/CS305_README.git

cd CS305_README

Install the package:

python -m pip install -e .

To install the development dependencies:

python -m pip install -e ".[dev]"

After installation, check that the command is available:

gbmerge --help

Usage

Available Commands

Command                       Purpose

gbmerge check.            Check input files and their compatibility.

gbmerge merge             Merge Gradescope scores into the LMS gradebook.

gbmerge match-report      Generate a report about student matching.

gbmerge init-config       Initialize a configuration file.


Typical Workflow:

1.Prepare the LMS gradebook and Gradescope export.

2.Initialize a configuration file if your workflow requires one.

3.Check the inputs and review student matching.

4.Generate a match report and investigate questionable matches.

5.Run the merge with the appropriate options.

6.Inspect the output before uploading it to the LMS.

Configuration: The repository includes config-example.yml as a starting point for configuration. Review the configuration carefully before using it for a course. Grading options must reflect the course's actual policies. For example, a drop-lowest setting should not be enabled unless the course uses that grading rule.

API

The project gives us a Python API and the gbmerge command-line interface.

The main API entry point is MergeJob. The package also supports functionality related to student matching, grading policies, upload planning, output generation, and audit logging.

Command-Line Help

To inspect the CLI options:

gbmerge --help

To inspect the options for an individual operation:

gbmerge merge --help

Python API Reference

The implementation is located in src/gbmerge/. Use the source files there for the exact class constructors, function signatures, parameters, and return values.

Maintainers

This README is maintained by Shritan Kondaveti as part of the CS305 README assignment in the CS305_README GitHub repository.

Credits

This repository is based on the original readme-project-gradebook-merge project.

Credit goes to the original project author: Tim Richards.
