---
title: Website publication
date: 2022-04-22T14:21:20-05:00
author: Dustin Wheeler
tags: [site, lektor, github-pages]
---

## GitHub Pages

 This site is hosted using [GitHub Pages][gh-pages], a hosting service available to all GitHub accounts (for free!). Setting up [Lektor][lektor] to deploy to GitHub is very simple once you've configured your machine to [connect to GitHub using an SSH connection][gh-ssh].
 
 Instructions can be found in the [Lektor deployment docs][lk-deploy], but here's a brief summary:
 
 - Add the following line to your Lektor project config file (`project_name.lektorproject`) in the root folder of your site:
```
[servers.ghpages]
target = ghpages://your-user/your-repository
```
	 
  - If the repository is `username.github.io`, this will be published to your default user site (<https://username.github.io>). Otherwise, it will be published to the project-specific page (<https://username.github.io/project-name>)
 - Once this is set up, you can deploy the current build of your site by executing `lektor build && lektor deploy` from the command line. 


[gh-pages]: https://pages.github.com.com/
[lektor]: https://www.getlektor.com/
[gh-ssh]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh
[lk-deploy]: https://www.getlektor.com/docs/deployment/ghpages/