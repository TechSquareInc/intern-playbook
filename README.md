# Intern Playbook

This repository contains documentation for interns, built using [Sphinx](https://www.sphinx-doc.org/) and will eventually get deployed to a static website hosted on AWS S3.

##  Purpose

This site is designed to provide onboarding guides, technical documentation, and resources for interns at TechSquare. The site is authored using reStructuredText and will be maintained via GitHub workflows.

---

## Getting Started with Development

### 1. Clone the Repository

```bash
$ git clone https://github.com/TechSquareInc/intern-playbook.git
$ cd intern-playbook
$ git checkout dev
```

### 2. Setup Your Python Environment

```bash
$ python -m venv .venv
$ source .venv/bin/activate
(.venv)$ python -m pip install sphinx
```

### 3. Build the Documentation Locally

```bash
cd docs
make html
```

#### View it in your browser:

```bash
xdg-open docs/build/html/index.html
```

## Deployment Workflow
 - Work happens in **feature branches off** `dev`
 - Open a PR into dev
 - Merging into `dev` will (eventually):
   - Trigger a GitHub Action to build the docs
   - Deploy them to the Dev S3 bucket
