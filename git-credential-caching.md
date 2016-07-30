# Git Credential Caching

Okay, I've been using Git continuously for the past 72 hours. And I must say, having to enter my username and password for every *git push* I do is extremely annoying.

### Fix

One thing you can do is to use a *credential helper* to make Git cache your Github username and password everytime it talks to Github.

### Enable Git Caching

```sh
$ git config --global credential.helper cache
```

The default cache-timout is *15mins*. You probably want to change that to 1hr or so by doing:

```sh
$ git config --global credential.helper 'cache --timeout=3600'
```

This post is also my immediate test to see if this Git credential caching system serves my purpose. :)

### Edit

It works!