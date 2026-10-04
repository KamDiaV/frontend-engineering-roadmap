# I. База CSS

## 1. Что такое CSS и для чего он используется?

**CSS (Cascading Style Sheets)** — язык стилей, который используется для описания **представления HTML-документа**.

HTML определяет структуру и смысл содержимого:

```html
<h1>Frontend</h1>
<p>Изучаем CSS.</p>
```

CSS определяет, как это содержимое должно выглядеть:

```css
h1 {
  font-size: 48px;
}

p {
  color: #555;
}
```

CSS позволяет управлять:

- цветами;
- шрифтами;
- размерами;
- отступами;
- границами;
- фоном;
- расположением элементов;
- адаптивностью;
- анимациями;
- переходами;
- визуальным состоянием интерфейса.

CSS также позволяет адаптировать один HTML-документ под разные условия отображения:

```css
@media (width < 768px) {
  .container {
    padding-inline: 16px;
  }
}
```

Таким образом:

```text
HTML → структура и семантика
CSS  → представление
JS   → поведение и логика
```

### Короче:

CSS — язык стилей для описания внешнего вида и расположения HTML-элементов.

Он отвечает за оформление, layout, адаптивность, состояния, переходы и анимации интерфейса.

---

## 2. Что означает Cascading Style Sheets?

**Cascading Style Sheets** переводится как:

> каскадные таблицы стилей.

Слово **Cascading** здесь особенно важно.

Один элемент может одновременно получать стили из разных источников:

```css
p {
  color: black;
}

.article p {
  color: blue;
}

#intro {
  color: red;
}
```

Браузеру необходимо определить, какое значение `color` в итоге использовать.

Для этого существует **cascade algorithm**.

Он учитывает, среди прочего:

- происхождение стиля;
- `!important`;
- cascade layers;
- specificity;
- scoping proximity;
- порядок объявления.

То есть CSS называется **каскадным**, потому что несколько потенциальных значений одного свойства проходят через систему приоритетов, после чего браузер выбирает итоговое значение.

### Короче:

Cascading Style Sheets означает «каскадные таблицы стилей».

«Cascading» относится к алгоритму, который определяет, какое из конкурирующих CSS-значений должно применяться к элементу.

---

## 3. Как CSS связан с HTML?

HTML создаёт структуру документа:

```html
<article class="card">
  <h2 class="card__title">
    CSS
  </h2>

  <p>
    Cascading Style Sheets
  </p>
</article>
```

CSS обращается к элементам этой структуры с помощью **селекторов**:

```css
.card {
  padding: 24px;
}

.card__title {
  font-size: 32px;
}
```

Упрощённо:

```text
HTML
↓
DOM

CSS
↓
CSSOM

DOM + информация о стилях
↓
rendering
```

HTML определяет:

> какие элементы существуют и как они связаны.

CSS определяет:

> как эти элементы должны быть представлены.

Браузер парсит HTML в DOM, CSS — в CSSOM, вычисляет стили элементов и использует эти данные при layout и rendering страницы.

---

## 4. Какими способами можно подключить CSS к HTML?

Существует три основных способа.

### 1. External CSS

Отдельный `.css`-файл:

```html
<link
  rel="stylesheet"
  href="styles.css"
>
```

```css
body {
  margin: 0;
}
```

Это основной способ для обычных проектов.

---

### 2. Internal CSS

CSS помещается внутри `<style>`:

```html
<head>
  <style>
    body {
      margin: 0;
    }
  </style>
</head>
```

---

### 3. Inline CSS

CSS указывается непосредственно в атрибуте `style`:

```html
<p style="color: red;">
  Text
</p>
```

Все три варианта относятся к **author styles** — стилям автора страницы.

---

## 5. Чем inline, internal и external CSS отличаются друг от друга?

### External CSS

```html
<link rel="stylesheet" href="styles.css">
```

CSS находится в отдельном файле.

Преимущества:

- переиспользуется на нескольких страницах;
- легче поддерживать;
- HTML и CSS разделены;
- файл может кэшироваться браузером.

---

### Internal CSS

```html
<style>
  p {
    color: red;
  }
</style>
```

CSS находится внутри HTML-документа.

Подходит, например, для небольших автономных страниц или специальных случаев.

---

### Inline CSS

```html
<p style="color: red;">
  Text
</p>
```

Стиль задаётся непосредственно элементу.

Он:

- плохо масштабируется;
- смешивает структуру и представление;
- усложняет поддержку;
- имеет высокий приоритет среди обычных author declarations.

Важно:

> нельзя просто утверждать, что inline CSS «всегда сильнее».

Каскад сначала учитывает origin, importance, layers и другие уровни. Например, пользовательский `!important` может иметь более высокий приоритет, чем author inline style.

---

## 6. Как браузер применяет CSS к HTML-документу?

Упрощённый процесс выглядит так:

```text
HTML
↓
DOM

CSS
↓
CSSOM

DOM + CSSOM
↓
style calculation
↓
layout
↓
paint
↓
compositing
```

### 1. Parsing HTML

Браузер разбирает HTML и строит **DOM**.

### 2. Parsing CSS

CSS разбирается и преобразуется во внутреннее представление стилей, обычно называемое **CSSOM**.

### 3. Selector matching

Браузер определяет, какие CSS-правила подходят каждому элементу.

Например:

```css
.card p {
  color: red;
}
```

применяется только к подходящим `<p>`.

### 4. Cascade

Если несколько declarations задают одно свойство:

```css
p {
  color: red;
}

.text {
  color: blue;
}
```

браузер применяет алгоритм каскада.

### 5. Inheritance

Некоторые значения могут наследоваться от родителя.

### 6. Computed styles

Для каждого элемента браузер определяет итоговые значения свойств.

### 7. Layout

Рассчитываются размеры и положение элементов.

### 8. Paint

Элементы рисуются.

### 9. Compositing

Некоторые нарисованные слои объединяются для итогового отображения страницы.

---

## 7. Что такое CSS rule?

**CSS rule**, или CSS-правило, — конструкция, которая связывает набор CSS declarations с элементами, подходящими под selector.

Например:

```css
.card {
  padding: 20px;
  background-color: white;
}
```

Здесь всё выражение:

```css
.card {
  padding: 20px;
  background-color: white;
}
```

является **qualified rule**.

В повседневной речи его обычно называют просто CSS rule.

Важно: в CSS существуют и другие виды правил, например at-rules:

```css
@media (width < 768px) {
  ...
}
```

```css
@layer components {
  ...
}
```

### Короче:

CSS rule связывает selector с блоком CSS declarations:

```css
selector {
  property: value;
}
```

---

## 8. Из каких частей состоит CSS-правило?

Обычное style rule состоит из:

```text
selector
+
declaration block
```

Например:

```css
.button {
  color: white;
  background-color: black;
}
```

Здесь:

```text
.button
```

— selector.

А:

```css
{
  color: white;
  background-color: black;
}
```

— declaration block.

Внутри него находятся declarations:

```css
color: white;
```

Каждая declaration состоит из:

```text
property : value
```

То есть:

```text
CSS rule
├── selector
└── declaration block
    ├── declaration
    │   ├── property
    │   └── value
    └── declaration
        ├── property
        └── value
```

---

## 9. Что такое selector?

**Selector** — часть CSS-правила, определяющая, к каким элементам применяется правило.

Например:

```css
p {
  color: red;
}
```

Selector:

```css
p
```

находит элементы `<p>`.

Пример class selector:

```css
.card {
  padding: 20px;
}
```

Пример ID selector:

```css
#header {
  ...
}
```

Пример attribute selector:

```css
input[type="email"] {
  ...
}
```

Пример составного selector:

```css
.article > p:first-child {
  ...
}
```

Selector отвечает на вопрос:

> какие элементы должны получить эти declarations?

---

## 10. Что такое declaration?

**CSS declaration** — запись, которая задаёт значение конкретного CSS-свойства.

Например:

```css
color: red;
```

Она состоит из:

```text
property → color
value    → red
```

В declaration block может находиться несколько declarations:

```css
.card {
  color: black;
  padding: 20px;
  border-radius: 8px;
}
```

Здесь три declarations:

```css
color: black;
padding: 20px;
border-radius: 8px;
```

---

## 11. Что такое property?

**Property** — CSS-свойство, определяющее, какую характеристику элемента нужно изменить.

Например:

```css
color: red;
```

`color` — property.

Другие примеры:

```css
font-size
margin
padding
width
display
background-color
position
```

Каждое property имеет:

- допустимый набор значений;
- initial value;
- правила inheritance;
- определённое поведение при вычислении.

Например:

```css
width: 300px;
```

```text
property → width
value    → 300px
```

---

## 12. Что такое value?

**Value** — значение CSS-property.

Например:

```css
color: red;
```

```text
property → color
value    → red
```

Значения могут иметь разные типы.

Например:

```css
width: 300px;
```

```css
opacity: 0.5;
```

```css
display: grid;
```

```css
color: rgb(20 20 20);
```

```css
width: 50%;
```

```css
margin: calc(1rem + 10px);
```

Некоторые properties принимают несколько компонентов значения:

```css
border: 1px solid black;
```

Здесь значение shorthand-property состоит из нескольких частей.

---

## 13. Что такое stylesheet?

**Stylesheet** — набор CSS-правил, используемых для стилизации документа.

Например, файл:

```text
styles.css
```

может содержать:

```css
body {
  margin: 0;
}

h1 {
  font-size: 48px;
}

.button {
  padding: 12px 20px;
}
```

Stylesheet может поступать из разных источников:

```text
author stylesheet
user stylesheet
user-agent stylesheet
```

Также author stylesheet может быть:

```html
<link rel="stylesheet" href="styles.css">
```

или:

```html
<style>
  ...
</style>
```

Stylesheets участвуют в CSS cascade.

---

## 14. Что такое user agent stylesheet?

**User agent stylesheet** — встроенные стили браузера.

Именно поэтому HTML без собственного CSS всё равно имеет некоторое оформление.

Например:

```html
<h1>Heading</h1>

<p>Paragraph</p>
```

обычно визуально отличаются.

Браузер может иметь правила, концептуально похожие на:

```css
h1 {
  display: block;
  font-size: 2em;
  font-weight: bold;
}

p {
  display: block;
}
```

Это объясняет, почему:

- заголовки выглядят крупнее;
- `<strong>` обычно жирный;
- ссылки имеют характерное оформление;
- списки имеют отступы;
- `<div>` ведёт себя как block-level box.

Важно отличать:

```text
initial value CSS-property
```

и:

```text
user-agent default style
```

Например, initial value свойства `display` — `inline`, но браузерская таблица стилей задаёт `<div>` поведение `block`. Поэтому `display: initial` и `display: revert` могут дать разные результаты.

---

## 15. Что такое inheritance в CSS?

**Inheritance** — механизм, при котором некоторые CSS-properties получают значение от родительского элемента, если собственное значение для элемента не было задано.

Например:

```css
body {
  color: #333;
}
```

```html
<body>
  <p>
    Hello <strong>world</strong>
  </p>
</body>
```

`color` наследуется, поэтому текст внутри `<p>` и `<strong>` обычно получает цвет родителя.

Но наследуются не все свойства.

Например:

```css
.parent {
  margin: 50px;
}
```

ребёнок не получает:

```css
margin: 50px;
```

автоматически.

Для inherited property, если значение не задано, используется **computed value родителя**.

Для non-inherited property обычно используется initial value свойства.

---

## 16. Какие свойства наследуются по умолчанию, а какие нет?

CSS-properties имеют собственное правило:

```text
Inherited: yes
```

или:

```text
Inherited: no
```

### Обычно наследуются свойства, связанные с текстом

Например:

```css
color
font-family
font-size
font-style
font-weight
line-height
text-align
letter-spacing
word-spacing
visibility
```

Например:

```css
body {
  font-family: Arial, sans-serif;
  color: #333;
}
```

Большая часть текста внутри `body` наследует эти значения.

---

### Обычно не наследуются свойства layout и box model

Например:

```css
margin
padding
border
width
height
background
display
position
top
right
bottom
left
box-sizing
overflow
```

Например:

```css
.parent {
  padding: 50px;
  background: red;
}
```

Ребёнок не получает автоматически:

```css
padding: 50px;
background: red;
```

Общее практическое правило:

```text
типографика → часто наследуется
layout / box model → обычно не наследуется
```

Но это только ориентир.

---

## 17. Что означают значения `inherit`, `initial`, `unset` и `revert`?

Это **CSS-wide keywords**, которые можно применять к CSS-properties.

---

### `inherit`

Принудительно берёт computed value свойства у родительского элемента.

```css
.child {
  color: inherit;
}
```

Работает даже для свойств, которые обычно не наследуются:

```css
.child {
  border: inherit;
}
```


---

### `initial`

Устанавливает **начальное значение CSS-свойства (initial value)**, определённое спецификацией CSS, независимо от того, какое значение обычно назначает этому элементу браузер.

```css
.element {
  display: initial;
}
```

**Важно:** начальное значение свойства и стандартный браузерный стиль HTML-элемента — не одно и то же.

Например, для свойства `display` начальное значение — `inline`. При этом браузер по умолчанию задаёт элементу `<div>` значение `block` через встроенную таблицу стилей (User Agent Stylesheet).

Поэтому:

```css
div {
  display: initial;
}
```

приведёт к тому, что `<div>` получит `display: inline`, а не привычное для него `display: block`.

Таким образом, **`initial` возвращает свойство к значению из спецификации CSS, а не к стандартному оформлению конкретного HTML-элемента.**

---

### `unset`

Работает по-разному в зависимости от свойства:

```text
если property наследуемое
→ inherit

если property ненаследуемое
→ initial
```

Например:

```css
.element {
  color: unset;
}
```

`color` наследуется, поэтому будет взят цвет родителя.

Но:

```css
.element {
  margin: unset;
}
```

`margin` не наследуется, поэтому будет использовано initial value.

---

### `revert`

Откатывает значение так, как если бы стили **текущего cascade origin** не задавали это свойство.

Например, в author stylesheet:

```css
button {
  all: revert;
}
```

может вернуть браузерские или пользовательские значения, которые существовали до author styles.

Это отличается от:

```css
initial
```

потому что `revert` может вернуться к user-agent stylesheet.

Например, browser default для `<button>` не обязательно совпадает с initial values отдельных CSS-properties.

Короче:

```text
inherit
→ значение родителя

initial
→ initial value из CSS specification

unset
→ inherit или initial

revert
→ откат текущего cascade origin
```

---

## 18. Что такое cascade в CSS?

**Cascade** — алгоритм, который определяет, какое значение CSS-property применяется, если для одного элемента существует несколько конкурирующих declarations.

Например:

```css
p {
  color: red;
}

.text {
  color: blue;
}
```

```html
<p class="text">
  Hello
</p>
```

Оба правила задают `color`.

Браузер должен выбрать одно.

Для этого используется cascade algorithm.

Современный CSS cascade учитывает:

```text
1. relevance
2. origin и importance
3. cascade layers
4. specificity
5. scoping proximity
6. source order
```

Кроме того, особое место в каскаде занимают:

- CSS animations;
- CSS transitions.

Важно:

> specificity — только один из этапов cascade.

Нельзя сводить каскад к правилу «самый специфичный selector всегда выигрывает».

Например, декларация из более приоритетного cascade origin может победить более специфичный selector из менее приоритетного origin.

### Короче:

Cascade — алгоритм выбора итогового значения CSS-свойства среди нескольких конкурирующих declarations.

Он учитывает origin, importance, layers, specificity, scope proximity и source order.

---

## 19. По каким правилам браузер выбирает итоговое значение свойства?

Современный cascade algorithm можно представить как последовательность фильтров.

### 1. Relevance

Сначала остаются только declarations, которые вообще применимы.

Например:

```css
@media (width < 600px) {
  p {
    color: red;
  }
}
```

при ширине 1200px не участвует в выборе.

Selector также должен соответствовать элементу.

---

### 2. Origin и importance

CSS может происходить из разных origins:

```text
user-agent
user
author
```

Также учитывается `!important`.

Упрощённый порядок от меньшего к большему:

```text
normal user-agent
normal user
normal author
CSS animations
author !important
user !important
user-agent !important
CSS transitions
```

Важно:

```text
!important
```

меняет порядок origins: пользовательские important styles имеют приоритет над author `!important`.

Это важно для accessibility — пользователь должен иметь возможность переопределять некоторые стили сайта.

---

### 3. Cascade layers

Внутри origin учитываются:

```css
@layer
```

Например:

```css
@layer reset, components, utilities;
```

Для обычных declarations более поздний layer имеет более высокий приоритет.

Unlayered normal author styles имеют более высокий приоритет, чем normal declarations внутри layers.

Для `!important` порядок layers инвертируется.

---

### 4. Specificity

Если declarations всё ещё конкурируют, сравнивается specificity selectors.

Например:

```css
p {
  color: red;
}

.article p {
  color: blue;
}
```

`.article p` имеет большую specificity.

Но specificity сравнивается только после предыдущих уровней каскада.

---

### 5. Scoping proximity

Если используются:

```css
@scope
```

и specificity одинакова, может учитываться расстояние до scope root.

Правило, scope root которого ближе к элементу, получает преимущество.

---

### 6. Source order

Если предыдущие условия равны, выигрывает declaration, расположенная позже.

```css
p {
  color: red;
}

p {
  color: blue;
}
```

Итог:

```text
blue
```

---

### Важно: inheritance

Inheritance используется не как способ «победить» явную declaration.

Если непосредственно к элементу применяется подходящее значение свойства, оно имеет приоритет над наследуемым значением.

### Короче:

Браузер последовательно учитывает:

```text
relevance
→ origin + importance
→ cascade layers
→ specificity
→ scoping proximity
→ source order
```

Specificity и «последнее правило» работают только после более приоритетных этапов каскада.

---

## 20. Что такое source order и когда он влияет на стили?

**Source order** — порядок, в котором CSS declarations располагаются в таблицах стилей.

Классический пример:

```css
.text {
  color: red;
}

.text {
  color: blue;
}
```

Оба selectors:

- подходят одному элементу;
- имеют одинаковую specificity;
- находятся в одинаковом origin;
- имеют одинаковую importance;
- находятся на одинаковом уровне cascade layers;
- имеют одинаковую scoping proximity.

Поэтому выигрывает объявленное позже:

```css
color: blue;
```

Это часто описывают правилом:

> при прочих равных побеждает последнее объявление.

Но утверждение:

> «в CSS всегда побеждает правило, которое написано ниже»

неверно.

Например:

```css
#title {
  color: red;
}

.title {
  color: blue;
}
```

Несмотря на то что `.title` находится ниже, `#title` имеет более высокую specificity.

Ещё важнее: более высокий cascade origin, importance или layer может решить конфликт **до того, как браузер вообще перейдёт к source order**.

Поэтому source order — это фактически **последний tie-breaker** каскада.