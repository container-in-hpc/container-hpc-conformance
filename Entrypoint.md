# Entrypoint

This document aims to define a common understanding of what an entrypoint (and subsequently the CMD) is meant to do.
For a refresher on `ENTRYPOINT` and `CMD` please have a look at the section below.

## Goal

The initiative aims to define a common understanding of what entrypoints are supposed to do. 
Some containers use the entrypoint to pick the execution environment from multiple options installed within the container.
Not running the entrypoint will result in a broken container.

Others use the entrypoint in application containers so that arguments added to a container will be arguments to the main command (like `echo` below).


## ReCap entrypoint/cmd

The `ENTRYPOINT` is like the SHEBANG in a script. It defines the context in which arguments to the containers are executed. 

#### Alias containers (made up name)

Some use cases for containers are to substitute (`alias`) commands. 
For these containers it makes sense to prepare an entrypoint that sets up the container for the task at hand.

| ENTRYPOINT | CMD | RUN COMMAND | STDOUT |
| -----------| --- | ----- | ----- | 
| `echo` | `A B C` | `docker run $IMG A B C` | `A B C` |


#### Login containers (made up name)

A login containers will drop the user into a shell with the tools and applications available in the default environment (`PATH`,etc.).
Thus, a container can also be used non-interactively. `docker run 

| ENTRYPOINT | CMD | RUN COMMAND | STDOUT |
| -----------| --- | ----- | ----- | 
| `/bin/bash` | `` | `docker run $IMG echo A B C` | `A B C` |
| `/bin/bash` | `` | `docker run $IMG` | (drops into `bash`) |


