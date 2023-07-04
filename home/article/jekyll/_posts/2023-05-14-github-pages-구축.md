---
layout: article
---

# {{ page.title }}

---

**index**
1. 환경설정
2. 테마설정
3. 내용설정
4. 전체구조

---


{% raw %}
# 1. 환경설정

**Terminal**
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
$ gem install jekyll bundler rouge
$ jekyll new ./
$ bundle install
$ bundle exec jekyll serve 
```

# 2. 테마설정

**Terminal**
```bash
$ mkdir ./assets/css
$ rougify style igorpro > assets/css/igorpro.css
```

**path: ./assets/css/igorpro.css**
```bash
.highlight table td { padding: 5px; }
.highlight table pre { margin: 0; }
.highlight, .highlight .w {
  color: #444444;
}
.highlight .cp {
  color: #CC00A3;
}
.highlight .cs {
  color: #CC00A3;
}
.highlight .c, .highlight .ch, .highlight .cd, .highlight .cm, .highlight .cpf, .highlight .c1 {
  color: #FF0000;
}
.highlight .kc {
  color: #C34E00;
}
.highlight .kd {
  color: #0000FF;
}
.highlight .kr {
  color: #007575;
}
.highlight .k, .highlight .kn, .highlight .kp, .highlight .kt, .highlight .kv {
  color: #0000FF;
}
.highlight .s, .highlight .sb, .highlight .sc, .highlight .dl, .highlight .sd, .highlight .s2, .highlight .se, .highlight .sh, .highlight .si, .highlight .sx, .highlight .sr, .highlight .s1, .highlight .ss {
  color: #009C00;
}
.highlight .sa {
  color: #0000FF;
}
.highlight .nb, .highlight .bp {
  color: #C34E00;
}
```

**path: ./assets/css/style.css**
```
@font-face {
    font-family: 'IBMPlexMono-Regular';
    src: url('/assets/font/IBMPlexMono-Regular.ttf') format('truetype');
}

@font-face {
    font-family: 'IBMPlexSansKR-Regular';
    src: url('/assets/font/IBMPlexSansKR-Regular.ttf') format('truetype');
}

html, body {
    width: 1200px;
    margin: 10px;
    overflow-x: hidden;
    overflow-y: auto;
    font-family: 'IBMPlexMono-Regular', 'IBMPlexSansKR-Thin', monospace;
    background-color:ghostWhite;
}

div {
    overflow: auto;
}

a {
    color:black;
}

ul {
    list-style-type: square;
}

/* semantic tag */
header {
    text-align: center;
    border-bottom: 1px solid black;
}

footer {
    border-top: 1px solid black;
    padding-top: 30px;
}

main {
    margin: 50px 0;
}

.date { font-size:small;color:gray; }

.list-style-directory { list-style-image: url('/assets/icon/list-directory-icon.png'); }
.list-style-file { list-style-image: url('/assets/icon/list-file-icon.png');}
.color-gray { color:gray; }
.font-small { font-size:small; }
.font-bold { font-weight:bold; }

.form-layout-1 * { margin: 5px 0;}
.form-layout-1 label { display:inline-block; width:100px; height:20px; vertical-align:top; text-align:center;}
.form-layout-1 select { width:1090px; height:30px; }
.form-layout-1 input { width:1080px; height:30px; }
.form-layout-1 textarea { width:1080px; height:700px; }
.form-layout-1 button { float:right; margin-right:5px;}

.article h1 {margin-top: 50px;}
.article h1:before { color:gray;content: "# "; }
.article h2 {margin-top: 40px;}
.article h2:before { color:gray;content: "## "; }
.article h3 {margin-top: 30px;}
.article h3:before { color:gray;content: "### "; }
.article h4 {margin-top: 20px;}
.article h4:before { color:gray;content: "#### "; }
.article h5 {margin-top: 10px;}
.article h5:before { color:gray;content: "##### "; }
.article h6 {margin-top: 0px;}
.article h6:before { color:gray;content: "###### "; }

.article blockquote {
    border-left:5px solid black;
    margin:20px 0;
    background-color:lightGray;
    width:100%;
}
.article blockquote p {
    padding:0 10px;
    margin: 0;
}
```

# 3. 내용설정

## 3.1. `_config.yml`

**path: ./_config.yml**
```yml
project:
  name: KIM's BLOG
  author: kwangminkim

# Conversion
highlighter: rouge
```

## 3.2. `_layouts`

**path: ./_layouts/default.html**
```html
---
---

<!DOCTYPE html>
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

**path: ./_layouts/category.html**
```html
---
---

<!DOCTYPE html>
<html>
<head>
    {% include head.html %}
</head>
<body>
{% include header.html %}
<main>
    {% assign title = page.name | split: "." | first %}

    <b>{{ title }}</b>

    <ul class="list-style-file">
        {% for post in site.posts %}
        {% if post.categories contains title %}
        <li><a href="{{ post.url }}"><span class="date">[{{ post.date | date : "%Y-%m-%d" }}]</span>{{ post.title }}</a></li>
        {% endif %}
        {% endfor %}
    </ul>
</main>
{% include footer.html %}
</body>
</html>
```

**path: ./_layouts/article.html**
`default.html`
```html
---
---

<!DOCTYPE html>
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

## 3.3. `_includes`

**path: ./_includes/head.html**
```html
<meta charset="UTF-8">
<link rel="icon" href="/assets/icon/favicon.ico" type="image/x-icon">
<link rel="stylesheet" href="/assets/css/style.css">
<title>{{ site.project.name }}</title>
```

**path: ./_includes/header.html**
```html
<header>
    <h1><a href="/">{{ site.project.name }}</a></h1>
</header>
```

**path: ./_includes/footer.html**
```html
<footer>
    <div>ⓒ{{ site.project.author }}</div>
</footer>
```

## 3.4. `_data`

**path: ./_data/main_categories.yml**
```yml
- name: Jekyll
  link: /home/article/jekyll
```

## 3.5. index

**path: ./index.md**
```md
---
layout: default
---

**default**
<ul class="list-style-file">
    <li><a href="/home/about">about</a></li>
</ul>

**List of categories**
<ul class="list-style-directory">
    {% for main_category in site.data.main_categories %}
        <li><a href="{{ main_category.link }}">{{ main_category.name }}</a></li>
    {% endfor %}
</ul>

**The last 5 articles**
<ul class="list-style-file">
    {% for post in site.posts limit:5 %}
        <li><a href="{{ post.url }}"><span class="date">[{{ post.date | date : "%Y-%m-%d" }}]</span><span>[{{ post.categories[-1] }}]</span>{{ post.title }}</a></li>
    {% endfor %}
</ul>
```

## 3.6. article

**path: ./home/article/jekyll.md**
```md
---
layout: category
---
```

**path: ./home/article/jekyll/_posts/2023-05-14-github-pages-구축**
```md
# this article
```

# 4. 전체구조
```
├── 404.html
├── CNAME
├── Gemfile
├── Gemfile.lock
├── _config.yml
├── _data
│   └── main_categories.yml
├── _includes
│   ├── footer.html
│   ├── head.html
│   └── header.html
├── _layouts
│   ├── article.html
│   ├── category.html
│   └── default.html
├── _site
├── assets
│   ├── css
│   │   ├── _site
│   │   │   ├── feed.xml
│   │   │   └── style.css
│   │   ├── igorpro.css
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
│       ├── jekyll
│       │   ├── _drafts
│       │   └── _posts
│       │       └── 2023-05-14-github-pages-구축.md
│       └── jekyll.md
└── index.md
```
{% endraw %}