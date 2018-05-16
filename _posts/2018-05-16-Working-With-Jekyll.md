---
title: "Working With Jekyll and Github Pages"
categories: jekyll
author: aaroneg
tags: jekyll rage github github-pages
---
# Summary
Basic Jekyll / Github Pages operation is pretty simple if you want to use the 'out of box' stuff. The moment you begin wanting to customize things is where you run into trouble. So far it's been a fun project, but there are some things that I skimmed over in the documentation that I probably should have stopped and read closer.

# Choosing a theme
I wanted to use the 'hacker' theme, not because I feel like I'm some sort of amazing 'hacker' person, nor do I pretend to be an expert on most things. It's just the best (in my opinion) theme supported by Github Pages out of the box. I like dark themes because even though there's plenty of sunlight in all of the places I'm sitting at a computer reading things, when it's night or overcast outside there are few things more annoying than a bright white light in my eyes.

[Github](https://pages.github.com/themes/) provides a small assortment of supported themes.

# Customizing your theme and site pages
You'll need to ensure your site has the following folders to continue:
```
_includes
_layouts
```

* `_includes` is where you'll place things like HTML snippets that you'll include on some or all of your pages.
* `_layouts` is where you'll change how pages of X type will be displayed

## Acquire the layouts from your theme
The reason you can begin without a `_layouts` folder is, github does some magic and pulls those in from your chosen theme. To begin, find the github repo for the theme and browse to it's `_layouts` folder. 

These are the source of your layouts if you've never added your own. They're also the place you should start, if you want to tweak a few things but still want it to be properly themed. Copy the layouts from the theme into your `_layouts` folder.

I wanted to change the site title from the repository name to the name of my domain. I also wanted to get rid of the prominent placement of github badges and add an edit link to all of my posts so a visitor could see the source for the pages.

## Make the changes you'd like
Here's the commit I made to do most of the things referenced in this post. [a5879c2](https://github.com/aaroneg/aaroneg.github.io/commit/a5879c20f71453bdd4c4f3a1bef10db5770381df)


# References
* [Github supported themes](https://pages.github.com/themes/)
* [How not to get frustrated with jekyll](http://cyluun.github.io/blog/how-to-not-get-frustrated-with-jekyll)
* [Customizing CSS and HTML in your Jekyll theme](https://help.github.com/articles/customizing-css-and-html-in-your-jekyll-theme/)