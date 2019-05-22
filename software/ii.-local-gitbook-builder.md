---
description: Contributed by Xupeng Chen
---

# II. Local Gitbook Builder

> Gitbook 新版不再支持pdf和其他静态导出，也不再兼容旧版command line版本，旧版command line不支持右边栏和一些hint和embed语法，需要第三方插件，

### Install command line gitbook tool

先安装brew和npm两个包管理软件

```text
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```text
brew install node
brew install npm
```

再用npm安装gitbook

```text
npm install gitbook -g
npm install gitbook-cli -g
gitbook -V #查看版本gitbook和gitbook-cli版本
```

### Install packages for gitbook tool

在`book.json`中填入插件名称，then run `gitbook install`就可以自动安装依赖的插件。安装新版gitbook的一些替代插件以及一些额外的美化插件。

> urlembed取代embed，效果不是很完美，tabs也没有新版gitbook的效果 插件用法

```text
{% urlembed %}
https://website.org/stuff/this-is-the-path-name
{% endurlembed %}
```

```text
{% tabs first="First Tab", second="Second Tab", third="Third Tab" %}

{% content "first" %}
Content for first tab ...

{% content "second" %}
Content for second tab ...

{% content "third" %}
Content for third tab ...

{% endtabs %}
```

### Build gitbook \(html\)

```text
gitbook init #自动生成SUMMARY.md，但多级目录似乎无法找到，建议略过这一步用手工编辑版本
gitbook serve #可在浏览器预览，默认在http://localhost:4000
gitbook build #产生html
```

### How to build pdf/epub

* 下载calibre

  [https://calibre-ebook.com/dist/osx](https://calibre-ebook.com/dist/osx)

* 链接到`bin`下
* `ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin`
* 产生pdf `gitbook pdf . training_book.pdf`

