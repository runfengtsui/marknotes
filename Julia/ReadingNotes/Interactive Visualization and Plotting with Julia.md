---
Title: Interactive Visualization and Plotting with Julia (Diego Javier Zea)
Author: 邱彼郑楠
Date: 2023-04-01
Modified: 2023-04-21
---

1. Julia defines project environments using two files.
    * `Project.toml` file that stores the set of dependencies.
    * `Manifest.toml` file that stores the exact version of all the packages and their dependencies.

While the former is mandatory for any environment, the latter is optional.

2. There are multiple options for dealing with project environments.
    * start `julia` in a given environment by using the `--project` argument.
    * change between environments using the `activate` command in `Pkg` mode.
    * run the `instantiate` command of `Pkg` mode to get all the needed packages when you first activate a non-empty environment on your system.
