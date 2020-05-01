# Favicon для сайта на GitHub Pages

Просто бросить иконку в "корень" репозитория не получится, т.к. в действительности, это не корень сайта, например: `https://github.com/olexsyn/e-note/`, и браузеры не подхватят ее. Поэтому, лучше прописать к ней путь на странице или в шаблоне:

```html
<link href="{{ site.baseurl }}/favicon.ico" rel="shortcut icon" type="image/png">
```
<small>тут у меня `favicon.ico` в реальности - файл `.png`, поэтому - `image/png`</small>

<span class="r">TODO!</span> разберись с этим!

```html
	<link rel="apple-touch-icon" href="/img/favicons/apple-touch-icon.png" sizes="180x180">
	<link rel="icon" href="/img/favicons/favicon-32x32.png" sizes="32x32" type="image/png">
	<link rel="icon" href="/img/favicons/favicon-16x16.png" sizes="16x16" type="image/png">
	<link rel="manifest" href="/img/favicons/manifest.json">
	<link rel="mask-icon" href="/img/favicons/safari-pinned-tab.svg" color="#563d7c">
	<link rel="icon" href="/img/favicons/favicon.ico">
	<meta name="msapplication-config" content="/img/favicons/browserconfig.xml">
	<meta name="theme-color" content="#563d7c">
```
