---
title: "Streamlining the install of Jekyll and Github Pages on Ubuntu on Windows"
categories: github
author: aaroneg
tags: jekyll github
---
# Summary 
Writing Github pages is pretty easy but it's annoying having to commit, push and wait to see your changes, or maybe you want to preview the changes locally before everyone else can see them. 

The Github help pages are pretty good, but are not optimized for an Ubuntu 16.04 on Windows install.

# Install Ubuntu on Windows
It's very straightforward to install ubuntu on Windows. 

[Microsoft Documentation](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

# Install Ubuntu packages
These packages are required to allow all the gems to install properly.

```bash
sudo apt update && sudo apt install build-essential ruby ruby-dev zlib1g-dev -y
```

# Create your Github Pages repo:
[Github Documentation](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)

# Run the local server to preview your changes as you make them:
```bash
bundle exec jekyll serve
```