# Introduction
This repository contains several scripts useful for interacting with the RIT CS
department's "try" submission utility.

All of these tools are built around the idea that you are going to write code on
your personal machine, track the code with git and push your code "upstream" to
the CS machines.

## TRYSPEC
All of these tools depend upon the existence of a file named TRYSPEC in your
repository. There must be a different TRYSPEC for every repository / project.
This file is a ZSH script which describes how the project should be submitted.
An example TRYSPEC follows:

	typeset -r INSTRUCTOR="wrc-grd"
	typeset -r PROJECT="cg1-h1"
	
	typeset -a FILES
	FILES=( "hw1.txt" )
	typeset -r FILES

# Installation
- On the CS machines, symlink (or copy) the "try" and "git-init-for-try" scripts
  into some directory in your path. Mine is "~/bin". Make sure the directory you
  place it in is in your path in front of where the real "try" is.
- Add an exported environment variable called "TRY_HELPERS_HOME" to your shell's
  rc file. Set it to the location of your checked out try-helpers repository.
  You can do this by placing the following line in your bashrc:
  `export TRY_HELPERS_HOME="$HOME/path_to_repository"`

# Usage
- Create a git repository on the CS machines to be the "upstream" for your sources
  using the command `git init-for-try`. This will not and can not be a bare
  repository.
- Create a git repository on your machine for you to develop in. Make sure to
  write a TRYSPEC.
- Set the CS machine as your repository's upstream with your equivalent of
  `git remote add origin username@machine.cs.rit.edu:repositorydir`.
- When you run `git push`, the sources specified by your TRYSPEC will be
  automatically submitted!

There is also the "try" script. This is a script which wraps the real "try"
utility. It is used by the try-helpers git hook, but it also allows you to
submit using your TRYSPEC from the command line. From a CS department machine,
running "try" with no arguments will look for a TRYSPEC in the current directory
and automatically submit with try if one can be found.

<!--- vim:set tw=80: --->
