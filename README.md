# VCS-PRE-COMMIT BUILDOUT


This help to install and configure 
[vcs-pre-commit](https://github.com/petrus-v/vcs-pre-commit) by sandboxing it
with [buildout](http://www.buildout.org)


## Install

This is what I've done on my Debian Jessie

```Shell
mkdir ~/.pre-commit
cd ~/.pre-commit
:~/.pre-commit$ virtualenv-3.4 -p python3.4 --no-setuptools pre-commit-venv
~/.pre-commit$ hg clone https://github.com/petrus-v/vcs-pre-commit-buildout.git pre-commit-buildout
~/.pre-commit$ cd pre-commit-buildout
~/.pre-commit/pre-commit-venv/bin/python bootstrap.py -c buildout.cfg
~/.pre-commit/pre-commit-buildout$ bin/buildout -c buildout.cfg
~/.pre-commit/pre-commit-buildout$ cd ~/bin
~/bin$ ln -s ../.pre-commit/pre-commit-buildout/bin/vcs-pre-commit
```

## Configuration

### Mercurial

Add this part in you ``~/.hgrc`` file

```init
[hooks]
precommit.vcs-pre-commit = vcs-pre-commit --vcs hg
```

### Git

With git you can't set global hooks, but we still have a way using template
directory:


```Shell
~$ cd
~$ mkdir -p ~/.git/templates/hooks/
~$ ln -s ~/bin/vcs-pre-commit ~/.git/templates/hooks/pre-commit
~$ git config --global init.templatedir '~/.git/templates'
```

Then the symbolic link will  be created on all your new repo.

You can simply do `git init` on existing repos to apply your git template.

*ressource*:

* [git-init documentation](http://git-scm.com/docs/git-init)

## Similar projects

* [pre-commit](http://pre-commit.com): As I understood, this aims to configure
  GIT pre-commit hooks per project (yes inside the project). Wher vcs-pre-commit
  assume you are workgins on multiple projects
  requiring similar pre-commit hooks and with multiple vcs.
