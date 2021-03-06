---
layout: post
title:  "Contribution Guide"
post-title:  "Contribution Guide"
date:   2021-04-22 21:41:46 -0500
permalink: /tutorials/contribution_guide.html
permalink_name: /contribution_guide
category: tutorials
description: "Guide to contributing to this site"

categories: Tutorials
---

---
# Overview

---
This site is based on GitHub Pages and Jekyll. You can use these to host a static site without ever touching html or css. Your posts are written in markdown(cheatsheet). Markdown is very simple to write basic posts in, and Jekyll handles the parsing of these files and creates a standard html and css based site for you.

Jekyll is fairly simple to use once you have it set up. You’ll need a few things to get going.

* Linux (For Example: Ubuntu)
* [Ruby](https://www.ruby-lang.org/en/documentation/installation/)
* [Bundler](https://bundler.io/)

If you don’t know how to use Linux here’s a [great site](https://linuxjourney.com/).

If you don’t know git here’s a basic [guide](https://git-scm.com/docs/gittutorial). I didn’t vet this thoroughly, but it
looks decent enough.

---
To download the project simply run:

```shell
git clone https://github.com/UML-Embedded/uml-embedded.github.io.git
```

---
# Project Structure

---
This tree shows you how the project is structured.

uml-embedded

* index.md
* tutorials.md 
* blog.md
* about.md
* 404.html
* assets
    * images
    * posts
        * tutorials
            * tutorial_template
                * tutorial_template_asset1.png
                * tutorial_template_asset2.png
        * blogs
        * projects
* _posts
    * 2021-01-1-tutorial_template.md
    * 2021-02-1-blog_template.md
    * 2021-03-1-project_template.md

---
This is a pretty rough outline of the structure. Unless your editing one of the main tabs you only really need to focus on the posts, and assets folders. The assets folder will hold the images you need to include in your post. Sort it under the appropriate category(for example, tutorials) and label it as you see fit within that folder.

Your post will go under the post folder will contain your post. The title of the post must follow the format shown. The date must be accurate, and you must use dashes as shown until you reach the post name. Within the post name please use underscores to separate words.

As long as you fill out the header information for the post properly, Jekyll will autogenerate everything for you. Here is an example post for the tutorial template post shown above

---
# Example Post

---
```markdown
---
layout: post
title:  "Tutorial Template"
post-title:  "Tutorial Template"
date:   2021-01-01 21:41:46 -0500
permalink: /tutorials/tutorial_template.html
permalink_name: /tutorial_template
detail_image: /assets/images/posts/tutorials/tutorial_template/tutorial_template_asset2.png
category: tutorials
description: "Template for tutorials :)"

categories: Tutorials
---

---

# Body of your post goes here :)
* Write all your stuff and things!
* Here!
![Images too!](/assets/images/tutorial_template/tutorial_template_asset1.png)

Markdown can have embedded html too!
```
---
# Going through the example

---
```markdown
layout: post
title:  "Tutorial Template"
post-title:  "Tutorial Template"
```

The layout will always be post. Do not change this unless you know what you’re doing.

The title is whatever you would like to call your post, and your post title will need to be the same.

---
```markdown
date:   2021-01-01 21:41:46 -0500
permalink: /tutorials/tutorial_template.html
permalink_name: /tutorial_template
detail_image: /assets/images/posts/tutorials/tutorial_template/tutorial_template_asset2.png
```

The date must be accurate to when you write the post. If the date and time occurs in the future the post will not be generated by Jekyll until that time occurs. The permalink should go /category/post_title.html

Categories
* tutorials
* blogs
* projects

Post title will be the title you previously chose in lower case letters, seperated by underscores rather than spaces.

The detail image will be pasted into the header page for each section. (ie: the tutorial page has a small clip of the image) and the post put the detail image at the top of the post itself. If you do not want a detail image simply delete the line.

---
```markdown
category: tutorials
description: "Template for tutorials :)"

categories: tutorials
---

---

# Body of your post goes here :)
```
Category is the respective category of your post. The same categories as listed above.

The first set of dashes closes of the header that jekyll uses, and the second set is a simple markdown horizontal rule. I like the look of it so keep it around please.

Everything after this goes into the body of your post. You can write anything you want in markdown or html, and it will be generated by Jekyll into the main site.

---
# Generating the Site

---
After you’ve written the post you’ll need to generate the site, and you should see your new post added to the respective category. You’ll need to run a few commands in the terminal to do it

```shell
cd uml-embedded.github.io
bundle update
bundle exec jekyll serve
```

That last command will host the site on a local server. The link will appear in the terminal after you enter it. Go ahead and look through the post to make sure it looks how you want, and when you’re satisfied, make a pull request.

---
# Creating a Pull Request for Your Post
---

All you need to do is fork the repository, create a development branch, make your changes, push to your repo and then go on GitHub and generate a pull request.

Here’s a good [guide](https://opensource.com/article/19/7/create-pull-request-github) on that.