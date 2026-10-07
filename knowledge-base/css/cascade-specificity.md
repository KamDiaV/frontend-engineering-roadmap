# III. Специфичность и каскад

## 1. Что такое specificity?

**Specificity (специфичность)** — это вес CSS-селектора, который браузер использует при разрешении конфликтов между несколькими CSS-объявлениями, применимыми к одному и тому же элементу и свойству.

Например:

```css
p {
  color: red;
}

.text {
  color: blue;
}
```

HTML:

```html
<p class="text">Hello</p>
```

К одному элементу подходят два правила:

```css
p {
  color: red;
}
```

и:

```css
.text {
  color: blue;
}
```

Оба задают одно и то же свойство:

```css
color
```

Браузеру необходимо определить, какое значение использовать.

Селектор класса `.text` имеет более высокую специфичность, чем селектор элемента `p`, поэтому итоговым будет:

```css
color: blue;
```

### Важно: specificity — только часть каскада

Нельзя считать, что CSS всегда просто выбирает «самый специфичный селектор».

Specificity сравнивается только после более важных этапов каскада.

Упрощённо современный CSS Cascade работает так:

```text
1. Relevance
      ↓
2. Origin + Importance
      ↓
3. Cascade Layers
      ↓
4. Specificity
      ↓
5. Scoping Proximity
      ↓
6. Source Order
```

То есть браузер сначала определяет:

- применимо ли правило;
- откуда оно происходит;
- является ли оно `!important`;
- в каком cascade layer оно находится;

и только после этого при необходимости сравнивает specificity.

Например, правило с очень высокой specificity может проиграть правилу из более приоритетного cascade layer.

---

## 2. Как рассчитывается специфичность CSS-селектора?

В современной модели specificity обычно представляют тремя группами:

```text
ID – CLASS – TYPE
```

Например:

```text
1-2-3
```

означает:

```text
1 ID-селектор
2 селектора уровня CLASS
3 селектора уровня TYPE
```

Браузер подсчитывает компоненты селектора в каждой категории.

---

### Первая колонка — ID

Сюда относятся ID-селекторы:

```css
#header
#app
#navigation
```

Каждый ID добавляет:

```text
1-0-0
```

Например:

```css
#header {
}
```

имеет specificity:

```text
1-0-0
```

---

### Вторая колонка — CLASS

Сюда относятся:

- селекторы классов;
- селекторы атрибутов;
- большинство псевдоклассов.

Например:

```css
.card
```

```text
0-1-0
```

Селектор атрибута:

```css
[type="email"]
```

```text
0-1-0
```

Псевдокласс:

```css
:hover
```

```text
0-1-0
```

Комбинация:

```css
.button:hover
```

содержит:

```text
.button → 0-1-0
:hover  → 0-1-0
```

Итого:

```text
0-2-0
```

---

### Третья колонка — TYPE

Сюда относятся:

- селекторы элементов;
- псевдоэлементы.

Например:

```css
p
```

имеет:

```text
0-0-1
```

Псевдоэлемент:

```css
::before
```

также добавляет:

```text
0-0-1
```

Поэтому:

```css
p::before
```

имеет specificity:

```text
0-0-2
```

---

### Примеры расчёта

#### Пример 1

```css
p
```

```text
0-0-1
```

---

#### Пример 2

```css
.card
```

```text
0-1-0
```

---

#### Пример 3

```css
.card p
```

Здесь:

```text
.card → 0-1-0
p     → 0-0-1
```

Итого:

```text
0-1-1
```

---

#### Пример 4

```css
.card.active p
```

Здесь:

```text
.card   → 0-1-0
.active → 0-1-0
p       → 0-0-1
```

Итого:

```text
0-2-1
```

---

#### Пример 5

```css
#app .card p
```

Здесь:

```text
#app  → 1-0-0
.card → 0-1-0
p     → 0-0-1
```

Итого:

```text
1-1-1
```

---

### Что не увеличивает specificity?

#### Универсальный селектор `*`

```css
*
```

имеет:

```text
0-0-0
```

#### Комбинаторы

Например:

```css
>
+
~
```

и пробел между descendant-селекторами сами по себе specificity не добавляют.

Поэтому:

```css
.card > p
```

имеет такую же specificity по компонентам, как:

```css
.card p
```

То есть:

```text
0-1-1
```

### Как сравнивается specificity?

Колонки сравниваются **слева направо**.

Например:

```text
1-0-0
```

выше, чем:

```text
0-100-100
```

потому что сначала сравнивается количество ID.

То есть нельзя считать specificity обычным десятичным числом.

Правильно:

```text
ID важнее CLASS
CLASS важнее TYPE
```

а не:

```text
100 классов = 1 ID
```

Такого правила в CSS нет.

---

## 3. Что имеет больший приоритет: ID, class или element selector?

С точки зрения specificity:

```text
ID > CLASS > TYPE
```

То есть:

```text
#id     → 1-0-0
.class  → 0-1-0
element → 0-0-1
```

Например:

```css
p {
  color: red;
}

.text {
  color: blue;
}

#intro {
  color: green;
}
```

HTML:

```html
<p id="intro" class="text">
  Hello
</p>
```

Все три правила подходят одному элементу.

Их specificity:

```text
p       → 0-0-1
.text   → 0-1-0
#intro  → 1-0-0
```

Поэтому при прочих равных победит:

```css
#intro {
  color: green;
}
```

Итог:

```text
green
```

### Но важно помнить о каскаде

Фраза:

> ID всегда побеждает class.

слишком упрощённая.

Правильнее:

> ID имеет более высокую specificity, чем class, если сравниваемые объявления находятся на одном соответствующем уровне каскада.

Например, правило класса из более приоритетного cascade layer может победить правило с ID из менее приоритетного layer.

Поэтому specificity нельзя рассматривать отдельно от CSS Cascade.

---

## 4. Как inline styles влияют на специфичность?

**Inline styles** — CSS-объявления, записанные непосредственно в атрибуте `style` HTML-элемента.

Например:

```html
<p style="color: red;">
  Hello
</p>
```

Здесь:

```css
color: red;
```

является inline style.

Предположим, также существует CSS:

```css
#text {
  color: blue;
}
```

HTML:

```html
<p
  id="text"
  style="color: red;"
>
  Hello
</p>
```

Обычный inline style получит приоритет над обычным author-правилом из stylesheet:

```text
red
```

даже несмотря на ID-селектор.

---

### Является ли inline style частью specificity?

Технически `style=""` не является CSS-селектором, поэтому его нельзя буквально посчитать в системе:

```text
ID – CLASS – TYPE
```

Однако в учебных материалах часто используют условное представление:

```text
inline – ID – CLASS – TYPE
```

и говорят, что inline style имеет вес:

```text
1-0-0-0
```

а ID:

```text
0-1-0-0
```

Это удобно как мнемоника, но важно понимать:

> inline style имеет специальное место в каскаде и не является ещё одной категорией CSS-селектора.

Обычные inline author styles имеют приоритет над обычными author declarations из stylesheet, включая layered и unlayered author CSS.

### Например

```html
<p
  id="text"
  style="color: red;"
>
  Hello
</p>
```

```css
#text {
  color: blue;
}
```

Итог:

```text
red
```

### Но inline style не является абсолютным максимумом

Например:

```css
#text {
  color: blue !important;
}
```

может победить обычный inline style:

```html
<p
  id="text"
  style="color: red;"
>
  Hello
</p>
```

Потому что `!important` переводит объявление на другой уровень каскада.

---

## 5. Как `!important` влияет на каскад?

`!important` — специальный флаг CSS declaration, повышающий его **importance** в алгоритме каскада.

Синтаксис:

```css
.button {
  color: red !important;
}
```

`!important` записывается после значения свойства:

```css
property: value !important;
```

Например:

```css
color: red !important;
```

---

### `!important` не увеличивает specificity

Это принципиально важно.

Например:

```css
.text {
  color: red !important;
}

#intro {
  color: blue;
}
```

HTML:

```html
<p id="intro" class="text">
  Hello
</p>
```

Несмотря на то что:

```text
#intro → 1-0-0
.text  → 0-1-0
```

победит:

```css
color: red !important;
```

Причина не в том, что `.text` получил большую specificity.

Причина в том, что `!important` обрабатывается **до specificity** на более высоком этапе CSS Cascade.

То есть:

```text
importance
     ↓
specificity
```

а не наоборот.

---

### Что если оба объявления имеют `!important`?

Например:

```css
.text {
  color: red !important;
}

#intro {
  color: blue !important;
}
```

Теперь оба объявления являются important.

Если они находятся в одинаковом origin и cascade layer, браузер снова сравнивает specificity.

Тогда победит:

```css
#intro {
  color: blue !important;
}
```

поскольку:

```text
#intro → 1-0-0
.text  → 0-1-0
```

---

### Origin тоже имеет значение

CSS может происходить из разных источников:

```text
User Agent
User
Author
```

`Author` — CSS разработчика сайта.

`User` — стили пользователя.

`User Agent` — стили браузера.

user-agent styles → Chrome / Safari / Firefox
user styles       → стили, заданные самим пользователем
author styles     → твой CSS проекта

Для important declarations порядок origin отличается от обычных declarations.

Например:

```text
author !important
       <
user !important
       <
user-agent !important
```

Это важно, в частности, для accessibility: пользователь должен иметь возможность переопределять стили сайта своими важными правилами.

### CSS Transitions

Во время активного CSS Transition переходящее значение имеет ещё более высокий каскадный приоритет, чем important declarations.

Это специальный случай современного CSS Cascade.

---

## 6. Почему чрезмерное использование `!important` считается плохой практикой?

`!important` сам по себе не является ошибкой CSS.

Проблема возникает при его использовании как постоянного способа решения конфликтов.

Например:

```css
.button {
  color: red !important;
}
```

Позже требуется изменить цвет:

```css
.button--primary {
  color: blue;
}
```

Но новое правило не работает, потому что предыдущий `color` имеет `!important`.

Разработчик может добавить ещё один `!important`:

```css
.button--primary {
  color: blue !important;
}
```

Затем появляется другое правило:

```css
.header .button--primary {
  color: green !important;
}
```

Так постепенно возникает **specificity war** — постоянное увеличение силы CSS-правил.

### Основные проблемы чрезмерного `!important`

#### 1. Усложняет переопределение

Обычные правила больше не могут изменить значение.

#### 2. Нарушает естественный каскад

CSS специально спроектирован так, чтобы правила можно было переопределять посредством:

- структуры stylesheet;
- specificity;
- source order;
- cascade layers.

Постоянный `!important` обходит часть этой архитектуры.

#### 3. Приводит к цепочке новых `!important`

Для переопределения important declaration часто приходится создавать другое important declaration.

#### 4. Усложняет отладку

Разработчику становится труднее определить, почему конкретное значение победило.

#### 5. Ухудшает масштабируемость CSS

В большом проекте множество important declarations создают трудноуправляемую систему зависимостей.

MDN рекомендует рассматривать `!important` как инструмент для специальных случаев, а не как стандартный способ повышения приоритета.

### Когда `!important` может быть оправдан?

Например:

- необходимо гарантированно установить критическое utility-состояние;
- приходится переопределять внешние стили, архитектуру которых невозможно изменить;
- создаются специальные accessibility/user styles;
- используется заранее продуманная архитектура important rules.

Но прежде обычно стоит проверить:

```text
Можно ли решить проблему:
→ source order?
→ более подходящим selector?
→ архитектурой компонентов?
→ cascade layer?
```

Особенно для сторонних библиотек современные cascade layers часто являются более удобным решением, чем наращивание specificity или использование `!important`.

---

## 7. Что произойдёт, если два правила имеют одинаковую специфичность?

Если два CSS-объявления имеют одинаковую specificity, браузер продолжает выполнять следующие этапы каскада.

В обычной ситуации, если все остальные параметры одинаковы, побеждает правило, объявленное позже.

Например:

```css
.text {
  color: red;
}

.text {
  color: blue;
}
```

Оба селектора имеют:

```text
0-1-0
```

Итог:

```text
blue
```

Потому что второе объявление находится позже.

Это называется **Source Order**.

---

### Более точная модель 2026 года

Одинаковой specificity недостаточно, чтобы сразу перейти к source order.

Современный каскад также учитывает **Scoping Proximity**, если используются правила `@scope`.

Упрощённо:

```text
Specificity одинаковая?
        ↓
Scoping Proximity
        ↓
Source Order
```

Если `@scope` не используется или scoping proximity одинакова, выигрывает более позднее объявление.

### Например

```css
.title {
  color: red;
}

.title {
  color: green;
}

.title {
  color: blue;
}
```

Все три правила имеют:

```text
0-1-0
```

Поэтому при прочих равных применяется:

```css
color: blue;
```

### Главное правило

Не:

> В CSS всегда побеждает последнее правило.

А:

> Последнее правило побеждает только тогда, когда более приоритетные параметры каскада не разрешили конфликт раньше.

---

## 8. Как наследование взаимодействует с каскадом?

**Inheritance (наследование)** — механизм, при котором некоторые CSS-свойства получают вычисленное значение соответствующего свойства родительского элемента.

Например:

```css
body {
  color: green;
}
```

HTML:

```html
<body>
  <h1>Hello</h1>
</body>
```

`color` является наследуемым свойством.

Если у `<h1>` нет собственного значения `color`, он может унаследовать:

```text
green
```

от родителя.

---

### Что происходит сначала: cascade или inheritance?

Сначала браузер рассматривает объявления, которые непосредственно применяются к элементу.

Если для свойства нет подходящего собственного значения и свойство наследуется, используется значение родителя.

Упрощённо:

```text
Declarations
     ↓
Cascade
     ↓
Есть собственное значение?
     ↓
   да → использовать его

   нет
     ↓
свойство наследуется?
     ↓
   да → взять computed value родителя
   нет → использовать initial value
```

---

### Собственное правило сильнее наследуемого

Рассмотрим:

```css
#parent {
  color: green;
}

h1 {
  color: purple;
}
```

HTML:

```html
<div id="parent">
  <h1>Hello</h1>
</div>
```

У родительского правила очень высокая specificity:

```text
#parent → 1-0-0
```

У:

```css
h1
```

только:

```text
0-0-1
```

Но `<h1>` будет:

```text
purple
```

Почему?

Потому что:

```css
h1 {
  color: purple;
}
```

непосредственно задаёт `color` самому `<h1>`.

А:

```css
#parent {
  color: green;
}
```

задаёт значение родителю, которое `<h1>` мог бы только унаследовать.

Непосредственно заданное элементу значение имеет приоритет над наследуемым значением независимо от specificity правила на предке.

---

### Ключевое слово `inherit`

Наследование можно вызвать принудительно:

```css
.child {
  color: inherit;
}
```

Тогда элемент получает computed value свойства `color` родительского элемента.

`inherit` можно использовать даже для свойств, которые обычно не наследуются:

```css
.child {
  border: inherit;
}
```


### Главное различие

```text
Cascade
→ выбирает значение среди конкурирующих declarations.

Inheritance
→ помогает определить значение, когда оно должно быть получено от родителя.
```

Это разные механизмы, хотя оба участвуют в определении итогового CSS-значения.

---

## 9. Как `:is()`, `:not()` и `:has()` влияют на специфичность?

Функциональные псевдоклассы:

```css
:is()
:not()
:has()
```

имеют особые правила specificity.

Сам псевдокласс не добавляет обычный вес:

```text
0-1-0
```

как большинство других псевдоклассов.

Вместо этого specificity определяется наиболее специфичным селектором в его списке аргументов.

---

### `:is()`

Например:

```css
:is(p, .text, #intro)
```

Аргументы имеют:

```text
p      → 0-0-1
.text  → 0-1-0
#intro → 1-0-0
```

Наибольшая specificity:

```text
1-0-0
```

Поэтому:

```css
:is(p, .text, #intro)
```

имеет:

```text
1-0-0
```

---

### `:not()`

Например:

```css
:not(.disabled, #hidden)
```

Аргументы:

```text
.disabled → 0-1-0
#hidden   → 1-0-0
```

Наибольшее значение:

```text
1-0-0
```

Поэтому specificity:

```text
1-0-0
```

---

### `:has()`

Например:

```css
.card:has(#image)
```

Сначала:

```text
.card → 0-1-0
```

Аргумент `:has()`:

```text
#image → 1-0-0
```

Итого:

```text
1-1-0
```

---

### Более сложный пример

```css
article:is(.post, #featured) p
```

Состав:

```text
article              → 0-0-1
:is(.post, #featured) → 1-0-0
p                    → 0-0-1
```

Итого:

```text
1-0-2
```

Потому что внутри `:is()` наибольшую specificity имеет:

```css
#featured
```

### Почему это важно?

Можно случайно значительно увеличить specificity.

Например:

```css
:is(.card, #special) {
  color: red;
}
```

Даже наличие одного ID в списке делает specificity этого `:is()` высокой:

```text
1-0-0
```

Поэтому `:is()`, `:not()` и `:has()` следует использовать с пониманием их влияния на каскад.

---

## 10. Почему `:where()` имеет нулевую специфичность?

`:where()` внешне очень похож на `:is()`.

Например:

```css
:where(h1, h2, h3) {
  margin: 0;
}
```

Но у него есть специальное правило:

> specificity самого `:where()` и всех селекторов внутри его аргумента всегда равна `0-0-0`.

Например:

```css
:where(#app, .card, article)
```

Несмотря на наличие:

```css
#app
```

specificity всего `:where()`:

```text
0-0-0
```

---

### Сравним `:is()` и `:where()`

```css
:is(#app, .card) {
  color: red;
}
```

Specificity:

```text
1-0-0
```

А:

```css
:where(#app, .card) {
  color: red;
}
```

Specificity:

```text
0-0-0
```

---

### Зачем это сделано?

Чтобы можно было создавать удобные общие CSS-правила, которые легко переопределяются.

Например:

```css
:where(h1, h2, h3) {
  margin: 0;
}
```

Теперь:

```css
.title {
  margin: 20px;
}
```

легко переопределит базовый стиль.

### Где полезен `:where()`?

Например:

- CSS Reset;
- базовые стили;
- стили библиотек;
- дизайн-системы;
- стили компонентов, которые пользователь должен легко переопределять.

Например:

```css
:where(.article) h2 {
  margin-block: 1em;
}
```

Здесь `.article` внутри `:where()` не увеличивает specificity.

Specificity определяется только:

```css
h2
```

то есть:

```text
0-0-1
```

Нулевая specificity `:where()` предусмотрена специально для управления каскадом.

---

## 11. Что такое Cascade Layers (`@layer`)?

**Cascade Layers** — механизм CSS, позволяющий разделять CSS-правила на слои и явно задавать приоритет между группами стилей.

Для этого используется at-rule:

```css
@layer
```

Cascade Layers поддерживаются основными современными браузерами и являются широко доступной возможностью CSS.

---

### Создание слоя

Например:

```css
@layer reset {
  * {
    margin: 0;
    padding: 0;
  }
}
```

Создан слой:

```text
reset
```

---

### Можно заранее объявить порядок слоёв

```css
@layer reset, base, components, utilities;
```

Здесь порядок обычных declarations:

```text
reset
  ↓
base
  ↓
components
  ↓
utilities
```

Для **обычных** declarations более поздний слой имеет более высокий приоритет.

То есть:

```text
utilities > components > base > reset
```

---

### Пример

```css
@layer base, components;

@layer base {
  #button {
    color: red;
  }
}

@layer components {
  .button {
    color: blue;
  }
}
```

HTML:

```html
<button
  id="button"
  class="button"
>
  Save
</button>
```

Если смотреть только на specificity:

```text
#button → 1-0-0
.button → 0-1-0
```

можно подумать, что цвет будет красным.

Но `components` находится в более приоритетном layer.

Поэтому результат:

```text
blue
```

Это происходит потому, что порядок cascade layers сравнивается **до specificity**.

---

### Стили вне layer

Обычные author styles, которые находятся вне какого-либо layer, имеют более высокий приоритет, чем обычные author styles внутри layers.

Например:

```css
@layer components {
  #title {
    color: red;
  }
}

.title {
  color: blue;
}
```

HTML:

```html
<h1
  id="title"
  class="title"
>
  Hello
</h1>
```

Результат:

```text
blue
```

Несмотря на:

```text
#title → 1-0-0
.title → 0-1-0
```

Причина:

```text
unlayered normal style
>
layered normal style
```

Specificity даже не понадобится сравнивать.

---

### `!important` меняет порядок layers

Для important declarations порядок layers **инвертируется**.

Предположим:

```css
@layer reset, base, components;
```

Для обычных declarations:

```text
components > base > reset
```

Но для important declarations:

```text
reset > base > components
```

Кроме того, important declarations внутри layers имеют приоритет над important declarations, находящимися вне layers.

Это сделано специально, чтобы ранние фундаментальные слои могли защищать критические important-правила.

---

## 12. Для чего нужны Cascade Layers?

Основная задача Cascade Layers — позволить управлять приоритетом больших групп CSS-правил **без повышения specificity** и без постоянного использования `!important`.

В большом проекте CSS может поступать из разных источников:

```text
Reset
Framework
Third-party library
Base styles
Components
Utilities
Overrides
```

Без layers эти правила находятся внутри одного author origin и постоянно конкурируют посредством specificity и source order.

Это может приводить к ситуации:

```css
.button {
}
```

затем:

```css
.page .button {
}
```

затем:

```css
#app .page .button {
}
```

а затем:

```css
#app .page .button {
  color: red !important;
}
```

То есть specificity постепенно увеличивается.

---

### Cascade Layers позволяют задать архитектуру заранее

Например:

```css
@layer reset, vendor, base, components, utilities;
```

Теперь приоритет обычных declarations:

```text
reset
  <
vendor
  <
base
  <
components
  <
utilities
```

При конфликте браузер сначала смотрит на layer.

Например:

```css
@layer vendor {
  #app .library .button {
    color: red;
  }
}

@layer components {
  .button {
    color: blue;
  }
}
```

Хотя:

```css
#app .library .button
```

имеет намного большую specificity, чем:

```css
.button
```

победит:

```css
.button {
  color: blue;
}
```

поскольку `components` расположен в более приоритетном layer.

---

### Основные преимущества Cascade Layers

#### 1. Управление приоритетом на архитектурном уровне

Можно определить:

```text
какие группы CSS важнее других
```

не анализируя specificity каждого отдельного селектора.

---

#### 2. Уменьшение specificity wars

Нет необходимости постоянно создавать всё более сложные селекторы:

```css
.page .content .card .button {}
```

только ради переопределения другого правила.

---

#### 3. Удобная работа со сторонними библиотеками

Например, CSS библиотеки можно разместить в отдельном layer:

```css
@layer vendor;
```

а собственные компоненты — в более позднем:

```css
@layer components;
```

Тогда собственный простой селектор может переопределить сложный селектор сторонней библиотеки.

MDN прямо рекомендует cascade layers как стандартный способ управления приоритетом third-party CSS без соревнования специфичности.

---

#### 4. Предсказуемая архитектура большого проекта

Например:

```css
@layer reset, base, layout, components, utilities;
```

Можно заранее определить назначение:

```text
reset
→ сброс браузерных различий

base
→ глобальная типографика и базовые элементы

layout
→ структура страницы

components
→ компоненты интерфейса

utilities
→ небольшие служебные классы
```

Это делает каскад значительно более предсказуемым.

---

### Важное правило порядка layers

Порядок именованных layers определяется порядком их первоначального создания.

Поэтому удобно объявлять его в начале CSS:

```css
@layer reset, base, components, utilities;
```

а ниже наполнять слои:

```css
@layer reset {
  /* ... */
}

@layer base {
  /* ... */
}

@layer components {
  /* ... */
}

@layer utilities {
  /* ... */
}
```

После создания layer его позиция относительно уже существующих layers не меняется простым повторным объявлением.

---

## Общая схема: как связаны Cascade и Specificity

Для понимания всей темы полезно запомнить не отдельные правила, а порядок принятия решения браузером.

Упрощённая современная модель:

```text
Для одного элемента и одного CSS-свойства
                ↓
Какие declarations вообще подходят?
                ↓
            Relevance
                ↓
       Origin + Importance
                ↓
         Cascade Layers
                ↓
           Specificity
                ↓
       Scoping Proximity
                ↓
          Source Order
                ↓
         Cascaded Value
                ↓
Inheritance / Initial Value
       при необходимости
```

Поэтому фраза:

> «В CSS побеждает самый специфичный селектор»

неверна.

Правильнее:

> **Specificity — один из этапов CSS Cascade. Она сравнивается только после origin, importance и cascade layers. При одинаковой specificity могут учитываться scoping proximity и затем source order.**

---

## Краткая таблица Specificity

| Селектор | Specificity |
|---|---:|
| `*` | `0-0-0` |
| `p` | `0-0-1` |
| `::before` | `0-0-1` |
| `.card` | `0-1-0` |
| `[type="email"]` | `0-1-0` |
| `:hover` | `0-1-0` |
| `.card:hover` | `0-2-0` |
| `.card p` | `0-1-1` |
| `.card > p` | `0-1-1` |
| `#header` | `1-0-0` |
| `#header .card` | `1-1-0` |
| `#header .card p` | `1-1-1` |
| `:where(#app, .card)` | `0-0-0` |
| `:is(#app, .card)` | `1-0-0` |

---

## Главное, что нужно запомнить

```text
Specificity:
ID > CLASS / ATTRIBUTE / PSEUDO-CLASS > TYPE / PSEUDO-ELEMENT
```

Но весь CSS Cascade шире:

```text
Origin + Importance
        ↓
Cascade Layers
        ↓
Specificity
        ↓
Scoping Proximity
        ↓
Source Order
```

И отдельно:

```text
!important ≠ высокая specificity
```

`!important` изменяет importance объявления и действует на более раннем этапе каскада.

```text
inline style ≠ обычный selector
```

Inline styles имеют специальный высокий приоритет среди author styles.

```text
Inheritance ≠ specificity
```

Непосредственно заданное элементу значение имеет приоритет над унаследованным значением.

```text
@layer
```

позволяет управлять приоритетом целых групп CSS-правил до сравнения specificity.