# Running Python on the Cluster ✨

*Python is a high-level, interrpreted, general-purpose programming language.*

---

## Review of Python Fundamentals
Python's ease of use and rich ecosystem make it an essential tool in HPC workflows.

### Using Python in a SysAdmin Environment
Python is used instead of Bash if a program requires more complexity than Bash can handle.
According to the Google shell style [guide](https://docs.python.org/3/tutorial/index.html), you should use Python over Bash if:
- You are writing a script that is more than a 100 lines long.
- The control flow logic isn't straight forward.
- The script will grow in complexity in the future.
- The script will need regular maintenance.

### Python as a Script
To make an executable Python script, make sure, like any Bash script, you start your python file with a shebang. This allows you to rename your file and move it to `/usr/local/bin` to run it as a command.

#### Shebang
Use `#!/usr/bin/env python3` instead of `#!/bin/python3`.
- The former searches that user's `PATH` to find the `python3` binary.
- The latter assumes it is always installed to `/bin/` whcih can cause issues.

```bash
# Right:
	#!/usr/bin/env python3

# Less right:
	#!/bin/python3
```

## Resources
- [Running Python on an HPC Cluster](https://researchcomputing.princeton.edu/support/knowledge-base/python#quick): This site goes through setting up and running Python on an HPC cluster.
- [The Python Tutorial](https://docs.python.org/3/tutorial/index.html): This tutorial is designed for *programmers* that are new to Python, but **not** *beginners* who are new to programming.
