# IV. Box Model

## 1. Что такое CSS Box Model?

**CSS Box Model (блочная модель CSS)** — модель, которая описывает, как браузер представляет элемент в виде прямоугольной области и как рассчитываются его размеры и пространство вокруг него.

Упрощённо каждый CSS-box состоит из нескольких слоёв:

```text
margin
└── border
    └── padding
        └── content
```

То есть у элемента есть:

1. содержимое — `content`;
2. внутренний отступ — `padding`;
3. граница — `border`;
4. внешний отступ — `margin`.

Например:

```html
<div class="card">
  Hello
</div>
```

```css
.card {
  width: 200px;
  padding: 20px;
  border: 2px solid black;
  margin: 30px;
}
```

Браузер рассматривает `.card` не просто как область шириной `200px`.

В зависимости от `box-sizing` к размеру содержимого могут дополнительно прибавляться:

```text
padding
+
border
```

А `margin` создаёт пространство уже **за пределами border box**.

Box Model необходим для понимания:

- размеров элементов;
- расстояния между элементами;
- работы `width` и `height`;
- `padding`;
- `border`;
- `margin`;
- расположения элементов в layout.

Важно понимать, что HTML-элемент и CSS-box — не абсолютно одно и то же понятие. В процессе layout элемент может генерировать один или несколько CSS-боксов. Однако на начальном уровне удобно представлять большинство обычных элементов как прямоугольные коробки.

---

## 2. Из каких частей состоит Box Model?

Классическая CSS Box Model состоит из четырёх областей:

```text
┌───────────────────────────────┐
│            MARGIN             │
│   ┌───────────────────────┐   │
│   │        BORDER         │   │
│   │   ┌───────────────┐   │   │
│   │   │    PADDING    │   │   │
│   │   │   ┌───────┐   │   │   │
│   │   │   │CONTENT│   │   │   │
│   │   │   └───────┘   │   │   │
│   │   └───────────────┘   │   │
│   └───────────────────────┘   │
└───────────────────────────────┘
```

### 1. Content

Область, где располагается содержимое элемента:

- текст;
- изображение;
- дочерние элементы;
- другое содержимое.

### 2. Padding

Пространство между содержимым и границей элемента.

```text
content
↓
padding
↓
border
```

### 3. Border

Граница вокруг `content + padding`.

### 4. Margin

Пространство снаружи `border`.

Используется для отделения элемента от других элементов.

Таким образом:

```text
content
+ padding
+ border
= border box
```

А затем вокруг него находится:

```text
margin
```

Важно: `margin` влияет на занимаемое элементом пространство относительно соседей, но **не является частью border box элемента**.

---

## 3. Что такое Content Box?

**Content Box** — внутренняя область CSS-box, в которой располагается непосредственное содержимое элемента.

Например:

```html
<div class="box">
  Hello
</div>
```

Текст:

```text
Hello
```

находится внутри content box.

Если используется стандартная модель:

```css
.box {
  box-sizing: content-box;
  width: 200px;
  height: 100px;
}
```

то:

```text
content width  = 200px
content height = 100px
```

То есть свойства:

```css
width
height
```

задают размер именно **content box**.

Если затем добавить:

```css
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
```

content box всё равно останется:

```text
200px
```

по ширине.

Но фактический border box станет шире:

```text
200px content
+ 20px left padding
+ 20px right padding
+ 5px left border
+ 5px right border

= 250px
```

Это стандартное поведение при:

```css
box-sizing: content-box;
```

Content box может содержать:

- текст;
- изображения;
- другие элементы;
- заменяемое содержимое;
- другое содержимое элемента.

---

## 4. Что такое Padding?

**Padding (внутренний отступ)** — пространство между содержимым элемента и его границей (`border`).

Схема:

```text
border
└── padding
    └── content
```

Например:

```css
.button {
  padding: 10px;
}
```

Это создаёт расстояние `10px` между содержимым кнопки и её границами.

```text
┌─────────────────────┐
│      padding        │
│   ┌─────────────┐   │
│   │    Button   │   │
│   └─────────────┘   │
│      padding        │
└─────────────────────┘
```

Padding можно задавать отдельно для каждой стороны:

```css
padding-top: 10px;
padding-right: 20px;
padding-bottom: 10px;
padding-left: 20px;
```

Или использовать shorthand:

```css
padding: 10px 20px;
```

Здесь:

```text
10px → top и bottom
20px → left и right
```

### Синтаксис shorthand

Одно значение:

```css
padding: 20px;
```

```text
top    20px
right  20px
bottom 20px
left   20px
```

Два значения:

```css
padding: 10px 20px;
```

```text
top/bottom → 10px
left/right → 20px
```

Три значения:

```css
padding: 10px 20px 30px;
```

```text
top        → 10px
left/right → 20px
bottom     → 30px
```

Четыре:

```css
padding: 10px 20px 30px 40px;
```

Порядок:

```text
top
right
bottom
left
```

Удобная мнемоника:

```text
по часовой стрелке
```

### Padding и фон

Фон элемента по умолчанию распространяется не только под content, но и под padding.

Например:

```css
.box {
  padding: 20px;
  background-color: lightblue;
}
```

Область padding также будет иметь светло-голубой фон.

### Padding влияет на размеры элемента

При:

```css
box-sizing: content-box;
```

padding добавляется к `width` и `height`.

При:

```css
box-sizing: border-box;
```

padding входит внутрь заданных `width` и `height`.

---

## 5. Что такое Border?

**Border (граница)** — область CSS-box, расположенная вокруг content и padding.

Схема:

```text
margin
└── border
    └── padding
        └── content
```

Пример:

```css
.card {
  border: 2px solid black;
}
```

`border` — shorthand для трёх характеристик:

```text
border-width
border-style
border-color
```

То есть:

```css
border: 2px solid black;
```

означает:

```css
border-width: 2px;
border-style: solid;
border-color: black;
```

### Границы отдельных сторон

Можно управлять сторонами независимо:

```css
border-top: 1px solid black;
border-right: 2px solid blue;
border-bottom: 3px solid red;
border-left: 4px solid green;
```

Также существуют отдельные свойства:

```css
border-width
border-style
border-color
```

### Border участвует в размере элемента

При:

```css
box-sizing: content-box;
```

border добавляется к размеру content box.

Например:

```css
.box {
  width: 200px;
  border: 5px solid black;
}
```

Ширина border box:

```text
200
+ 5
+ 5
= 210px
```

Если есть ещё padding:

```css
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
```

получаем:

```text
200 + 20 + 20 + 5 + 5 = 250px
```

При:

```css
box-sizing: border-box;
```

border уже входит в заданную ширину.

---

## 6. Что такое Margin?

**Margin (внешний отступ)** — пространство снаружи границы элемента.

Схема:

```text
margin
└── border
    └── padding
        └── content
```

Например:

```css
.card {
  margin: 20px;
}
```

Margin создаёт пространство вокруг элемента и может отделять его от соседних элементов.

### Margin можно задавать отдельно

```css
margin-top: 10px;
margin-right: 20px;
margin-bottom: 30px;
margin-left: 40px;
```

Или посредством shorthand:

```css
margin: 10px 20px 30px 40px;
```

Порядок:

```text
top → right → bottom → left
```

### `margin: auto`

Margin также может принимать значение:

```css
auto
```

Например, классический способ горизонтального центрирования блочного элемента с заданной шириной:

```css
.box {
  width: 500px;
  margin-inline: auto;
}
```

Свободное горизонтальное пространство распределяется между соответствующими `auto` margins.

### Margin не является частью border box

Например:

```css
.box {
  width: 200px;
  margin: 50px;
}
```

`width: 200px` не превращается из-за margin в `300px`.

Border box остаётся своего рассчитанного размера, а margin создаёт дополнительное внешнее пространство вокруг него.

### Особенность Margin

Вертикальные margins в обычном block layout в некоторых ситуациях могут **схлопываться (margin collapsing)**.

Padding такого поведения не имеет.

---

## 7. Как рассчитывается итоговый размер элемента?

Расчёт зависит прежде всего от свойства:

```css
box-sizing
```

Основные варианты:

```css
content-box
border-box
```

---

### При `box-sizing: content-box`

Это стандартная модель для большинства элементов.

Например:

```css
.box {
  box-sizing: content-box;

  width: 200px;
  height: 100px;

  padding: 20px;

  border: 5px solid black;

  margin: 30px;
}
```

`width: 200px` означает:

```text
ширина content box = 200px
```

#### Ширина border box

Формула:

```text
content width
+ padding-left
+ padding-right
+ border-left
+ border-right
```

Получаем:

```text
200
+ 20
+ 20
+ 5
+ 5

= 250px
```

#### Высота border box

```text
content height
+ padding-top
+ padding-bottom
+ border-top
+ border-bottom
```

Получаем:

```text
100
+ 20
+ 20
+ 5
+ 5

= 150px
```

То есть визуальный border box:

```text
250px × 150px
```

---

#### А что с margin?

Margin находится снаружи border box.

Если для простоты представить, что margins не схлопываются и все четыре значения участвуют в занимаемом пространстве:

```text
горизонтальное пространство:

30 + 250 + 30 = 310px
```

```text
вертикальное пространство:

30 + 150 + 30 = 210px
```

Но важно различать:

```text
размер border box
```

и:

```text
пространство, которое элемент может занимать вместе с margin
```

Margin не включается в `width`/`height` элемента и может дополнительно подчиняться правилам layout — например, вертикальные margins могут схлопываться.

---

### Формула для `content-box`

Ширина border box:

```text
width
+ padding-left
+ padding-right
+ border-left-width
+ border-right-width
```

Высота:

```text
height
+ padding-top
+ padding-bottom
+ border-top-width
+ border-bottom-width
```

---

### При `box-sizing: border-box`

Если написать:

```css
.box {
  box-sizing: border-box;

  width: 200px;
  padding: 20px;
  border: 5px solid black;
}
```

внешняя ширина border box останется:

```text
200px
```

Внутри неё браузер размещает:

```text
border + padding + content
```

Поэтому ширина content box составит:

```text
200
- 20
- 20
- 5
- 5

= 150px
```

---

## 8. Чем `box-sizing: content-box` отличается от `border-box`?

Свойство:

```css
box-sizing
```

определяет, **что именно включается в значения `width` и `height` элемента**.

---

### `content-box`

Это стандартная модель для большинства элементов.

```css
box-sizing: content-box;
```

В этом случае:

```css
width: 300px;
```

означает:

```text
content width = 300px
```

Padding и border добавляются сверху.

Например:

```css
.box {
  box-sizing: content-box;
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}
```

Расчёт:

```text
300
+ 20
+ 20
+ 5
+ 5

= 350px
```

Итоговый border box имеет ширину:

```text
350px
```

---

### `border-box`

```css
box-sizing: border-box;
```

В этом случае заданные:

```css
width
height
```

включают:

```text
content
+
padding
+
border
```

Например:

```css
.box {
  box-sizing: border-box;
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}
```

Итоговая ширина border box:

```text
300px
```

А content box:

```text
300
- 20
- 20
- 5
- 5

= 250px
```

### Сравнение

```text
content-box

width
= content

реальный border box
= width + padding + border
```

```text
border-box

width
= content + padding + border
```

| Свойство | `content-box` | `border-box` |
|---|---|---|
| `width` включает content | Да | Да |
| `width` включает padding | Нет | Да |
| `width` включает border | Нет | Да |
| `width` включает margin | Нет | Нет |

**Margin не входит ни в `content-box`, ни в `border-box`.**

### Важный нюанс

`content-box` является initial value свойства `box-sizing`, но браузеры по умолчанию используют `border-box` для некоторых элементов интерфейса, включая, например, `<table>`, `<select>`, `<button>` и некоторые типы `<input>`.

---

## 9. Почему часто используют `box-sizing: border-box`?

`border-box` делает расчёт размеров элементов значительно более предсказуемым.

Представим:

```css
.card {
  width: 300px;
  padding: 20px;
  border: 5px solid black;
}
```

При стандартном:

```css
box-sizing: content-box;
```

получаем:

```text
300 + 40 + 10 = 350px
```

То есть элемент оказался шире, чем можно было ожидать по записи:

```css
width: 300px;
```

При:

```css
box-sizing: border-box;
```

эта же запись означает:

```text
полный border box = 300px
```

Это особенно удобно для:

- адаптивной вёрстки;
- grid;
- flexbox;
- карточек;
- форм;
- компонентов с фиксированной шириной;
- элементов с `width: 100%`.

Например:

```css
.input {
  width: 100%;
  padding: 16px;
  border: 1px solid gray;
}
```

С `border-box`:

```text
input остаётся шириной 100%
```

Padding и border размещаются внутри этой ширины.

Поэтому во многих проектах используется глобальная настройка:

```css
html {
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}
```

Иногда используется более короткий вариант:

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

Оба подхода позволяют сделать размеры элементов более предсказуемыми.

---

## 10. Что такое Margin Collapsing?

**Margin Collapsing (схлопывание внешних отступов)** — поведение CSS, при котором некоторые соседние вертикальные margins блоков объединяются в один margin вместо того, чтобы складываться.

Например:

```css
.first {
  margin-bottom: 50px;
}

.second {
  margin-top: 30px;
}
```

Можно ожидать:

```text
50 + 30 = 80px
```

Но в обычном block layout эти margins могут схлопнуться.

Тогда расстояние составит:

```text
50px
```

То есть из двух положительных margins используется больший.

### Если оба margin положительные

Берётся больший:

```text
50px + 30px
→ 50px
```

### Если оба margin отрицательные

Используется значение с большей абсолютной величиной, то есть наиболее отрицательное.

Например:

```text
-20px
-50px

→ -50px
```

### Если один положительный, другой отрицательный

Отрицательное значение вычитается из положительного.

Например:

```text
50px
-20px

→ 30px
```

### Важное ограничение

Margin collapsing относится прежде всего к:

```text
margin-top
margin-bottom
```

то есть вертикальным margins блоков в обычном block formatting context.

Горизонтальные margins:

```text
margin-left
margin-right
```

не схлопываются.

---

## 11. В каких случаях вертикальные Margin схлопываются?

Существует три основных сценария margin collapsing.

---

### 1. Между соседними блоками

Например:

```html
<div class="first">First</div>
<div class="second">Second</div>
```

```css
.first {
  margin-bottom: 40px;
}

.second {
  margin-top: 20px;
}
```

Если элементы находятся в обычном block flow и ничто не препятствует схлопыванию:

```text
40px + 20px
```

не превращаются в:

```text
60px
```

Итоговый отступ:

```text
40px
```

---

### 2. Между родителем и первым дочерним блоком

Например:

```html
<div class="parent">
  <p class="child">Text</p>
</div>
```

```css
.parent {
  margin-top: 20px;
}

.child {
  margin-top: 50px;
}
```

При определённых условиях верхний margin первого дочернего блока может схлопнуться с верхним margin родителя.

Для этого между краями не должно быть разделителя вроде:

- `border-top`;
- `padding-top`;
- inline-содержимого;
- clearance.

Из-за этого иногда новичок пишет:

```css
.child {
  margin-top: 50px;
}
```

и ожидает, что ребёнок отойдёт вниз внутри родителя.

Но визуально может показаться, что вниз переместился сам родитель.

Причина — margin collapsing.

---

### 3. Между родителем и последним дочерним блоком

Нижний margin последнего дочернего блока также может схлопнуться с нижним margin родителя при выполнении соответствующих условий.

Например, если у родителя:

- нет `padding-bottom`;
- нет `border-bottom`;
- высота не создаёт препятствие для схлопывания;
- элементы участвуют в подходящем обычном block formatting context.

---

### 4. У пустого блока — между собственными `margin-top` и `margin-bottom`

В некоторых условиях верхний и нижний margins одного пустого блока могут схлопнуться друг с другом.

Например, блок:

- не содержит line box;
- не имеет подходящего содержимого, разделяющего margins;
- не имеет вертикального padding и border;
- имеет подходящую `height`/`min-height`;
- не создаёт новый formatting context.

Упрощённо:

```html
<div class="empty"></div>
```

```css
.empty {
  margin-top: 30px;
  margin-bottom: 50px;
}
```

Его верхний и нижний margins в определённых условиях могут участвовать в одном collapsed margin.

### Главное для начала

Три ситуации, которые нужно запомнить в первую очередь:

```text
1. sibling ↔ sibling

2. parent ↔ first child

3. last child ↔ parent
```

и отдельный случай:

```text
4. пустой block
```

---

## 12. В каких случаях Margin Collapsing не происходит?

Margin collapsing происходит не всегда.

---

### 1. Горизонтальные margins не схлопываются

```css
margin-left
margin-right
```

не используют механизм margin collapsing.

Например:

```css
.first {
  margin-right: 20px;
}

.second {
  margin-left: 30px;
}
```

Нельзя применять к ним правило:

```text
max(20px, 30px)
```

как при вертикальном margin collapsing.

---

### 2. Между Flex Items

Например:

```css
.container {
  display: flex;
}
```

Margins flex items друг с другом не схлопываются.

```html
<div class="container">
  <div class="first"></div>
  <div class="second"></div>
</div>
```

```css
.first {
  margin-bottom: 30px;
}

.second {
  margin-top: 20px;
}
```

В flex layout механизм обычного margin collapsing между flex items не применяется.

---

### 3. Между Grid Items

То же относится к:

```css
.container {
  display: grid;
}
```

Margins grid items не схлопываются друг с другом.

---

### 4. У абсолютно позиционированных элементов

Например:

```css
.element {
  position: absolute;
}
```

Margins absolutely positioned boxes не схлопываются.

То же относится к:

```css
position: fixed;
```

---

### 5. У floated elements

Например:

```css
.element {
  float: left;
}
```

Margins floated boxes не схлопываются с окружающими boxes обычным способом.

---

### 6. У `inline-block`

Например:

```css
.element {
  display: inline-block;
}
```

Margins такого box не схлопываются.

---

### 7. Через границу разных formatting contexts

Margins не схлопываются через границу независимых formatting contexts.

Например, новый Block Formatting Context можно создать:

```css
.parent {
  display: flow-root;
}
```

Тогда margins детей не схлопываются наружу через границу этого BFC.

Это одна из современных и понятных причин использовать:

```css
display: flow-root;
```

---

### 8. Если между parent и child есть `padding`

Например:

```css
.parent {
  padding-top: 1px;
}
```

Теперь `margin-top` первого ребёнка отделён от края родителя padding и не схлопывается с верхним margin родителя.

---

### 9. Если между ними есть `border`

Например:

```css
.parent {
  border-top: 1px solid transparent;
}
```

Border разделяет margins.

Но добавлять «невидимый border» только ради борьбы со схлопыванием обычно не лучший архитектурный подход.

---

### 10. Если между margins есть содержимое

Например:

```html
<div class="parent">
  Text
  <p>Paragraph</p>
</div>
```

Наличие line box между краями препятствует соответствующему parent-child collapsing.

---

### 11. При `clearance`

Некоторые ситуации с:

```css
clear
```

также препятствуют обычному схлопыванию margins.

### Практически

Если margin ведёт себя неожиданно, стоит проверить:

```text
display: block?
flex?
grid?
position?
float?
padding?
border?
новый BFC?
```

Для современного layout во Flexbox и Grid проблема margin collapsing встречается значительно реже.

---

## 13. Чем Margin отличается от Padding?

Главное различие:

```text
padding → пространство ВНУТРИ элемента

margin → пространство СНАРУЖИ элемента
```

Схема:

```text
           margin
┌─────────────────────────┐
│        border           │
│  ┌───────────────────┐  │
│  │      padding      │  │
│  │   ┌───────────┐   │  │
│  │   │  content  │   │  │
│  │   └───────────┘   │  │
│  └───────────────────┘  │
└─────────────────────────┘
```

### Padding

```css
.card {
  padding: 20px;
}
```

Создаёт пространство:

```text
между content и border
```

### Margin

```css
.card {
  margin: 20px;
}
```

Создаёт пространство:

```text
за пределами border
```

### Основные различия

| Характеристика | Padding | Margin |
|---|---|---|
| Находится внутри border | Да | Нет |
| Находится снаружи border | Нет | Да |
| Фон элемента распространяется на область | Обычно да | Нет |
| Участвует в `border-box` | Да | Нет |
| Может быть отрицательным | Нет | Да |
| Может схлопываться | Нет | Вертикальный margin иногда может |
| Используется для пространства внутри компонента | Да | Нет |
| Используется для расстояния между элементами | Обычно нет | Да |

### Когда использовать Padding?

Когда нужно увеличить пространство **внутри самого элемента**.

Например:

```css
.button {
  padding: 12px 24px;
}
```

Так увеличивается область вокруг текста кнопки внутри её границ.

### Когда использовать Margin?

Когда нужно отделить элемент от соседних элементов.

Например:

```css
.card {
  margin-bottom: 32px;
}
```

Это создаёт пространство после карточки.

---

## 14. Может ли Padding быть отрицательным?

Нет.

Отрицательные значения padding являются **недопустимыми в CSS**.

Например:

```css
.box {
  padding: -20px;
}
```

Это не означает:

> уменьши внутренний отступ на 20px.

Такое значение является invalid.

Браузер не применит отрицательное значение `padding`.

Допустимо:

```css
padding: 0;
padding: 10px;
padding: 2rem;
padding: 5%;
```

Недопустимо:

```css
padding: -10px;
```

### Почему?

Padding представляет размер внутренней области между content edge и border edge.

Эта область не может иметь отрицательную толщину.

Поэтому спецификация ограничивает padding неотрицательными значениями.

---

## 15. Может ли Margin быть отрицательным?

Да.

В отличие от padding, margin может принимать отрицательные значения.

Например:

```css
.box {
  margin-top: -20px;
}
```

Это может сместить элемент ближе к предыдущему содержимому или привести к визуальному перекрытию элементов.

Например:

```html
<div class="first">First</div>
<div class="second">Second</div>
```

```css
.first {
  height: 100px;
  background: lightblue;
}

.second {
  margin-top: -20px;
  background: lightpink;
}
```

Второй элемент может переместиться вверх относительно своего обычного положения.

### Где отрицательные margins могут использоваться?

Например:

- для намеренного визуального перекрытия;
- для декоративных layout-эффектов;
- для корректировки позиции элемента;
- в некоторых старых layout-паттернах.

### Но использовать нужно осторожно

Отрицательный margin влияет на normal flow и взаимодействие элемента с соседями.

Он может привести к:

- неожиданному перекрытию;
- сложной адаптивности;
- трудной отладке;
- проблемам при изменении содержимого.

В современном CSS для многих задач вместо отрицательных margins могут быть удобнее:

```css
transform
grid
flexbox
position
```

Однако отрицательные margins остаются полноценной и допустимой частью CSS.

---

## 16. Что такое Outline и чем он отличается от Border?

**Outline (обводка)** — линия, которая рисуется вокруг элемента, обычно снаружи его border, но не участвует в расчёте размеров и layout.

Например:

```css
.button {
  outline: 2px solid blue;
}
```

Синтаксис похож на border:

```css
outline: width style color;
```

Например:

```css
outline: 3px solid red;
```

Можно также задавать:

```css
outline-width
outline-style
outline-color
```

---

### Главное отличие от Border

Border является частью Box Model:

```text
content
↓
padding
↓
border
↓
margin
```

Outline в эту последовательность не входит.

Он рисуется поверх визуального представления элемента и **не занимает дополнительного пространства в layout**.

---

### Пример

```css
.box {
  width: 200px;
  border: 10px solid black;
}
```

При `content-box` border увеличивает размер border box:

```text
200 + 10 + 10 = 220px
```

Но:

```css
.box {
  width: 200px;
  outline: 10px solid red;
}
```

outline не увеличивает рассчитанный размер элемента.

Элемент не становится на `20px` шире с точки зрения layout.

Outline может визуально перекрывать соседнее содержимое, потому что браузер не резервирует для него дополнительное место.

---

### `outline-offset`

Можно управлять расстоянием между outline и краем элемента:

```css
.button {
  outline: 2px solid blue;
  outline-offset: 4px;
}
```

Схематично:

```text
outline

   ↓ 4px

border
padding
content
```

---

### Сравнение Border и Outline

| Характеристика | Border | Outline |
|---|---|---|
| Является частью Box Model | Да | Нет |
| Может влиять на размер box | Да | Нет |
| Влияет на layout | Может | Нет |
| Рисуется вокруг элемента | Да | Да |
| Можно задавать стороны отдельно | Да | Нет аналогичного набора `outline-top/right/...` |
| Есть `outline-offset` | Нет | Да |
| Часто используется для focus indicator | Может | Очень часто |

---

### Outline и Accessibility

Одно из самых важных применений outline — визуальное обозначение фокуса.

Например:

```css
.button:focus-visible {
  outline: 3px solid blue;
  outline-offset: 3px;
}
```

Это позволяет пользователю, перемещающемуся по странице клавиатурой, видеть текущий элемент.

Поэтому запись:

```css
*:focus {
  outline: none;
}
```

без альтернативного видимого focus indicator — плохая практика.

Если стандартный outline браузера не соответствует дизайну, его можно заменить:

```css
.button:focus-visible {
  outline: 2px solid currentColor;
  outline-offset: 4px;
}
```

Главное — сохранить хорошо заметное визуальное состояние фокуса.

---

## Общая схема Box Model

```text
┌─────────────────────────────────────┐
│                MARGIN               │
│                                     │
│   ┌─────────────────────────────┐   │
│   │           BORDER            │   │
│   │                             │   │
│   │   ┌─────────────────────┐   │   │
│   │   │       PADDING       │   │   │
│   │   │                     │   │   │
│   │   │   ┌─────────────┐   │   │   │
│   │   │   │   CONTENT   │   │   │   │
│   │   │   └─────────────┘   │   │   │
│   │   │                     │   │   │
│   │   └─────────────────────┘   │   │
│   │                             │   │
│   └─────────────────────────────┘   │
│                                     │
└─────────────────────────────────────┘
```

```text
content
+ padding
+ border
= border box
```

```text
margin
= пространство снаружи border box
```

При:

```css
box-sizing: content-box;
```

```text
width = content
```

При:

```css
box-sizing: border-box;
```

```text
width = content + padding + border
```

Margin:

```text
не входит в width в обоих случаях
```

---

## Главное, что нужно запомнить

```text
Content
→ содержимое элемента

Padding
→ пространство внутри элемента
→ между content и border

Border
→ граница вокруг content + padding

Margin
→ пространство снаружи элемента
```

```text
content-box
→ width задаёт размер content

border-box
→ width включает content + padding + border
```

```text
padding
→ отрицательным быть не может

margin
→ отрицательным быть может
```

```text
вертикальные margins
→ иногда схлопываются

padding
→ никогда не схлопывается
```

```text
outline
→ не является частью Box Model
→ не занимает место в layout
→ часто используется для focus state
```