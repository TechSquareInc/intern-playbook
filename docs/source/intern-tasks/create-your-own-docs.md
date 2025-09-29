# Create Your Own Documentation Pages using Sphinx & Read the Docs

*Documentation is a critical skill for system administrators, researchers, developers, or anyone working on a project that needs clear communication. Having a well structured documentation site can make your work more accessible and professional.*

## Sphinx

[Sphinx](https://www.sphinx-doc.org/en/master/index.html) is a powerful documentation generator wrritten in Python. It takes plain-text source files, usually written in [reStructured Text](https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html), but also supports [Markdown](../core-tools/learning-markdown), and converts them into html pages. Sphinx lets you organize your content into multiple pages, create tables of contents, and embed code examples.

## Read the Docs

[Read the Docs](https://docs.readthedocs.com/platform/latest/index.html) is a platform that hosts documentation sites. It integrates with Sphinx projects seemlessly, and connects to GitHub or GitLab to automatiicaly build your site whenever you push changes.

### Getting Started

**1. Set Up Your Environment**

Creating a virtual environment isn't neccessary, but can help keep dependencies isolated from other working environments.
```bash
python -m venv venv
source venv/bin/activate
```

**2. Install Sphinx and MyST parser**

MyST Parser allows writing in Markdown, which is often simpler and used more widely than reStructured Text
```bash
pip install sphinx
pip install myst-parser
```

**3. Initialize Your Sphinx Project**

Sphinx provides a command-line tool called `sphinx-quickstart` that sets up the project structure. After running this `sphinx-quickstart` command, Sphinx  will have created a source directory with `conf.py` and a root document, `index.rst`. This root document serves are a welcome page, as well as contains the "table of contents tree" or *toctree*.

The `source` directory is where you will place your markdown files. You'll also see a `build` folder where the generated html pages wil appear. After making a few pages, or editing pages, from the `docs` directory, you can run `make html` to see these pages built in your browser.

> **Note:** Sphinx documentation has a more complete tutorial on their [documentation site](https://www.sphinx-doc.org/en/master/tutorial/index.html) that takes you through buidling your first project.


**4. Initialize Your Git Repository**

Read the Docs makes your documentation publicly acessible and automatically rebuilds the site whenever you push updates. If you've already run `sphinx-quickstart` and have a Sphinx project folder with `source/`, `build/`, `conf.py`, and `index.rst`, you can initialize a git repository from the root of your Sphinx project (the directory containing `docs/`).
```bash
git init
```

Sphinx generates a lot of files in `build/` that don't need to be versioned. Create a `.gitignore` file and add files you want to be ignored when versioning.
```bash
# Python
.venv/

# Sphinx build output
docs/_build/
docs/build/
```

**5. Hosting on Read the Docs**

Once you have a repo established on Git, you'll need to link the project to Read the Docs. First, create an  account. Navigate to the [Sign Up Page](https://app.readthedocs.org/accounts/signup/) and choose the option "Sign Up with GitHub" (or GitLab, depending on preference). On the authorization page, click the green `Authorize readthedocs` button. Finish following the account configuration steps, including the "verify your email address" step, and then you should see your Read the Docs dashboard.

Next, you can import your Git project to Read the Docs. From your dashboard, click the `Import a Project` button and add the Git project with your Sphinx pages. You'll need to fill out a few details about your project, inclduing Name, the Repository URL, and the Default branch. Click `Next` to create the project, and open the project home. From you project home, if the build has finished, you will see a green "Build completed" indicator. Once your pages have been built, click the `View docs` button to your documentation live.

> **Note:** Read the Docs documentation has a more complete tutorial on their [documentation site](https://docs.readthedocs.com/platform/latest/tutorial/index.html#) that takes you through setting up a project using an already created sphinx project [template](https://github.com/readthedocs/tutorial-template/).

### Best Practices

- Organize content logically with headings, subheadings, and seperate pages.
- Be specific, consistent, and include clear examples and references for commands or scripts.
- Update your documentation whenever scripts, workflows, or tools change.

### Challenge

Using one of the projects you created from this documentation site, create your own docs to pair with your project. 


## Resources
- [Sphinx Documentation](https://www.sphinx-doc.org/en/master/index.html): Official Sphinx Documentation
- [reStructuredText Documentation](https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html): Offical reStructuredText Documentation
- [Read the Docs](https://docs.readthedocs.com/platform/latest/index.html): Official Read the Docs Documentation
- [Sphinx Tutorial](https://www.sphinx-doc.org/en/master/tutorial/index.html): Getting Started with Sphinx Tutorial
- [Read the Docs Tutorial](https://docs.readthedocs.com/platform/latest/tutorial/index.html#): Getting Started with Read the Docs Tutorial
- [Read the Docs Sign Up](https://app.readthedocs.org/accounts/signup/): Read the Docs Account Creation
- [GitHub Repo for Sphinx Project Template](https://github.com/readthedocs/tutorial-template/): Template for building Sphinx Projects
- [Sphinx Templates](https://sphinx-themes.org/): Sphinx Theme  Gallery
