---
title:  "How to install jekyll On Mac OS"
header:
  teaser: "jekyll-400x250.jpg"
categories: 
  - Jekyll
tags:
  - update
---

{% include toc title="Install Jekyll" %}


## 1. Ruby
For most Mac OS version today, it has already installed ruby by default. You can check it use command as follows in your terminal.

```
  ruby -v
```

However, if you have to install one, I strongly recommand you install [rvm](http://rvm.io/rvm/install) or [homebrew](https://brew.sh/) first, then install ruby.

## 2. RubyGem
RubyGems is a package management framework for Ruby.You can use commands as follow to check the version and update gem.

```
  gem -v 
  gem update --system 
```

## 3. jekyll
Use gem to install jekyll.

```
  gem install jekyll
```

**Warning Notice:** After Mac OS 10.11, because of the `rootless`, users can't modify `/usr/bin` directory even if using 'sudo' or 'su'. However, gem will install packages to the default directory which is equal to gem installation path `/usr/bin` causes error. Here is two ways to solve this problem:
{: .notice--warning}

* a. Shut down rootless

```
sudo nvram boot-args="kext-dev-mode=1 rootless=0";sudo reboot
```

* b. Install jekyll to other directory

&emsp;&emsp;Use -n set target directory


```
sudo gem install jekyll -n /usr/local/bin/
```

&emsp;&emsp;Then add /usr/local/bin to your path environment variable.

```
export PATH="/usr/local/bin:$PATH"
source ~/.bash_profile
```

&emsp;&emsp;Finally use command as follows to check whether jekyll is installed successfully.

```
jekyll -v
```

