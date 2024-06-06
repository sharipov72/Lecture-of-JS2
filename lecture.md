Создание оглавления из заголовков h2
Процесс написания скрипта для формирования оглавления из тегов <h2> представим в виде следующих шагов:

1. Создадим HTML обёртку для оглавления и присвоим её переменной tpl:
```js
const tpl = '<section class="table-of-contents"><div style="font-weight: bold;">Содержание:</div><ul>{{contents}}</ul></section>';
```
2. Объявим переменную contents с помощью ключевого слова let и присвоим ей в качестве значения пустую строку:
```js
let contents = '';
```
В эту переменную мы будем собирать HTML код оглавления.

3. Создадим переменную elHeaders и поместим в неё все найденные теги <h2> в элементе с классом article:
```js
const elHeaders = document.querySelectorAll('.article h2');
```
Для выбора элементов используется метод querySelectorAll().

4. Сформируем HTML код оглавления на основе <h2>:
```js
elHeaders.forEach((el, index) => {
  if (!el.id) {
    el.id = `id-${index}`;
  }
  const url = `${location.href.split('#')[0]}#${el.id}`;
  contents += `<li><a href="${url}">${el.textContent}</a></li>`;
});
```
В этом коде для перебора выбранных <h2> используется метод forEach(). Внутри forEach() мы сначала устанавливаем заголовку <h2> значение атрибута id, если у него его конечно нет. После этого формируем URL и сохраняем его в переменную url. Затем добавляем к значению переменной contents элемент оглавления.

5. Вставим HTML содержимое оглавления внутрь <aside> перед первым элементом с помощью метода insertAdjacentHTML:
```js
document.querySelector('aside').insertAdjacentHTML('afterbegin', tpl.replace('{{contents}}', contents));
```
Конечный HTML получим взяв значение переменной tpl, в которой {{contents}} заменим на содержимое переменной contents.


В итоге мы получим следующий код на чистом JavaScript для автоматической генерации содержания статей:
```js
const tpl = '<section class="table-of-contents"><div style="font-weight: bold;">Содержание:</div><ul>{{contents}}</ul></section>';
let contents = '';
const elHeaders = document.querySelectorAll('.article h2');
elHeaders.forEach((el, index) => {
  if (!el.id) {
    el.id = `id-${index}`;
  }
  const url = `${location.href.split('#')[0]}#${el.id}`;
  contents += `<li><a href="${url}">${el.textContent}</a></li>`;
});
document.querySelector('aside').insertAdjacentHTML('afterbegin', tpl.replace('{{contents}}', contents));
```
Получи все заголовки Следующим шагом является получение HTML-контента, который включает в себя весь текст и заголовки страницы.
Обычно контент всегда находится внутри тега Article (<article>).
```js
const article = document.getElementById(‘article’);
```
 Язык кода: JavaScript (javascript) Теперь получи все заголовки внутри тега article. Ради простоты мы выбираем только H2 и H3.
```js
const headings = article.querySelectorAll("h2, h3");
```
 Язык кода: JavaScript (javascript) Сохрани общее количество заголовков в переменной.
```js
const totalHeadings = headings.length;
```
 Язык кода: JavaScript (javascript) В нашем HTML уже есть div с id toc, который присутствует в теге article. Но ты также можешь создать его с помощью js.
```js
const toc = document.getElementById("toc");
```
 Язык кода: JavaScript (javascript) 3. Создай OL Теперь создай основной OL, который будет содержать все основные элементы списка.
```js
let tocOl = document.createElement("ol"); 
```
Язык кода: JavaScript (javascript) Создай фрагмент документа, который будет использоваться как контейнер для ol. Все элементы списка будут добавлены к нему.

Фрагмент документа здесь делает виртуальный DOM каждый раз, когда мы что-то добавляем в него. Он используется для производительности сценария, потому что он не изменяет фактические элементы DOM.
```js
let tocFragment = new DocumentFragment();
```
 Язык кода: JavaScript (javascript) Теперь создай переменную для основных элементов li.
```js
let mainLi = null;
```
 Язык кода: JavaScript (javascript) Также добавь ещё несколько переменных, которые будут использоваться в sub ul.
```javascript
let subUl = null; let subLi = null; let isSibling = false;
```