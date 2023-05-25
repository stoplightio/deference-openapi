# OpenAPI Dereferencing Action

This repository contains a GitHub Actions workflow that automatically dereferences OpenAPI specifications when a pull request is created or updated. The dereferenced specifications are committed to the `bundled_specifications` directory in the branch that triggered the workflow.

## Structure

The main workflow is defined in the file `.github/workflows/dereference-openapi.yaml`. This workflow runs whenever a pull request is created or updated.

The workflow does the following:

1. Checks out the code from the branch that triggered the workflow.
2. Installs `jq` and `yq`, which are command-line tools for handling JSON and YAML files.
3. Searches for YAML and JSON files in the repository, excluding the `bundled_specifications` directory.
4. For each file found, checks if it's an OpenAPI specification by looking for the `openapi` key.
5. If it's an OpenAPI specification, uses the `swagger-cli` tool to dereference it, and writes the output to the corresponding location in the `bundled_specifications` directory.
6. Commits the changes to the `bundled_specifications` directory and pushes them back to the branch.

The workflow logs the names of the files that were successfully and unsuccessfully dereferenced. You can view these logs in the GitHub Actions UI.

## Usage

To use this workflow in your own repository, follow these steps:

1. Create a `.github/workflows` directory in your repository if it doesn't already exist.
2. Copy the `dereference-openapi.yaml` file to your `.github/workflows` directory.
3. Create a pull request or update an existing one. The workflow will run automatically.

Please note that this workflow assumes your OpenAPI specifications are YAML or JSON files. If your specifications are in a different format, you'll need to modify the workflow to handle that format.
