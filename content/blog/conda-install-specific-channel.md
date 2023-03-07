---
title: "Installing a `conda` package from a specific channel"
date: 2023-03-07T14:46:20-05:00
tags: [conda]
---

While trying to set up some new packages in a conda environment, I accidentally "upgraded" to an incompatible version of one of the libraries. I created an environment to run Psi4 and wanted to add some new dependencies. Before proceeding, I decided to upgrade the packages in the environment using `mamba upgrade --all`. Before accepting the changes, I made sure there weren't any major version upgrades, then proceeded with the upgrade. What I didn't notice was that two of the libraries (`libecpint` and `pint`) were moved from the psi4 channel to the conda-forge channel. Psi4 is quite particular about it's dependencies, so this change broke the installation. 

Since the "upgrade" was just a crossgrade (no version change, just a channel change), trying to fix it by adding the psi4 channel to the environment rc file (via `conda config --env --add channels psi4`) didn't help. Nor did changing the channel priority from flexible to strict (`conda config --env --set channel_priority strict`). What did finally work was (probably) what I should have tried first: manually specify the location with the package install command. Running `mamba install channel::package` took care of the issue and everything is now working just fine. 