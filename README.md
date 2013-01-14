
# Thieriot

Thieriot is a simple tool for managing Jenkins builds for a project, right
from the shell.  It allows you to check which of your branches have Jenkins
jobs set up, and to easily create any that are missing.

## Usage

![](http://github.com/rodnaph/thieriot/raw/master/screenshot.png)

As you can see, each of your branches will be listed, along with...

* a tick/cross indicating if it has a build on Jenkins
* an ID you can refer to it as for commands
* information about if it is currently building or not
* if the branch has a build and it's failing the name will be red

## Configuration

Configuration is handled via a YAML file in your project root called _.thieriot.yml_.  The only required
parameter is the _jenkins_url_, if you don't specify the project name it will be guessed from the folder
name of your project.

```yaml
jenkins_url: jenkins.mycompany.com
project_name: myproject
```

Thieriot assumes your jobs are named after your project, with a hyphen then the branch name.  For example:

```
myproject-master
myproject-featurebranch
etc...
```

## Authentication

If your Jenkins instance requires authentication you can configure this using your
Jenkins username and your API token.  Just create the following environment
variables (eg. in .bash_profile or .zshrc).

```bash
export THIERIOT_USER=myuser
export THIERIOT_TOKEN=jj324g23jh4gj32h4g3hj4g234j23
```

## Creating a Jenkins job

The way Thieriot works is to use your master branch's job to create copies for
your feature branches.  This obviously means you need to create your master
build yourself, but after that setting up jobs for your feature branches is easy.

```bash
$> trt create 2
```

This will try and create a job for the branch numbered _2_.

## Building a job

Your jobs will probably build automatically on some commit hooks, but if they don't
then you can kick them off from the shell.

```bash
$> trt build 3
```

## Following a build

When a job is building you can follow its output right from the shell using the
_follow_ command.  If the job is not yet running it will be started.

```bash
%> trt follow 3
```

This will then print the job's console output straight to the shell.  You can stop
following by pressing _ctrl-c_.

## Deleting a job

When you're done with feature branches, it's easy to delete them right from the shell.

```bash
$> trt delete 2
```

Watch you don't delete master though! :O

## Viewing a job

To quickly open your browser to the branch's jobs page on Jenkins, use the view command.

```bash
$> trt view 2
```

(NB: Only works on OSX at the moment)

## Arbitrary job names

All Thieriot's commands can take a number as the alias for the branch/job.  But you can
also use arbitrary names, that may match jobs that you don't have branches for.  For
instance if your project has a packaging job named _myproject-pkg_ you could kick this
off and follow its progress using...

```bash
trt follow pkg
```

# Installation

## Macports

You can install Thieriot straight through MacPorts.

```bash
port install thieriot
```

## From Source

To install Thieriot from source just clone the repo, and put it in your _PATH_.
You might also need some of the dependencies, listed below depending on your OS.

 * Perl
 * Perl JSON
 * Perl JAML

Perl modules available from CPAN if they're not packaged for your OS.

```
$> sudo cpan
install JSON
install YAML
```

