---
layout: article
---

# {{ page.title }}

---

1. dependency
2. layouts
3. fragments
4. use layout

---

## 1. dependency

```gradle
...

dependencies {
	implementation 'nz.net.ultraq.thymeleaf:thymeleaf-layout-dialect'
    ...
}

...
```

## 2. layouts

> /templates/layouts/default.html

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org" xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout">
<head th:replace="/fragments/head :: headFragment"></head>
<body>
<header th:replace="/fragments/header :: headerFragment"></header>
<th:block layout:fragment="content"></th:block>
<footer th:replace="/fragments/footer :: footerFragment"></footer>
</body>
</html>
```

## 3. fragments

> /templates/fragments/head.html
> 
> /templates/fragments/header.html
> 
> /templates/fragments/footer.html

**head.html**
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">>
<head th:fragment="headFragment">
    <meta charset="UTF-8">
    <link rel="icon" href="/images/favicon.ico" type="image/x-icon">
    <link rel="stylesheet" href="/css/style.css" type="text/css">
    <title th:text="${@environment.getProperty('project.name')}"></title>
</head>
<body>
</body>
</html>
```

**header.html**
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">>
<body>
<header th:fragment="headerFragment">
  <h1><a th:href="@{/}" th:text="${@environment.getProperty('project.name')}"></a></h1>
</header>
</body>
</html>
```

**footer.html**
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">>
<body>
<footer th:fragment="footerFragment">
    <div>ⓒ<span th:text="${@environment.getProperty('project.copyright')}"></span></div>
</footer>
</body>
</html>
```

## 4. Use layout

> /templates/index.html

{% raw %}
```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org"
      xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout"
      layout:decorate="~{layouts/default}">
<main layout:fragment="content">
  <h1>Main</h1>
</main>
</html>
```
{% endraw %}