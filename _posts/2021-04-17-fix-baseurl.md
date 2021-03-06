---
layout: post
author: aska
---
# Project Page URL Structure

Sometimes it’s nice to preview your Jekyll site before you push your gh-pages branch to GitHub. However, the subdirectory-like URL structure GitHub uses for Project Pages complicates the proper resolution of URLs. Here is an approach to utilizing the GitHub Project Page URL structure (username.github.io/project-name/) whilst maintaining the ability to preview your Jekyll site locally.

1. In `_config.yml`, set the baseurl option to `/project-name` – note the leading slash and the absence of a trailing slash. `ex: baseurl: '/my-proj'`

2. When referencing JS or CSS files, do it like this: `{{ site.baseurl}}/path/to/css.css` – note the slash immediately following the variable (just before “path”).

3. When doing permalinks or internal links, do it like this: `{{ site.baseurl }}{{ post.url }}` – note that there is no slash between the two variables.

4. Finally, if you'd like to preview your site before committing/deploying using jekyll serve, be sure to pass an empty string to the `--baseurl` option, so that you can view everything at localhost:4000 normally (without `/project-name` at the beginning): ex: `jekyll serve --baseurl ''`

Also for Netlify, `jekyll build --baseurl ''`

And for Netlify, set `future: true` in `_config.yml`, or build using `--future` flag