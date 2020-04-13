# CS52 Workshops:  TITLE OF YOUR WORKSHOP

![](http://i.giphy.com/eUh8NINbZf9Ys.gif)

Brief motivation here as well as in presentation

## Overview

This tutorial will walk you through the creation of a static website using Jekyll, a static-site generator, and then through styling that website using Bootstrap.

## Setup

Visit this link for instructions on setting up the environment.  [Jekyll Setup](https://jekyllrb.com/docs/installation/macos/)

## Step by Step

Assuming you did the setup correctly, you should have Ruby > 2.4.0 installed. Why is this important? Ruby is an OOP programming language commonly used in web applications, and Jekyll happens to run on it. Ruby groups its modules by calling them "gems," which you can install.
1. Install the Jekyll and bundler gems in your project root directory (the bundler gem is just a gem management system). Run ```gem install jekyll bundler```.
2. Create a Gemfile to list your project's dependencies by running ```bundle init```.
3. Do ```nano Gemfile``` and add ```gem "jekyll"``` to the bottom of the file. This lists Jekyll as a dependency for you project.
4. Run ```bundle``` which will install Jekyll in your project (installing the gem just made it available to your computer).
5. Do ```touch index.html && code index.html```. This will create an HTML file in your root directory, and open it in VSCode.
6. In the file, paste the following:
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Home</title>
  </head>
  <body>
    <h1>Hello World!</h1>
  </body>
</html>
```
7. Now we will build and output our static site. Run ```jekyll build```. This will create a directory called ```_site```, where a copy of your ```index.html``` will be stored. It is this file that will be displayed as your site.
8. Now output your site with ```jekyll serve```, and open ```http://localhost:4000``` to access it! You should see an ```h1``` tag that says ```Hello World!``` Your site has been deployed locally to port ```4000```, the default for Jekyll.
9. You will now write your first line of Jekyll. Open ```index.html``` in your root directory and insert the following code at the very top of the file:
```
---
heading: Hello World!
---
```  
Now, change the text in the ```h1``` to ```{{ page.heading }}```. Now reload the page. It didn't change! That's because the syntax at the top of the page assigns heading as a variable name for the ```page```, and it contains the text ```Hello World!```. In Jekyll, double curly braces identify variables created in such a way.  
Let's test out a filter. Change the contents of the ```h1``` to ```{{ page.heading | downcase }}```, then refresh the page. You should see ```hello world!```.  
Why does this work, although it is not standard HTML5? If you enter the ```_site``` directory, it may provide some insight. The deployed site is from ```_site/index.html```, NOT the file you just modified. By running ```jekyll serve``` before, you told Jekyll to — on any change to ```index.html``` — rebuild the page in ```_site/index.html```, then redeploy it to port ```4000```. There is no "Jekyll" syntax in ```_site/index.html```, because Jekyll processes ```index.html``` into HTML5 that the browser can read. The way that Jekyll knows that you want to use its syntax is the inclusion of the "triple dash" section at the top of you ```index.html```. Pretty cool!  

10.  Now let's add some CSS. Add the following line of code to the bottom of the ```head``` section in ```index.html```:
```
<link rel="stylesheet" href="style.css">
```
In the terminal, go to your root directory and do ```touch style.css``` to create an empty stylesheet. Open it up and add the following style to it:
```
h1 {
  color: purple;
}
```
If you reload your page, you should see the text change color. What if you wanted to add ten more pages to your site with the same stylesheet, but didn't want to have to link the CSS file every time?   
As a problem that can easily extend to the inclusion of many, many CSS, JS, and other ```head``` properties, there is a way to streamline this in Jekyll.  
The answer is Layouts. First, let's create our second page, not in HTML, but in Markdown.  

11. Do ```touch about.md``` in your root directory, and add the following to it (you can personalize the text):
```
# About page

This page tells you a little bit about me.
```  

To turn this Markdown file into HTML, we will need to create a layout for it. Go to the terminal in your root directory and do ```mkdir _layouts && cd _layouts && touch default.html```. These commands will create a directory fo your layouts and an empty layout.  
Paste the following content in there:  
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <link rel="stylesheet" href="style.css">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {{ content }}
  </body>
</html>
```  
Now add the following to the top of your about.md:  
```
---
layout: default
title: About
---
```  
Here, you are passing ```default``` as the layout file you want to use to create the html file for the about page, and ```About``` as the title to be used in ```page.title``` on that page.  

12. Now go to ```http://localhost:4000/about.html``` in your browser. You should see your newly created about page!  

13. Next, we will work on some basic navigation. Suppose you wanted a ```nav``` that each of your pages share. In normal HTML, you would have to write it into each page individually. Jekyll makes this process modular, allowing you to import (or rather, include) HTML from a centralized source into each of your pages.  
14. In your root directory, do ```mkdir _includes && cd _includes && touch navigation.html```. This creates the directory for HTML that will be used in multiple files, as well as the file that we will be using to store our navigation code.  
15. Paste the following into navigation.html:
```
<nav>
  <a href="/">Home</a>
  <a href="/about.html">About</a>
</nav>
```  
You might wonder why we dont need to include the ```html``` tag anywhere in this file. That is because we are only storing a single component (the ```nav```) in this file, and it will inevitably be used in a file that does have ```html``` tags.  
In default.html (in your ```_layouts``` directory) add the following line to the top of the body:  
```
{% include navigation.html %}
```
Then, add ```layout: default``` into the top section (three-dash area) of your index.html under the root directory.  

We just did a couple of things. First, in ```default.html``` the ```{% %}``` syntax indicates logic or control-flow code. ```include``` is a special keyword that reaches into our ```_includes``` directory and searches for the parameter, ```navigation.html```. When it finds that file, it takes the code inside and inserts it where ```include``` was called, thus showing our ```nav```.  
In the index.html folder, we added the default layout in order to include our ```nav```. Technically, a lot of the code in ```index.html``` is now redundant, because we have a layout for it. However, this is inconsequential to the functioning of our website.  





* Explanations of the what **and** the why behind each step. Try to include:
  * higher level concepts
  * best practices

Remember to explain any notation you are using.

```javascript
/* and use code blocks for any code! */
```

![screen shots are helpful](img/screenshot.png)

:sunglasses: GitHub markdown files [support emoji notation](http://www.emoji-cheat-sheet.com/)

Here's a resource for [github markdown](https://guides.github.com/features/mastering-markdown/).

## Use collapsible sections when you are giving away too much code
<details>
 <summary>Click to expand!</summary>
 
 ```js
 // some code
 console.log('hi');
 ```
</details>



## Summary / What you Learned

* [ ] can be checkboxes

## Reflection

*2 questions for the workshop participants to answer (very short answer) when they submit the workshop. These should try to get at something core to the workshop, the what and the why.*

* [ ] 2 reflection questions
* [ ] 2 reflection questions


## Resources

* cite any resources
