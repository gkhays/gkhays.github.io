---
layout: post
title: Learning About GitHub Pages and Jekyll
---

Ignore the super old date on this post, it is inherited from the fork. I'm just now getting around to updating this thing. Eventually, I want to take some of my projects and Gists and wrap them in articles.

Candidates:

* JavaScript Sine Wave
* OrientDB Test Drive
* Ethereum PoC

Meanwhile, I had to learn some new things to get everything working smoothly.

## Notes on Relative Images

Since I have a dedicated `images` folder, how do I refer to relative image links when using Jekyll and Markdown? Is it `/images/xxx` or will `images/xxx` (with no leading slash) suffice? Below are one of each.

```md
![With](/images/404.jpg)
```
![With](/images/404.jpg)

```md
![Without](images/404.jpg)
```
![Without](images/404.jpg)

Wow! The first image is huge. Trying inline `HTML` instead. Note: I had to use a leading slash.

<img src="/images/404.jpg" alt="GitHub Mascot" style="width: 200px;"/>

Jekyll resolves relative links without the slash to `_posts` whereas a leading slash makes it relative to the top-level. Observe.

![Apparent Relative Link](/images/relative-links.png)

Or as Stimpy would say `obser-uve`!

![Stimpy](/images/scholar-stimpy.png)

## How to Change Image Size

`<img src="drawing.jpg" alt="Drawing" style="width: 200px;"/>`

[How to change image size Markdown?](http://stackoverflow.com/a/14747656/6146580)

`- End -`
