# virtualenv in Python

## Introduction

virtualenv allows creation of isolated Python environments for each
project.

This prevents dependency conflicts between projects.

------------------------------------------------------------------------

## Creating a Virtual Environment

python -m venv myenv

------------------------------------------------------------------------

## Activating

Windows: myenv`\Scripts`{=tex}`\activate`{=tex}

Mac/Linux: source myenv/bin/activate

------------------------------------------------------------------------

## Installing Packages Inside Virtual Environment

pip install flask

------------------------------------------------------------------------

## Deactivating

deactivate

------------------------------------------------------------------------

## Why Use virtualenv?

-   Clean dependency management
-   Project isolation
-   Better deployment consistency

------------------------------------------------------------------------

## Real-World Scenario

Project A requires Django 3. Project B requires Django 4. Using
virtualenv, both projects can run without conflict.
