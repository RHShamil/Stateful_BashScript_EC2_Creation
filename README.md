# Stateful Bash Script for Launching EC2 Instances

This project provides a stateful bash script for launching EC2 instances on AWS. It utilizes `jq` to manage state information by storing details of created instances in a JSON file. This approach prevents accidental creation of duplicate EC2 instances with the same name.

## Table of Contents

- [Introduction](#introduction)
- [What is a Stateful Script?](#what-is-a-stateful-script)
- [Components](#components)
    - [AWS CLI](#aws-cli)
    - [jq](#jq)
    - [JSON File for State Management](#json-file-for-state-management)
- [How it Works](#how-it-works)
- [Usage](#usage)
- [Benefits of a Stateful Script](#benefits-of-a-stateful-script)
- [Importance of State Management](#importance-of-state-management)
- [Further Exploration](#further-exploration)

## Introduction

This project demonstrates how to create a bash script that tracks the state of launched EC2 instances. By storing instance details in a JSON file and using `jq` for JSON processing, the script avoids creating duplicate instances with the same name, ensuring idempotency and preventing accidental resource wastage.

## What is a Stateful Script?

A stateful script maintains information about its previous executions. This allows the script to make decisions based on past actions, rather than treating each execution as a completely new event. In this context, the script stores information about created EC2 instances to prevent duplication.

## Components

### AWS CLI

The AWS Command Line Interface (CLI) is a tool that allows you to interact with AWS services from the command line. We'll use it to launch EC2 instances.

### jq

`jq` is a lightweight and flexible command-line JSON processor. It allows you to easily parse, filter, modify, and output JSON data. We'll use it to read and update the JSON file storing the EC2 instance state.

### JSON File for State Management

The JSON file acts as our state store. It contains a list of created EC2 instances, with relevant details such as instance name, ID, and launch time. This file enables the script to check if an instance with a given name already exists before attempting to launch a new one.

## How it Works

1. **Check for Existing Instance:** The script reads the JSON file using `jq` to see if an instance with the desired name already exists.
2. **Launch New Instance (if not exists):** If the instance name is not found in the JSON file, the script proceeds to launch a new EC2 instance using the AWS CLI.
3. **Update JSON File:** After successfully launching an instance, the script adds the new instance details (name, ID, launch time) to the JSON file using `jq`.
4. **Handle Existing Instance (if exists):** If the instance name is found in the JSON file, the script can either:
    * Do nothing (if you want to prevent accidental re-creation).
    * Display a message indicating the instance already exists.
    * Perform other actions, such as updating tags or checking instance status.

## Usage

(Include example commands and explanations of how to use the script, including required AWS credentials and parameters.)

## Benefits of a Stateful Script

* **Idempotency:** The script can be run multiple times without creating duplicate resources.
* **Resource Management:** Prevents accidental creation of unnecessary EC2 instances, saving costs.
* **Automation:** Enables reliable automation of EC2 instance deployments.
* **Tracking:** Provides a record of launched instances, making it easier to manage and monitor your infrastructure.

## Importance of State Management

State management is crucial in automation and infrastructure management. It ensures that scripts and tools behave predictably and reliably, even when run multiple times or in complex environments. Without state management, you risk errors, inconsistencies, and resource conflicts.

## Further Exploration

* **AWS CLI Documentation:** Learn more about the AWS CLI and its capabilities.
* **jq Manual:** Explore the full power of `jq` for JSON processing.
* **Terraform or CloudFormation:** Consider Infrastructure-as-Code tools like Terraform or CloudFormation for more advanced infrastructure management.

This README provides a high-level overview of the project. The actual script and configuration details will be available in the repository files.
