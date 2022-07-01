+++
author = "Thiago Araujo"
title = "Website with Hugo is a breeze"
date = "2022-07-01"
description = "A simple tutorial to create beautiful sites with Hugo."
tags = [
    "FOSS", 
    "Hugo",
]
categories = [
    "Computers",
]
+++

The goal of this post is twofold. First I want to help other people to build their static website 
without spending two important resources: time and money. Also, it is an explanation to my future 
self -- as Damian Conway said: 
> _"Documentation is a love letter that you write to your future self”_

So, let's get started.

## Hugo 

[Hugo](https://gohugo.io/) is the framework we use to build our website. The advantage of this framework 
-- at least for me -- is that we do not need to write a single line of HTML and CSS, this is 
good because my knowledge of these things is very close to zero -- and I don't want to learn them. 
With Hugo, we write our code in [markdown](https://www.markdownguide.org/), and Hugo themes do 
the rest for us. This webpage, for example, uses the theme: 
[Coder](https://themes.gohugo.io/themes/hugo-coder/) -- very neat theme.

Hugo has a nice documentation, and a very useful 
[quickstart](https://gohugo.io/getting-started/quick-start/). But before start playing with 
Hugo, it is useful to set the Github configuration.

## Github 

We want to use Github Pages to host our website. Let us first create two repos -- it is not necessary, 
but it is useful to keep our website organized. In particular, one of these repos will keep 
track of our Hugo configurations, the markdown, preferences and so on. I have called this repo 
`website` (see my github profile), but here let us call it `repo_01`. The second repo is the static 
website we generate with Hugo. It must be named as the URL page, in my case `thraraujo.github.io`, but 
here refer to it as `repo_02.github.io`. The idea of this second repo is to carry all 
static files (html, css and so on) of the website. It will be a submodule of the first one -- we will 
get there. 

Given what we said in the previous paragraph, I have cloned these two repos in my working directory, so 
I have something of the form:

```
./repo_01 
./repo_02.github.io
```

Always work in the `main` branch to avoid conflicts with Github pages. So, rename your 
`master` branch if necessary. Furthermore, I have initially added a readme to my second repo, and Github pages
was loading for this file.

## Setting and testing the website

Good. Now you run:

```
cd repo_01
hugo new site my_beautiful_website
```

and Hugo creates a lot of files inside the directory `my_beautiful_website`. The next step is to 
select a theme to your website. Hugo has a nice collection of [themes](https://themes.gohugo.io/).
As I said, I have chosen the [Coder](https://themes.gohugo.io/themes/hugo-coder/), but you better 
check out the options. Once you have chosen your beautiful theme, clone it to the folder 
themes inside the website directory, that is `my_beautiful_website/themes`.

Now we need to tweak two things. The file `config.toml` in `my_beautiful_website` must have all 
the configurations we need to use for our website -- and configuring it might be complicated. 
Let us use the lazy approach: Inside `my_beautiful_website/themes`, there is the folder with 
your chosen theme, and onelevel down, there should be a example website. Replace the original 
(and naked) `config.toml` of `my_beautiful_website` with the file of the example website -- 
and you are almost done. 

Now, open the `config.toml` with your favorite editor. The base website is a example URL. Change 
it to your website URL. In other words, you will find 

```
baseURL = "http://www.example.com"
```

replace with 

```
baseURL = "https://repo_02.github.io/"
```

The content of the website is in 
```
./repo_01/my_beautiful_website/content
```

Add some content -- check the example website once again to understand some parameters, definitions 
and so on. You can also modify one example page to fit your needs. In any case, add some content. 
Once you think you're ready. You might want to know if you didn't make any mistake. The command 

```
hugo server
```

will create a local server that you can access at `http://localhost:1313/`. Keep it open to see 
the modifications. 


## Deploying the website

Once you finished all these details, we need to deploy the website. Now it is time to play with 
the second repo `repo_02.github.io`. We have already cloned this repo, so let us make it a 
submodule of the first one. Basically we need to link it to the folder 
`./repo_01/my_beautiful_website/public`. 

So, go to the `my_beautiful_website` and use the command 

```
git submodule add -b main <URL of repo_02.github.io> public 
```

We are now watching watching all these modifications inside this page. We want to keep 
track of these modifications because Hugo generates its static files inside the `public` folder. 
At this point, this folder is empty, but we can finally generate our site (the static files) with 
the command

```
hugo -D
```

Now you can commit and push your modifications to github. If done correctly, our webpage already online --
that's the Github pages magic. As a final detail, you might want to pull the modifications to the second 
repo just to keep things syncronized. I recommend the following order 

    1. push ./repo_01/my_beautiful_website/public
    2. push ./repo_01 
    3. pull ./repo_02.github.io

And that's it.
