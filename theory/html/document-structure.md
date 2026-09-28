## II. Структура HTML-документа

### 1. Как выглядит минимальная структура современного HTML-документа?

Базовая структура HTML-документа выглядит так:

```html
<!DOCTYPE html>
<html lang="ru">
  <head>
    <meta charset="UTF-8">
    <title>Название страницы</title>
  </head>

  <body>
    <h1>Заголовок страницы</h1>
  </body>
</html>
```

Основные части документа:

```text
Document
├── DOCTYPE
└── html
    ├── head
    └── body
```

Здесь:

- `<!DOCTYPE html>` — объявление типа документа;
- `<html>` — корневой элемент;
- `<head>` — метаданные документа;
- `<body>` — содержимое страницы.

На практике структура часто дополняется viewport, CSS и JavaScript:

```html
<!DOCTYPE html>
<html lang="ru">
  <head>
    <meta charset="UTF-8">

    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0"
    >

    <title>Frontend Engineering</title>

    <link rel="stylesheet" href="./styles.css">
    <script src="./script.js" defer></script>
  </head>

  <body>
    <main>
      <h1>Frontend Engineering</h1>
    </main>
  </body>
</html>
```

---

### 2. Для чего нужен `<!DOCTYPE html>`?

`<!DOCTYPE html>` — объявление типа документа.

```html
<!DOCTYPE html>
```

В современном HTML его основная задача — указать браузеру использовать **standards mode**, то есть стандартный режим обработки документа.

DOCTYPE:

- располагается перед `<html>`;
- не является HTML-элементом;
- не отображается на странице;
- влияет на режим обработки и рендеринга документа.

Исторически DOCTYPE был связан с DTD и имел более сложный синтаксис. В HTML5 используется короткая форма:

```html
<!DOCTYPE html>
```

Как это выглядело раньше (на примере HTML 4.01 Strict):

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://w3.org">
```

#### Короче:

`<!DOCTYPE html>` нужен для того, чтобы браузер обрабатывал документ в современном стандартном режиме.

---

### 3. Что произойдёт, если не указать DOCTYPE?

Если корректный DOCTYPE отсутствует, браузер может перейти в **quirks mode**.

Quirks mode — режим совместимости со старыми веб-страницами, в котором некоторые правила CSS и layout работают иначе.

Основные режимы:

```text
no-quirks mode
limited-quirks mode
quirks mode
```

В современной разработке требуется стандартный режим — **no-quirks mode**.

Проверить режим документа через JavaScript можно так:

```js
document.compatMode;
```

В standards mode:

```text
CSS1Compat
```

В quirks mode:

```text
BackCompat
```

#### Короче:

Без корректного DOCTYPE браузер может перейти в quirks mode, из-за чего часть CSS и layout будет работать по устаревшим правилам.

---

### 4. Для чего нужен элемент `<html>`?

`<html>` — корневой элемент HTML-документа.

```html
<html lang="ru">
  ...
</html>
```

Он представляет весь HTML-документ и является **document element** в DOM.

Получить его через JavaScript можно так:

```js
document.documentElement;
```

Все основные элементы документа находятся внутри `<html>`.

#### Короче:

`<html>` — корневой элемент HTML-документа и document element в DOM.

---

### 5. Для чего используется атрибут `lang` у `<html>`?

Атрибут `lang` задаёт основной язык содержимого документа.

```html
<html lang="ru">
```

Примеры:

```html
<html lang="en">
```

```html
<html lang="en-GB">
```

Информация о языке используется:

- скринридерами;
- системами синтеза речи;
- переводчиками;
- поисковыми и другими инструментами обработки текста.

Это особенно важно для accessibility, поскольку скринридер может выбрать правильные правила произношения.

Язык можно переопределить для отдельного фрагмента:

```html
<p>
  Слово
  <span lang="en">accessibility</span>
  означает доступность.
</p>
```

#### Короче:

`lang` задаёт основной язык документа и помогает вспомогательным технологиям и другим программам правильно интерпретировать текст.

---

### 6. Чем отличаются `<head>` и `<body>`?

`<head>` и `<body>` выполняют разные функции.

### `<head>`

`<head>` содержит метаданные документа и информацию о связанных ресурсах.

Например:

```html
<head>
  <meta charset="UTF-8">
  <title>Главная страница</title>
  <link rel="stylesheet" href="./styles.css">
</head>
```

### `<body>`

`<body>` содержит основное содержимое страницы:

```html
<body>
  <header>...</header>

  <main>
    <h1>Главная страница</h1>
    <p>Содержимое страницы.</p>
  </main>

  <footer>...</footer>
</body>
```

Упрощённо:

```text
<head> → информация о документе
<body> → содержимое документа
```

---

### 7. Какие элементы обычно располагаются внутри `<head>`?

В `<head>` обычно располагаются:

- `<title>`;
- `<meta>`;
- `<link>`;
- `<style>`;
- `<script>`;
- `<base>`.

Например:

```html
<head>
  <meta charset="UTF-8">

  <meta
    name="viewport"
    content="width=device-width, initial-scale=1.0"
  >

  <meta
    name="description"
    content="Frontend Engineering Knowledge Base"
  >

  <title>Frontend Engineering</title>

  <link rel="icon" href="./favicon.ico">
  <link rel="stylesheet" href="./styles.css">

  <script src="./script.js" defer></script>
</head>
```

`<base>` используется реже и задаёт базовый URL для относительных ссылок:

```html
<base href="https://example.com/">
```

---

### 8. Для чего нужен `<title>`?

Элемент `<title>` задаёт название HTML-документа.

```html
<title>Frontend Engineering</title>
```

Он обычно используется браузером:

- во вкладке;
- в заголовке окна;
- в закладках;
- в других интерфейсах, где нужно обозначить страницу.

`<title>` не следует путать с `<h1>`.

```text
<title> → название документа
<h1>    → заголовок содержимого страницы
```

Например:

```html
<head>
  <title>HTML — Frontend Knowledge Base</title>
</head>

<body>
  <h1>HTML</h1>
</body>
```

---

### 9. Для чего используется `<meta charset="UTF-8">`?

`<meta charset="UTF-8">` объявляет кодировку символов документа.

```html
<meta charset="UTF-8">
```

Кодировка определяет, как последовательность байтов интерпретируется как текст.

UTF-8 позволяет представлять символы Unicode, например:

```text
Привет
Hello
日本語
€
```

Объявление кодировки рекомендуется размещать в начале `<head>`:

```html
<head>
  <meta charset="UTF-8">
  <title>Page</title>
</head>
```

Если кодировка определена неправильно, текст может отображаться некорректно.

Упрощённо:

```text
байты
↓
декодирование UTF-8
↓
символы
↓
HTML parsing
```

#### Короче:

`<meta charset="UTF-8">` сообщает браузеру, в какой кодировке записан HTML-документ.

---

### 10. Для чего нужен `<meta name="viewport">`?

`<meta name="viewport">` управляет настройкой viewport на мобильных устройствах.

Обычно используют:

```html
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0"
>
```

Здесь:

```text
width=device-width
```

задаёт ширину viewport на основе ширины устройства.

```text
initial-scale=1.0
```

задаёт начальный масштаб.

Это важно для адаптивной вёрстки и корректной работы media queries.

Например:

```css
@media (max-width: 768px) {
  .container {
    padding-inline: 20px;
  }
}
```

Ограничивать масштабирование пользователя с помощью `user-scalable=no` или жёсткого `maximum-scale` обычно не рекомендуется, поскольку это может ухудшать accessibility.

#### Короче:

`<meta name="viewport">` настраивает viewport на мобильных устройствах и позволяет адаптивной вёрстке работать относительно ширины устройства.

---

### 11. Что такое favicon и как его подключить?

**Favicon** — иконка, связанная с сайтом или страницей.

Она может отображаться:

- во вкладке браузера;
- в закладках;
- в истории;
- в других элементах интерфейса браузера.

Подключается через `<link>`:

```html
<link rel="icon" href="/favicon.ico">
```

Можно указать формат:

```html
<link
  rel="icon"
  type="image/png"
  href="/favicon.png"
>
```

Или размеры:

```html
<link
  rel="icon"
  type="image/png"
  sizes="32x32"
  href="/favicon-32x32.png"
>
```

---

### 12. Как подключить CSS к HTML?

Основной способ — подключить внешний CSS-файл через `<link>` внутри `<head>`:

```html
<link rel="stylesheet" href="./styles.css">
```

Здесь:

- `rel="stylesheet"` указывает, что ресурс является таблицей стилей;
- `href` содержит URL CSS-файла.

Также CSS можно добавить через `<style>`:

```html
<style>
  body {
    font-family: sans-serif;
  }
</style>
```

или через атрибут `style`:

```html
<p style="color: red;">
  Text
</p>
```

Для обычных проектов предпочтительно использовать внешний CSS-файл.

---

### 13. Как подключить JavaScript к HTML?

JavaScript подключается с помощью элемента `<script>`.

Внешний файл:

```html
<script src="./script.js"></script>
```

JavaScript можно также написать непосредственно внутри элемента:

```html
<script>
  console.log('Hello');
</script>
```

Для внешних скриптов могут использоваться дополнительные атрибуты:

```html
<script src="./script.js" defer></script>
```

```html
<script src="./script.js" async></script>
```

Для ES modules:

```html
<script type="module" src="./main.js"></script>
```

`<script>` не является void element, поэтому закрывающий тег обязателен.

---

### 14. Чем отличаются `async` и `defer` у `<script>`?

Оба атрибута позволяют загружать внешний классический скрипт параллельно с HTML parsing, но отличаются моментом и порядком выполнения.

### `defer`

```html
<script src="./script.js" defer></script>
```

Скрипт:

- загружается параллельно с HTML;
- выполняется после завершения parsing;
- сохраняет порядок относительно других deferred scripts;
- выполняется до `DOMContentLoaded`.

Например:

```html
<script src="./first.js" defer></script>
<script src="./second.js" defer></script>
```

Порядок выполнения:

```text
first.js
↓
second.js
```

### `async`

```html
<script src="./analytics.js" async></script>
```

Скрипт:

- загружается параллельно с HTML;
- выполняется, как только готов;
- может прервать HTML parsing;
- не гарантирует порядок относительно других async scripts.

Например, если второй файл загрузился раньше первого, он может выполниться первым.

### Сравнение

| `defer` | `async` |
| --- | --- |
| Загружается параллельно | Загружается параллельно |
| Выполняется после parsing | Выполняется сразу после загрузки |
| Сохраняет порядок | Порядок не гарантируется |
| Подходит для зависимых скриптов и работы с DOM | Подходит для независимых скриптов |

---

### 15. Где лучше подключать `<script>` и почему?

Выбор зависит от типа скрипта.

Для обычного frontend-скрипта хороший современный вариант — подключение в `<head>` с `defer`:

```html
<head>
  <script src="./script.js" defer></script>
</head>
```

Так браузер может начать загружать JavaScript параллельно с HTML, а выполнить его уже после завершения parsing.

Если используется обычный скрипт без `defer`:

```html
<script src="./script.js"></script>
```

его часто размещают перед закрывающим `</body>`:

```html
<body>
  ...

  <script src="./script.js"></script>
</body>
```

Это уменьшает вероятность того, что скрипт заблокирует parsing в начале документа.

Для независимых сторонних скриптов может использоваться `async`:

```html
<script src="./analytics.js" async></script>
```

ES modules:

```html
<script type="module" src="./main.js"></script>
```

по умолчанию имеют deferred-подобное поведение относительно parsing.