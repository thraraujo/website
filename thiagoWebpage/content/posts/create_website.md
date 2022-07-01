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

[Hugo](https://gohugo.io/) is a framework to build our website. The advantage of this framework 
-- at least for me -- is that we do not need to write a single line of HTML and CSS, this is 
good because my knowledge on these things is very close to zero -- and I don't want to learn them. 
With Hugo, we write our code in [markdown](https://www.markdownguide.org/), and Hugo themes do 
the rest for us. This webpage, for example, uses the theme: 
[Coder](https://themes.gohugo.io/themes/hugo-coder/) -- very neat theme.

Hugo has a nice documentation, and a very useful 
[quickstart](https://gohugo.io/getting-started/quick-start/). But before start playing with 
Hugo, it is useful to set the Github configuration.

## Github 

We need Github Pages to host our website. It is useful to create two repos. One of them will keep 
track of our Hugo configurations, the markdown, preferences and so on. I have called this repo 
`website`, but here I will call it `<repo_01>`. The second repo is the static website we generate 
with Hugo. I must be names as the URL page, in my case `thraraujo.github.io`, here 
`<repo_02.github.io>`. This repo will be a submodule of the first one -- we will get there. 
So, in my working directory, I have cloned these two repos:

```
./repo_01 
./repo_02.github.io
```

Something important -- always work in the `main` branch to avoid conflicts.

## Setting and testing the website

Good. Now you run 

```
cd repo_01
hugo new site my_beautiful_website
```

and Hugo creates a lot of files inside the directory `my_beautiful_website`. The next step is to 
select a theme to your website. Hugo has a nice collection of [themes](https://themes.gohugo.io/).
As I said, I have chosen the [Coder](https://themes.gohugo.io/themes/hugo-coder/), but you better 
check the options. Once you have picked your beautiful theme, clone it to the folder 
themes inside the website directory `my_beautiful_website`.

Now we need to tweak two things. The file `config.toml` of `my_beautiful_website` has all 
the configurations we need to use for our website, and its configuration might be complicated, 
and I prefer the lazy approach: Inside the folder themes, there is the folder with your chosen 
theme. Inside it there should be a example website. Replace the original `config.toml` of 
`my_beautiful_website` with the file of the example website and you are almost done. 

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
Once you think you're ready. You might want to check the website if everything is working. The 
command 

```
hugo server
```

will create a local server that you can access at `http://localhost:1313/`. Leave it open to see 
the modifications. 


## Deploying the website

Once you finished all these details, we need to deploy the website. Now it is time to play with 
the second repo `repo_02.github.io`. We have already cloned this repo, so let us make it a 
submodule of the first repo and link it to the folder `./repo_01/my_beautiful_website/public`.

So, go to the `my_beautiful_website` and use the command 

```
git submodule add -b main <URL of repo_02.github.io> public 
```

Hugo generates its static files inside the `public` folder. In this case, we are now watching 
all these modifications.

Finally you can generate your site as 

```
hugo -D
```

and now you can commit and push your modifications to github. If done as I said, your webpage 
is deployed. One final detail, you might want to pull the modifications from the second repo to
keep things syncronized. 


