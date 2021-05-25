<<<<<<< HEAD
[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/kronik3r/daktilo/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

# Daktilo
Daktilo is a [Jekyll](jekyllrb.com) theme with a minimal design inspired from typewriters.

# More info and Live preview
[Click here](http://daktilo.github.io/) to see the theme in action.

# Features
- Fully responsive
- [Disqus](https://disqus.com/) integration for comments.
- Google Analytics integration.
- Syntax Highlighter (using [highlight.js](https://highlightjs.org/)).
- Support for categories.
- Font-Awesome Icons.
- Optimized for SEO.
- Coolest [404 page ever](http://electrik-frog.com/daktilo/404.html).

# How to use it
Start by cloning the repository, then check the `_config.yml` file and change it accordingly.
Note that the `title` property is what will be displayed as logo.

Finally execute `jekyll serve --watch` and head to [localhost:4000](http://127.0.0.1:4000) to see the result.

# Using categories
Categories are little bit tricky. Please make sure to do the following for each category:

- Create a file within `categories` folder with the name of your category
For example let's say that we have a category called `An Awesome Category` you will need to add an `an-awesome-category.html` file with this content:

``` html
---
layout: category
category: an-awesome-category
permalink: /categories/an-awesome-category/
---

```

- Create an entry inside `_data/categories.yml`

``` html
- slug: an-awesome-category
  name: An Awesome Category
```

- Then you will see it in the footer in the `Explore` section.

# License

The contents of this repository is licensed under [The MIT License.](https://opensource.org/licenses/MIT)
=======
# Strata Reloaded

Simple, clean personal blogging template for Jekyll based on Strata by HTML5 UP.

![Strata Reloaded template screenshot](images/_screenshot.png)

## Features

* Parallax background effect
* Lightbox gallery
* Pre-styled components
* Blog with pagination
* Configurable footer
* Optimized for editing in [CloudCannon](https://cloudcannon.com/)
* RSS/Atom feed
* SEO tags
* Google Analytics
* Webmaster Verification

## Develop

1. Add your site and author details in `_config.yml`.
2. Add your Google Analytics key to `_config.yml`.
3. Get a workflow going to see your site's output (with [CloudCannon](https://app.cloudcannon.com/) or Jekyll locally).

## Develop

Urban was built with [Jekyll](https://jekyllrb.com/) version 3.3.1, but should support newer versions as well.

Install the dependencies with [Bundler](https://bundler.io/):

~~~bash
$ bundle install
~~~

Run `jekyll` commands through Bundler to ensure you're using the right versions:

~~~bash
$ bundle exec jekyll serve
~~~

## Editing

Strata Reloaded is already optimized for adding, updating and removing posts and footer elements in [CloudCannon](https://app.cloudcannon.com/).

### Posts

* Add, update or remove a post in the *Posts* collection.
* Change the defaults when new posts are created in `_posts/_defaults.md`.

### Footer

* Exposed as a data file to give clients better access.
* Set in the *Data* / *Footer* section.

## License

Free for personal and commercial use under the CCA 3.0 license. See LICENSE file for additional information and terms of use. This theme was adapted from Strata by HTML5 UP for use with [CloudCannon](https://cloudcannon.com) by [Comfusion LLC](https://comfusionllc.com).
>>>>>>> d2fae1c56cab60ec3f628bcc9f85c586ea3f276f
