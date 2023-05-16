---
layout: article
---

# {{ page.title }}

{% raw %}
> 명령행의 경우 Mac 환경에서 진행하였으며, 확장성을 위해 최대한 페이지당 종속되는 명령행은 레이아웃으로 빼내거나 생략하였다.

## 1. 환경설정

`command`
```bash
$ brew update
$ brew install rbenv ruby-build
$ rbenv versions
# if the current ruby uses system ruby, you need to change it with the command below
# $ rbenv install -l
# $ rbenv install 3.2.2(latest)
# $ rbenv versions
# $ rbenv global 3.2.2
# $ rbenv versions
# $ echo $SHELL
# $ vi ~/.zshrc or ~/.bashrc
# [[ -d ~/.rbenv ]] && \ 
#     export PATH=${HOME}/.rbenv/bin:${PATH} $$ \
#     eval "$(rbenv init -)"
# $ source ~/.zshrc or ~/.bashrc
$ gem install jekyll bundler
$ cd {prooject_root_path}
$ jekyll new ./
$ bundle install
$ bundle exec jekyll serve 
```

## 2. `_config.yml` 설정

`command`
```bash
$ pwd
{project_root_path}
$ vi _config.yml
```

`_comfig.yml`
```yml
project:
  name: blog.kkmproject
  author: kwangmin_kim
```

## 3. `_layouts` 설정

`command`
```bash
$ pwd
{project_root_path}
$ mkdir _layouts
$ cd _layouts
$ vi default.html
$ vi article.html
```

`default.html`
```html
---
---

<html>
<head>
{% include head.html %}
</head>
<body>
{% include header.html %}
<main>
    {{ content }}
</main>
{% include footer.html %}
</body>
</html>
```

`article.html`
```html
---
---

<html>
<head>
{% include head.html %}
</head>
<body>
{% include header.html %}
<main class="article">
    {{ content }}
</main>
{% include footer.html %}
</body>
</html>
```

## 4. `_includes` 설정

`command`
```bash
$ pwd
{project_root_path}
$ mkdir _includes
$ cd _includes
$ vi head.html
$ vi header.html
$ vi footer.html
```

`head.html`
```html
<meta charset="UTF-8">
<link rel="icon" href="/assets/icon/favicon.ico" type="image/x-icon">
<link rel="stylesheet" href="/assets/css/style.css">
<title>{{ site.project.name }}</title>
```

`header.html`
```html
<header>
    <h1><a href="/">{{ site.project.name }}</a></h1>
</header>
```

`footer.html`
```html
<footer>
    <div>ⓒ{{ site.project.author }}</div>
</footer>
```

## 5. `_data` 설정

`command`
```bash
$ pwd
{project_root_path}
$ mkdir _data
$ cd _Data
$ vi categories_for_articles.yml
```

`categories_for_articles.yml`
```yml
- name: java
  link: /home/article/java
- name: spring
  link : /home/article/spring
- name: jekyll
  link : /home/article/jekyll
```

## 6. `assets` 설정

```bash
$ pwd
{project_root_path}
$ mkdir assets
$ cd assets
$ mkdir css
$ mkdir font
$ mkdir icon
$ mkdir images
# set file ...
$ tree ./
.
├── css
│         └── style.css
├── font
│         ├── IBMPlexMono-Regular.ttf
│         └── IBMPlexSansKR-Regular.ttf
├── icon
│         ├── favicon.ico
│         ├── list-directory-icon.png
│         └── list-file-icon.png
└── images
```

## 7. 페이지 작성

`index.md`
```html
---
layout: default
---

**default**
<ul class="list-style-file">
        <li><a href="/home/about">about</a></li>
</ul>

**List of article categories**
<ul class="list-style-directory">
    {% for ca in site.data.categories_for_articles %}
        <li><a href="{{ ca.link }}">{{ ca.name }}</a></li>
    {% endfor %}
</ul>
```

`/home/about.md`
```html
---
layout: default
---

# About kkmproject

email : 1721046@gmail.com
```

`/home/categories.md`
```html
---
layout: default
---

{% assign title = page.name | split: "." | first %}

# Article list : {{ title }}

<ul class="list-style-file">
{% for post in site.posts %}
    {% if post.categories contains title %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
{% endfor %}
</ul>
```

`/home/category/_posts/article.md`
```html
---
layout: article
---

# {{ page.title }}

content...

```

## 8. 전체구조

```bash
$ tree {project_root_path}
kkmproject.github.io
├── 404.html
├── Gemfile
├── Gemfile.lock
├── _config.yml
├── _data
│   └── categories_for_articles.yml
├── _includes
│   ├── footer.html
│   ├── head.html
│   └── header.html
├── _layouts
│   ├── article.html
│   └── default.html
├── _site
│   ├── 404.html
│   ├── assets
│   │   ├── css
│   │   │   └── style.css
│   │   ├── font
│   │   │   ├── IBMPlexMono-Regular.ttf
│   │   │   └── IBMPlexSansKR-Regular.ttf
│   │   └── icon
│   │       ├── favicon.ico
│   │       ├── list-directory-icon.png
│   │       └── list-file-icon.png
│   ├── feed.xml
│   ├── home
│   │   ├── about.html
│   │   └── article
│   │       ├── java.html
│   │       ├── jekyll
│   │       │   └── 2023
│   │       │       └── 05
│   │       │           └── 14
│   │       │               └── github_pages_구축기.html
│   │       ├── jekyll.html
│   │       └── spring.html
│   └── index.html
├── assets
│   ├── css
│   │   └── style.css
│   ├── font
│   │   ├── IBMPlexMono-Regular.ttf
│   │   └── IBMPlexSansKR-Regular.ttf
│   ├── icon
│   │   ├── favicon.ico
│   │   ├── list-directory-icon.png
│   │   └── list-file-icon.png
│   └── images
├── home
│   ├── about.md
│   └── article
│       ├── _drafts
│       │   └── YYYY-MM-DD-title.md
│       ├── java
│       │   ├── _drafts
│       │   └── _posts
│       ├── java.md
│       ├── jekyll
│       │   ├── _drafts
│       │   └── _posts
│       │       └── 2023-05-14-github_pages_구축기.md
│       ├── jekyll.md
│       ├── spring
│       │   ├── _drafts
│       │   └── _posts
│       └── spring.md
└── index.md
```
{% endraw %}