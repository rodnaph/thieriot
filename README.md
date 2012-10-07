
Thieriot
========

Thieriot is a simple tool for managing Jenkins builds for a project, right
from the shell.  It allows you to check which of your branches have Jenkins
jobs set up, and to easily create any that are missing.

Usage
-----

```bash
$> trt
Thierot 0.0.1

✓ [1]   master
✘ [2]   new-feature-branch
✓ [3]   other feature branch
```

Configuration
-------------

Configuration is handled via a YAML file in your project root called _.thieriot_.

```yaml
jenkins_url = jenkins.mycompany.com
project_view = MyProject
```

Creating a Jenkins job
----------------------

The way Thieriot works is to use your master branch's job to create copies for
your feature branches.  This obviously means you need to create your master
build yourself, but after that setting up jobs for your feature branches is easy.

```bash
trt create 2
```

This will try and create a job for the branch numbered _2_.

Building a job
--------------

Your jobs will probably build automatically on some commit hooks, but if they don't
then you can kick them off from the shell.

```bash
trt build 3
```

