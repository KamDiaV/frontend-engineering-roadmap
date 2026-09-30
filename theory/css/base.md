# I. База CSS

### База

1. Что такое CSS и для чего он используется?
2. Что означает Cascading Style Sheets?
3. Как CSS связан с HTML?
4. Какими способами можно подключить CSS к HTML?
5. Чем inline, internal и external CSS отличаются друг от друга?
6. Как браузер применяет CSS к HTML-документу?
7. Что такое CSS rule?
8. Из каких частей состоит CSS-правило?
9. Что такое selector?
10. Что такое declaration?
11. Что такое property?
12. Что такое value?
13. Что такое stylesheet?
14. Что такое user agent stylesheet?
15. Что такое inheritance в CSS?
16. Какие свойства наследуются по умолчанию, а какие нет?
17. Что означают значения inherit, initial, unset и revert?
18. Что такое cascade в CSS?
19. По каким правилам браузер выбирает итоговое значение свойства?
20. Что такое source order и когда он влияет на стили?

---

### II. Селекторы

21. Какие основные типы CSS-селекторов существуют?
22. Чем отличаются селекторы по тегу, классу и id?
23. Почему для стилизации обычно предпочитают class, а не id?
24. Что такое универсальный селектор `*`?
25. Как работают групповые селекторы?
26. Что такое descendant selector?
27. Чем `A B` отличается от `A > B`?
28. Что делает adjacent sibling selector `+`?
29. Что делает general sibling selector `~`?
30. Что такое attribute selectors?
31. Как работают `[attr]`, `[attr="value"]`, `[attr^="value"]`, `[attr$="value"]`, `[attr*="value"]`?
32. Что такое pseudo-class?
33. Что такое pseudo-element?
34. Чем pseudo-class отличается от pseudo-element?
35. Для чего используются `:hover`, `:focus`, `:active`, `:visited`?
36. Чем `:focus` отличается от `:focus-visible`?
37. Как работают `:first-child`, `:last-child`, `:nth-child()`?
38. Чем `:nth-child()` отличается от `:nth-of-type()`?
39. Что делают `:not()`, `:is()` и `:where()`?
40. Что делает `:has()`?
41. Какие ограничения и особенности есть у `:visited`?
42. Для чего используются `::before` и `::after`?
43. Что необходимо указать, чтобы `::before` или `::after` появился?
44. Для чего используются `::placeholder`, `::selection`, `::marker`?

---

## III. Специфичность и каскад

45. Что такое specificity?
46. Как рассчитывается специфичность CSS-селектора?
47. Что имеет больший приоритет: id, class или element selector?
48. Как inline styles влияют на специфичность?
49. Как `!important` влияет на каскад?
50. Почему чрезмерное использование `!important` считается плохой практикой?
51. Что произойдёт, если два правила имеют одинаковую специфичность?
52. Как наследование взаимодействует с каскадом?
53. Как `:is()`, `:not()` и `:has()` влияют на специфичность?
54. Почему `:where()` имеет нулевую специфичность?
55. Что такое cascade layers (`@layer`)?
56. Для чего нужны cascade layers?

---

## IV. Box Model

57. Что такое CSS box model?
58. Из каких частей состоит box model?
59. Что такое content box?
60. Что такое padding?
61. Что такое border?
62. Что такое margin?
63. Как рассчитывается итоговый размер элемента?
64. Чем `box-sizing: content-box` отличается от `border-box`?
65. Почему часто используют `box-sizing: border-box`?
66. Что такое margin collapsing?
67. В каких случаях вертикальные margin схлопываются?
68. В каких случаях margin collapsing не происходит?
69. Чем margin отличается от padding?
70. Может ли padding быть отрицательным?
71. Может ли margin быть отрицательным?
72. Что такое outline и чем он отличается от border?

---

## V. Display и поток документа

73. Что такое normal flow?
74. Что делает свойство `display`?
75. Чем `block` отличается от `inline`?
76. Чем `inline-block` отличается от `inline`?
77. Что делает `display: none`?
78. Чем `display: none` отличается от `visibility: hidden`?
79. Что делает `display: contents`?
80. Что такое formatting context?
81. Что такое block formatting context?
82. В каких случаях создаётся BFC?
83. Для чего может быть полезен BFC?
84. Что такое `overflow`?
85. Чем отличаются `visible`, `hidden`, `auto`, `scroll`, `clip`?
86. Как overflow может влиять на layout?

---

## VI. Размеры и единицы измерения

87. Какие единицы измерения существуют в CSS?
88. Чем абсолютные единицы отличаются от относительных?
89. Чем `px` отличается от `%`?
90. Что такое `em`?
91. Что такое `rem`?
92. Чем `em` отличается от `rem`?
93. Что такое `vw` и `vh`?
94. Что такое `svh`, `lvh` и `dvh`?
95. Что такое `ch`?
96. Что такое `fr`?
97. Как работает `calc()`?
98. Для чего используются `min()`, `max()` и `clamp()`?
99. Чем `width` отличается от `max-width` и `min-width`?
100. Чем `height` отличается от `min-height`?
101. Что означает `width: auto`?
102. Что делает `aspect-ratio`?

---

## VII. Positioning

103. Какие значения свойства `position` существуют?
104. Как работает `position: static`?
105. Как работает `position: relative`?
106. Как работает `position: absolute`?
107. Относительно какого элемента позиционируется absolute-элемент?
108. Как работает `position: fixed`?
109. Как работает `position: sticky`?
110. Почему `position: sticky` иногда не работает?
111. Что делают `top`, `right`, `bottom`, `left`?
112. Что такое inset?
113. Что такое stacking context?
114. Что такое `z-index`?
115. Почему большой `z-index` иногда не помогает?
116. Какие свойства могут создавать новый stacking context?

---

## VIII. Flexbox

117. Что такое Flexbox и какие задачи он решает?
118. Как создать flex-контейнер?
119. Что такое main axis и cross axis?
120. Что делает `flex-direction`?
121. Что делает `justify-content`?
122. Что делает `align-items`?
123. Чем `align-items` отличается от `align-content`?
124. Что делает `align-self`?
125. Что делает `gap`?
126. Что делает `flex-wrap`?
127. Что такое `flex-basis`?
128. Что делает `flex-grow`?
129. Что делает `flex-shrink`?
130. Что означает сокращённая запись `flex`?
131. Что делает `order`?
132. Почему `order` нужно использовать осторожно с точки зрения accessibility?
133. Почему flex-элемент иногда не сжимается?
134. Для чего используют `min-width: 0` во flex-layout?
135. Как центрировать элемент по горизонтали и вертикали с помощью Flexbox?

---

## IX. CSS Grid

136. Что такое CSS Grid?
137. Чем Grid отличается от Flexbox?
138. Когда лучше использовать Grid, а когда Flexbox?
139. Как создать grid-контейнер?
140. Что делают `grid-template-columns` и `grid-template-rows`?
141. Что такое grid track?
142. Что такое grid line?
143. Что такое grid cell?
144. Что такое grid area?
145. Что делает единица `fr`?
146. Как работает `repeat()`?
147. Как работает `minmax()`?
148. Чем `auto-fill` отличается от `auto-fit`?
149. Что делает `gap` в Grid?
150. Как позиционировать элемент по grid lines?
151. Что такое named grid areas?
152. Как работает `grid-template-areas`?
153. Что такое implicit grid?
154. Что делают `grid-auto-columns` и `grid-auto-rows`?
155. Что делает `grid-auto-flow`?
156. Как центрировать grid-элемент?
157. Можно ли комбинировать Grid и Flexbox?

---

## X. Responsive Design

158. Что такое responsive design?
159. Что такое mobile-first?
160. Чем mobile-first отличается от desktop-first?
161. Что такое media query?
162. Как работает `@media`?
163. Что такое breakpoint?
164. Как выбирать breakpoints?
165. Почему не стоит ориентироваться только на конкретные устройства?
166. Что означает `min-width` в media query?
167. Что означает `max-width` в media query?
168. Что такое responsive typography?
169. Как использовать `clamp()` для адаптивного размера шрифта?
170. Как делать адаптивные изображения с помощью CSS?
171. Что такое container queries?
172. Чем container queries отличаются от media queries?
173. Как работает `@container`?
174. Когда container queries особенно полезны?

---

## XI. Текст и типографика

175. Что делают `font-family`, `font-size`, `font-weight`?
176. Что такое fallback fonts?
177. Что такое web fonts?
178. Как подключить шрифт через `@font-face`?
179. Что такое FOIT и FOUT?
180. Что делает `font-display`?
181. Чем `line-height` отличается от `font-size`?
182. Почему для `line-height` часто используют значение без единицы?
183. Что делает `letter-spacing`?
184. Что делает `text-align`?
185. Что делает `text-transform`?
186. Что делает `text-decoration`?
187. Как работает `text-overflow: ellipsis`?
188. Какие свойства нужны для однострочного ellipsis?
189. Как сделать многострочное обрезание текста?
190. Что делают `white-space`, `word-break`, `overflow-wrap`?

---

## XII. Цвета, фон и границы

191. Какие способы задания цвета существуют в CSS?
192. Чем HEX отличается от RGB?
193. Что такое HSL?
194. Что такое alpha channel?
195. Что делает `opacity`?
196. Чем `opacity` отличается от цвета с alpha-каналом?
197. Что делает `background-color`?
198. Как работает `background-image`?
199. Что делают `background-size`, `background-position`, `background-repeat`?
200. Чем `cover` отличается от `contain`?
201. Как работает `linear-gradient()`?
202. Как работает `radial-gradient()`?
203. Что такое `border-radius`?
204. Как создать круг с помощью CSS?
205. Что делает `box-shadow`?
206. Чем `box-shadow` отличается от `filter: drop-shadow()`?

---

## XIII. Псевдоклассы состояния и формы

207. Как стилизовать состояние hover?
208. Как стилизовать keyboard focus?
209. Почему нельзя просто убирать outline у focus?
210. Что делает `:disabled`?
211. Что делает `:checked`?
212. Что делает `:required`?
213. Что делают `:valid` и `:invalid`?
214. Что такое `:placeholder-shown`?
215. Как стилизовать checkbox или radio?
216. Что такое `appearance: none`?
217. Какие проблемы accessibility могут появиться при кастомизации form controls?

---

## XIV. Transitions, Transforms и Animations

218. Что такое CSS transition?
219. Какие свойства можно анимировать?
220. Что делают `transition-property`, `transition-duration`, `transition-timing-function`, `transition-delay`?
221. Что такое easing?
222. Что делает `transform`?
223. Как работают `translate`, `scale`, `rotate`, `skew`?
224. Чем transform отличается от изменения top/left?
225. Что такое transform origin?
226. Что такое CSS animation?
227. Что такое `@keyframes`?
228. Что делают `animation-duration`, `animation-delay`, `animation-iteration-count`?
229. Что делает `animation-fill-mode`?
230. Что делает `animation-direction`?
231. Что такое `prefers-reduced-motion`?
232. Почему его важно учитывать?

---

## XV. CSS Variables

233. Что такое CSS custom properties?
234. Как объявить CSS-переменную?
235. Как использовать `var()`?
236. Почему custom properties называются properties, а не обычными переменными?
237. Наследуются ли CSS custom properties?
238. Что такое fallback в `var()`?
239. Как переопределять переменные внутри компонента?
240. Как использовать CSS variables для темы?
241. Чем CSS custom properties отличаются от SCSS variables?

---

## XVI. Архитектура CSS

242. Почему CSS становится сложно поддерживать в больших проектах?
243. Что такое CSS architecture?
244. Что такое BEM?
245. Из каких частей состоит BEM?
246. Что такое block?
247. Что такое element?
248. Что такое modifier?
249. Какие преимущества и недостатки есть у BEM?
250. Что такое utility classes?
251. Чем utility-first отличается от BEM?
252. Что такое component-based styling?
253. Почему важно избегать слишком длинных селекторов?
254. Что такое specificity wars?
255. Как уменьшать связанность CSS?
256. Как организовывать CSS-файлы в проекте?
257. В чём смысл разделения styles на base, components, layout, pages?
258. Что такое reset CSS?
259. Что такое normalize CSS?
260. Чем reset отличается от normalize?

---


---

## XVIII. Современный CSS

277. Что такое CSS nesting?
278. Чем native CSS nesting отличается от SCSS nesting?
279. Что такое `:has()` и какие задачи он позволяет решать?
280. Что такое container queries?
281. Что такое cascade layers?
282. Что такое logical properties?
283. Чем `margin-inline` отличается от `margin-left` / `margin-right`?
284. Что делают `padding-block` и `padding-inline`?
285. Для чего нужны logical properties?
286. Что такое `subgrid`?
287. Когда полезен `display: subgrid`?
288. Что такое `color-mix()`?
289. Что такое `accent-color`?
290. Что такое `object-fit`?
291. Чем `object-fit: cover` отличается от `contain`?
292. Что такое `object-position`?
293. Что такое `scroll-snap`?
294. Что такое `overscroll-behavior`?
295. Что такое `content-visibility`?

---

## XIX. Производительность

296. Какие CSS-свойства могут вызывать layout?
297. Что такое reflow?
298. Что такое repaint?
299. Чем layout отличается от paint и composite?
300. Почему transform и opacity обычно лучше подходят для анимации?
301. Может ли CSS влиять на Core Web Vitals?
302. Как CSS может влиять на CLS?
303. Как шрифты влияют на производительность?
304. Почему стоит избегать слишком сложных селекторов?
305. Нужно ли вручную оптимизировать каждый CSS-селектор?
306. Что такое critical CSS?
307. Что такое unused CSS?

---

## XX. Accessibility в CSS

308. Как CSS может повлиять на accessibility?
309. Почему цвет не должен быть единственным способом передачи информации?
310. Что такое color contrast?
311. Почему важно состояние `:focus-visible`?
312. Почему `outline: none` может быть проблемой?
313. Как CSS может нарушить keyboard accessibility?
314. Почему визуальный порядок элементов не должен противоречить DOM-порядку?
315. Какие проблемы могут вызвать `order` во Flexbox?
316. Какие проблемы могут вызвать Grid placement и absolute positioning?
317. Почему важно учитывать `prefers-reduced-motion`?
318. Что такое `forced-colors`?
319. Что такое high contrast mode?

---

## XXI. Практические вопросы

320. Как центрировать элемент по горизонтали и вертикали?
321. Как сделать sticky header?
322. Как сделать footer прижатым к низу страницы?
323. Как сделать двухколоночный layout?
324. Как сделать адаптивную сетку карточек без большого количества media queries?
325. Как сделать карточки одинаковой высоты?
326. Как сделать изображение, которое сохраняет пропорции?
327. Как сделать изображение, полностью заполняющее контейнер?
328. Как сделать текст с многоточием?
329. Как сделать dropdown только с CSS и когда это плохая идея?
330. Как сделать модальное окно визуально поверх остальных элементов?
331. Почему `z-index: 9999` может не работать?
332. Как найти причину горизонтального скролла?
333. Почему элемент выходит за пределы контейнера?
334. Почему `height: 100%` иногда не работает?
335. Почему margin не работает так, как ожидается?
336. Почему `position: sticky` не работает?
337. Почему flex-элемент переполняет контейнер?
338. Почему Grid создаёт неожиданно широкую колонку?
339. Как сделать адаптивный layout без фиксированной ширины?
340. Какой layout выбрать для navbar: Flexbox или Grid?
341. Какой layout выбрать для карточек каталога?
342. Какой layout выбрать для двухмерной галереи?
343. Как сделать responsive container?
344. Как сделать компонент, который адаптируется к размеру своего контейнера?
345. Как проверить CSS на accessibility-проблемы?
346. Как искать причину того, что CSS-правило не применяется?
347. Как понять, какое правило победило в cascade?
348. Как отлаживать specificity?
349. Как использовать DevTools для анализа box model?
350. Как использовать DevTools для Flexbox и Grid?