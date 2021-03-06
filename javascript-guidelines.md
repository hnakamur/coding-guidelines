Javascript coding guidelines
============================

Code conventions
================
Принятый стиль основан на Lua code conventions и довольно сильно отличается от принятых в Javascript мире. Приоритеты:

* Читаемость кода (в том числе единообразие).
* Уменьшение вероятности возникновения ошибок.
* Минимизация числа изменённых строк с точки зрения системы контроля версий при модификации кода.
* Производительность кода.

Скобки
------
Фигурные скобки ставятся на следующей строке и выравниваются по вертикали. Блок внутри фигурных скобок отбивается единичным отступом.

```javascript
function foo()
{
  //Do something
}

if (price > 0)
{
  //Positive
}
else
{
  //Negative
}
```

Фигурные скобки ставятся всегда!

Неправильная запись:

```javascript
if (price > 0)
  foo();
  
for (var i=0; i<10; i++)
  foo(i);
```

Правильная запись:

```javascript
if (price > 0)
{
  foo();
}

for (var i=0; i<10; i++)
{
  foo(i);
}
```

Тело `if`, `else`, `while`, `switch`, `try` и `catch` обязательно обрамляется фигурными скобками.


Пробельные символы
------------------
Максимальная длина строки — 80 символов.

Единичный отступ оформляется в 2 пробела. Использование табов запрещено.

Бинарные операторы отбиваются с обеих сторон пробелом. Унарные операторы пишутся слитно с переменной. Тернарный оператор отбивается проблеами. Символы `;`, `.` и `,` пишутся слитно с предшествующим текстом.

```javascript
var a = 1 + 2,
  b = a++,
  c = a > 0 ? 'yes' : 'no';
```

После имени функции пробел не ставится.

После ключевых слов `if`, `while`, `switch` и `catch` ставится пробел.

```javascript
if (condition)
{
  //do something
}
```

Расстановка ';' в конце строк
------------------
В конце строк обязательно ставим ';'

Пример:

```javascript
var a = 10;

if (condition)
{
  foo();
}

for (var i=0; i<10; i++)
{
  foo(i);
}
```

А так же в конце строки не должно быть пробельных символов.

Допустимы только unix line endings (\n).

Операторы сравнения
------------------
По ряду причин, связанных с неявным приведением типов, == и != лучше не использовать.

Использовать только явное сравнение вида '!==' и '==='


Использование двойного отрицания '!!'
------------------
Не используем !НИ В КОЕМ СЛУЧАЕ!
Только преобразуем в код вида.

```javascript
var a = b ? true : false;
```

Комментарии
-----------
Комментарии отбиваются тем же отступом, что и блок, который они комментируют. Для описание интерфейса функции используются многострочные комментарии перед объявлением функции.

Eсли после '//' идет текст, то должен быть пробел, в других случаях (отбивка) - не нужно.

```javascript
//------------------- sample ----------------------
/*
 * Some really useful helper
 */
function help()
{
  // Let's rock
  //TODO: some todo
  //NOTE: some note
  //HACK: very bad :( - write clean code
}

```

Именование переменных
---------------------
Никакой "венгерской нотации".

Константы именуются ЗАГЛАВНЫМИ_БУКВАМИ.

Обычные переменные, имена функций и проч. — через_подчёркивание, без заглавных букв.

Имя переменной, обычно, существительное.

Имя переменной, содержащей объект должно содержать название этого объекта

Имя переменной (таблицы), содержащей в себе коллекцию объектов обычно содержит
существительное во множественном числе (foos — коллекция объектов foo).

Имя булевой переменной, обычно, is_* (are_*, has_* и проч. формы to be), have_*,
need_*, should_*, must_*, in_*, not_* и т.п.

Количество объектов: num_*.

Именование функций
---------------------

Имя функции должно заключать в себе глагол либо заканчиваться на существительное
с окончанием -er (чаще всего когда подразумевается "функтор"), кроме специальных
случаев и декларативного кода.

Best practicies
===============

Private vs. public
------------------
Не стоит без нужды раздувать публичный контракт объектов. Имена приватных функций и переменных должны заканчиваться
символом подчеркивания.

```javascript
O = new function()
{
  var private_variable_;
  function private_function_()
  {
    //Some privacy here
  }

  this.public_function()
  {

  }
}
```

Модификация публичного контракта извне недопустима, поскольку сильно затрудняет читаемость кода.

Порядок объявлений
------------------
Интерфейс и особенности реализации класса должны быть понятны из беглого обзора кода, без вчитывания в то, что там делается внутри конкретных методов. Все переменные должны быть объявлены явно до первого использования. Примерный порядок объявлений:

```javascript
O = new function()
{
  //private variables
  //public variables
  //private functions
  //public functions
}
```

Принцип единственной отвественности
-----------------------------------
Нежелательно создавать функции, которые делают разные вещи в зависимости от параметра boolean. Это затрудняет читаемость потому что глядя на вызов невозможно сказать что эта функция делает. Желательно разбивать такие функции на две:

```javascript
//function remove(archive)

function delete()

function archive()
```

Инициализация
-------------
Следует избегать null при инициализации переменных. Если значение не определено, нужно использовать undefined.

Для того чтобы показать что объект не инициализирован можно присвоить `false` переменной, в которой должен храниться объект:

```javascript
var reader = false;
//...
if (reader)
{
  read.do_read();
}
```

Подключение js-скриптов
-----------------------
Все внешние скрипты необходимо размещать в сервисах проекта и подключать оттуда.
Путь по которому сохраняется скрипт должен выглядеть так: `js/lib/<name>/<version>/<fullfilename>.js`.
Рядом неободимо положить файл VERSION.TXT. В нем указывается версия скрипта и откуда он загружен.
Пример:

  Скрипт: `/js/lib/jquery/1.6.2/jquery-1.6.2.min.js`

  VERSION.TXT:
    version: 1.6.2
    downloaded from http://code.jquery.com/jquery-1.6.2.min.js

Для динамически подключаемых скриптов не допускается прямое использование document.write(). Вместо этого необходимо
использовать соответствующие обертки от jQuery/ExtJS и аналогов.

Кроссплатформенность
---------------------

