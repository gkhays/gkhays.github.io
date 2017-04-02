---
layout: post
title: Throw-Away First Post
---

Ignore the super old date on this post, it is inherited from the fork. I'm just now getting around to updating this thing. Eventually, I want to take some of my projects and Gists and wrap them in articles.

Candidates:

* JavaScript Sine Wave
* OrientDB Test Drive
* Ethereum PoC

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

Wow! This image is huge. Trying inline `HTML` instead.

<img src="images/404.jpg" alt="GitHub Mascot" style="width: 200px;"/>

- End -
