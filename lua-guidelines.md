Приоритеты
==========

* Читаемость кода (в том числе единообразие).
* Уменьшение вероятности возникновения ошибок.
* Минимизация числа изменённых строк с точки зрения системы контроля версий при модификации кода.
* Производительность кода.

Старый код
==========

Старый код, не соответствующий гайдлайнам, должен по возможности исправляться
по ходу дела. Такие исправления оформляются отдельными коммитами.

Именование переменных
=====================

Никакой "венгерской нотации".

Константы именуются ЗАГЛАВНЫМИ_БУКВАМИ.

    THE_ULTIMATE_ANSWER = 42

Обычные переменные, имена функций и проч. — через_подчёркивание, без заглавных букв.

    SomeLongName(args) -> some_long_name(args)

Имя переменной, обычно, существительное.

Имя переменной, содержащей объект должно содержать название этого объекта
(см. XIV.3. Фабрики). (Обычно такая переменная — таблица.)

Имя переменной (таблицы), содержащей в себе коллекцию объектов обычно содержит
существительное во множественном числе (foos — коллекция объектов foo).

Линейные коллекции (в смысле ipairs) допускается называть с суффиксом _list в
случаях, когда нужно особо подчеркнуть линейность.

Имя булевой переменной, обычно, is_* (are_*, has_* и проч. формы to be), have_*,
need_*, should_*, must_*, in_*, not_* и т.п.

Количество объектов: num_*.

Пробельные символы
==================

В коде **нельзя использовать символы табуляции** (кроме мэйкфайлов). Если в
строковом литерале нужен символ табуляции, используйте

    "\t".

Строки желательно ограничивать теми кавычками, которых нет в тексте:

    "\"" -> '"'
    '\'' -> "'"
    "\"'" -> [["']]

В коде **нужно использовать отступы шириной два пробела** (**"единичный отступ"**),
кроме кода, который будет использоваться внутри Metalua. Такой код нужно
обозначить в комментариях в начале файла, и использовать отступы в три пробела.

**В конце строки не должно быть пробельных символов**.

**Максимальная длина строки — 80 символов**.

Нельзя ставить подряд больше одного пробела (кроме как для отступов в начале
строки и между "столбцами" в "табличных" данных).

Нельзя делать подряд больше одной пустой строки.

После каждой запятой и точки с запятой должен стоять пробел. Перед запятой и
точкой с запятой — не должно быть пробела.

    a, b, c

Все бинарные операторы (=, ~=, <, >, +, -, *, /, and, or, ..)  должны отделяться
пробелами слева и справа.

    a = b
    a > b
    a .. b

Оператор # и унарный минус не отделяются пробелом от операнда, но отделяются
пробелом слева.

    a > #b
    a = -b

Оператор not отделяется пробелами слева и справа.

    a = not b

Нельзя отделять пробелами скобки при вызове функций (кроме специальных
декларативных форм записи).

    a() + b()

После открывающей и перед закрывающей скобками пробел не ставится.

    a(b)

После открывающей фигурной скобки и перед закрывающей фигурной -- ставится.

    a({ b })
    { a, b }

Файл должен завершаться символом перевода строки.

Тело и заголовок неанонимной функции, занимающие вместе более одной строки
должны отделяться пустыми строками до и после.

Правила расстановки отступов
============================

FIXME: Нужны примеры! Пока — смотрите на код. -Alexander Gladysh 24.11.09 22:55

По умолчанию следует избегать разницы в отступах на соседних непустых строках
большей чем в один отступ (кроме специально оговорённых случаев).

При "разрыве" выражения и переносе части его на следующую строку в ней делается
один дополнительный отступ (кроме специально оговорённых случаев). Если
выражение разбито на несколько строк, все строки кроме самой первой начинаются с
одного дополнительного отступа.

    some_long_name_operand = some_long_name_operand_number_one
      + some_long_name_operand_number_two + some_long_name_operand_number_three
      + some_long_name_operand_number_four

В табличных, столбчатых и прочих подобных данных допускается расстановка
отступов по необходимости для сохранения столбцов, если это повышает читаемость.

    some_key       = "some_typical_value_1"
    some_other_key = "some_typical_value_2"
    third_key      = "some_typical_value_3"
    ...
    last_key       = "some_typical_value_4"

При многострочной записи код внутри, function-end, do-end, then-end,
repeat-until и подобных конструкций сдвигается вправо на один отступ.

    while
      some_long_name_operand ==
        other_long_name_operand another_long_name_operand
    do
      some_stuff()
    end

При многострочной записи конструктора таблицы, открывающая и закрывающая
фигурные скобки пишутся на новых строках с отступом, равным отступу первой
непустой строки перед открывающей скобкой.

    local t =
    {
      some_key       = "some_typical_value_1";
      some_other_key = "some_typical_value_2";
      third_key      = "some_typical_value_3";
      ...
      last_key       = "some_typical_value_4";
    }

Допускается сдвиг вправо на один отступ кода, находящегося между
begin()-end()-подобными парными конструкциями.

    TODO: example

При разделении вызова функции на несколько строк, аргументы функции сдвигаются
на ДВА отступа, закрывающая скобка — на один относительно строки с
открывающей. Открывающую скобку желательно ставить на той же строке, что и имя
функции. Желательно в этом случае писать каждый аргумент функции на новой
строке. Отступы в объявлении функции оформляются аналогично.

    long_function_name(
        with,
        many,
        many,
        parameters
      )

Если при вызове функции ей передаётся единственный аргумент, и этот аргумент —
анонимная функция, создаваемая конструкцией function-end непосредственно в
момент вызова, тело функции сдвигается на ОДИН отступ (а не на два). Ключевое
слово function пишется непосредственно после открывающей скобки вызова, без
пробела между ними. Соответствующее ключевому слову function ключевое слово end
пишется с тем же отступом, что и строка, на которой написано
function. Закрывающая скобка вызова ставится непосредственно после end-а, без
пробела между ними. Допускается запись в одну строку.

    fn(function(args)
      return some_stuff()
    end)

    foo(function(args) body() end)

Некоторы комплексные и смешанные примеры (добавляем по мере возникновения вопросов):

1.

    assert(
        action_handlers[action.tool],
        "unknown tool"
      )(
        manifest,
        cluster_info,
        param,
        machine,
        role_args,
        action
      )

2.

    machine.installed_rocks_set, machine.duplicate_rocks_set
        = luarocks_parse_installed_rocks(
            remote_luarocks_list_installed_rocks(
                machine.external_url
            )
        )

3. Допускается свешивание `..` при переносах

    writeln_flush(
        "-> blablablablablablablablablabla "
    .. blabla_blabla
    .. "': blablablablablablablablablabla"
    )

4.

    longname_a = longname_b
      [logic_operand] longname_c

5.

    if
       long_function_name(
             with,
             many,
             many,
             parameters
         ) == other_long_function(
             the,
             same
         )
    then
      body
    end

6.

    local func_name = function(
        param1,
        param2,
        longname3
      )
      body
    end

### Директива import

Для разбиения по строкам директивы import применяется специальное
форматирование, сложившееся исторически.

Каждая присваемая переменная пишется на отдельной строке. Список переменных
выравнивается по имени первой переменной.

Сама директива import пишется на отдельной строке вместе с именем импортируемой
библиотеки.

Открывающая и закрывающая фигурные скобки для списка импорта располагаются на
отдельных строках с отступом пердыдущей строки.

Список импорта разбивается по строкам с дополнительным отступом от фигурных
скобок. Элементы списка разделяются запятыми, не точкой с запятой (по аналогии
с форматированием при присваивании списка переменных).

Пример:

    local arguments,
          optional_arguments,
          method_arguments
          = import 'lua-nucleo/args.lua'
          {
            'arguments',
            'optional_arguments',
            'method_arguments'
          }

Если список импорта состоит из одного элемента, то директива import может
форматироваться либо в одну строку, с соблюдением всех общих правил, либо
разбиваться по строкам, как описано выше.

Пример:

    local is_table = import 'lua-nucleo/type.lua' { 'is_table' }

    local is_table
          = import 'lua-nucleo/type.lua'
          {
            'is_table'

### Многострочные константы

Для строк, заключенных в long brackets, правила для отступов **не действуют**.
Отступы расставляются так, чтобы при выводе строка выглядела так, как нужно.

Пример:

      io.stdout:write([[

    Config format:

    ]])

      io.stdout:flush()

FIXME: Нужно описать: return and or, нестандартный сдвиг влево при
конкатенации, многострочное условие if-then while-do for-do, (что ещё?!)
-Alexander Gladysh 24.11.09 22:56

Избыточный синтаксис
====================

Нельзя ставить скобки вокруг условия в if-then, while-do, for-do, repeat-until.

    if(a == b) then -> if a == b then

Синтаксический сахар
====================

Если функция не рекурсивная, используется форма определения a = function() end.

    local a = function(args)
      ...
    end

Если функция рекурсивная -- function a() end.

    local function a(args)
      ...
    end

При вызове методов нужно пользоваться оператором ":".

    t.method(t, args) -> t:method(args)

Нельзя опускать скобки при передаче строковых литералов и конструкторов таблиц в
качестве аргументов функций, если код написан в императивном стиле.

    TODO: example

В коде, написанном в декларативном стиле, желательно опускать скобки при
передаче строковых литералов и конструкторов таблиц в качестве аргументов
функций. (В т. ч. "import".)

Скобки при вызове функции с табличным литералом рекомендуется опускать
в следующих случаях

1. При декларативной записи.
2. Когда функция трансформирует таблицу в другую таблицу (пример: tset())
3. Когда функция сериализует таблицу (пример: luabins.save())

Нельзя опускать, когда функция просто что-то делает с таблицей
(например какой-нибудь count_number_of_keys()).

Правильно:

    api:input { };

    api:input
    {
    };

Неправильно:

    api:input
    { };

Циклы
=====

* Запрещается использовать `ipairs()`. Вместо него — numeric for.

* По возможности нужно избегать конкатенации в цикле с использованием
  переменной-аккумулятора. Вместо этого используйте concatter.

  Нежелательно:

    local s = ""
    for ... do
      s = s .. "something" .. foo()
    end
    return s

  Желательно:

    local cat, concat = make_concatter()
    for ... do
      cat "something" (foo())
    end
    return concat()

Функции
=======

### Проверка аргументов

#### Штатная проверка аргументов

    local is_log_enabled_raw = function(
        modules_config,
        levels_config,
        module_name,
        level
      )
      arguments(
          "table", levels_config,
          "table", modules_config,
          "string", module_name,
          "number", level
        )
      ...
    end

#### Аргументы по умолчанию

    local foo = function(bar)
      bar = bar or BAZ
      arguments(
          "quo", bar
        )

Конструкторы таблиц
===================

Если таблица создаётся на одной строке, желательно отделять её элементы
запятыми. Если список разделён запятыми, в конце списка "висящая" запятая
не ставятся.

    local ks = { "k1", "k2", "k3" }

Если таблица создаётся на нескольких строках, желательно отделять её элементы
точками с запятой, и располагать по одному элементу на строке.
Если список разделён точками с запятой, в конце списка также ставится точка
с запятой.

    local items =
    {
      "item1";
      "item2";
      "item3";
    }

Нельзя смешивать запятые и точки с запятой в одном списке.
Исключение — длинные таблицы однородных элементов, в которые
скорее всего нечасто придётся вчитываться, поскольку их содержимое очевидно:

    local letters =
    {
      "a", "b", "c", "d", "e";
      "f", "g", "h", "i", "j";
      "k", "l", "m", "n", "o";
      "p", "q", "r", "s", "t";
      "u", "v", "w", "x", "y";
      "z";
    }

    -- Конкретно это должно было бы быть записано при помощи tset().
    local lua51_keywords =
    {
      ["and"] = true,    ["break"] = true,  ["do"] = true;
      ["else"] = true,   ["elseif"] = true, ["end"] = true;
      ["false"] = true,  ["for"] = true,    ["function"] = true;
      ["if"] = true,     ["in"] = true,     ["local"] = true;
      ["nil"] = true,    ["not"] = true,    ["or"] = true;
      ["repeat"] = true, ["return"] = true, ["then"] = true;
      ["true"] = true,   ["until"] = true,  ["while"] = true;
    }

Видимость переменных
====================

Область видимости переменных должна быть максимально ограничена, насколько
позволяет здравый смысл в каждой конкретной ситуации.

Глобальные переменные запрещены (кроме специальных случаев). Любой случай
введения новой глобальный переменной должен утверждаться отдельно и
документироватья в коде.

Видимость переменных в глобальном scope файла следует максимально ограничивать
блоками do-end.

    local some_stuff
    do
      local some_local_func = function(...)
      end

      some_stuff = function(args)
        ...
        some_local_func(...)
        ...
      end
    end

Не следует повторно использовать одну и ту же переменную для разных целей (кроме
документированных случаев, где это необходимо из-за сверхжёстких требований по
производительности — на практике таких случаев пока не было).

Имена переменных не должны перекрывать имена переменных во внешних scope'ах
(допускаются обоснованные исключения, например в случаях, когда это улучшает
читаемость кода).

Стандартные глобальные переменные (например, print, error) желательно
"кешировать" в локальные в начале файла: local print, error = print, error. Это
позволяет создать код, который будет без "из коробки" работать внутри sandbox'а
с заменённым глобальным окружением.

    local type, setmetatable, tostring, select, assert, unpack
        = type, setmetatable, tostring, select, assert, unpack

    local os_time, os_date
        = os.time, os.date

Описание объектов
=================

Следует придерживаться следующего формата.

FIXME: Раскрыть; описать варианты с метатаблицами и upvalue как допустимые, и случаи, в которых они предпочтительны.)

    local make_myobject
    do
      local method = function(self, args)
      end

      make_myobject = function(args)
        return
          {
            method = method;
            --
            private_variable_ = 42;
          }
      end
    end

Поля таблицы с подчеркиванием в конце - приватные данные.

Модули
======

Разделение кода на файлы
========================

Общая культура программирования
===============================

В коде следует избегать использования безымянных "магических констант":
http://en.wikipedia.org/wiki/Magic_number_(programming)#Unnamed_numerical_constants

Именование функций
==================

Имя функции должно заключать в себе глагол либо заканчиваться на существительное
с окончанием -er (чаще всего когда подразумевается "функтор"), кроме специальных
случаев и декларативного кода.

Предикаты: is_<verb>
Фабрики: make_<object_name>

Именование тестов
=================

Имя теста должно описывать, что проверяет тест. Имя должно писаться без пробелов;
отдельные слова в имени разделяются дефисом.

Примеры:

    test:case "cookie-management" (function()
      ...

    test "POST-user-defined-Content-Type" (function()
      ...

Идентификаторы в имени теста пишутся как есть.

Пример:

    test:case "shell_escape-empty-string" (function ()
        ensure_strequals("shell_escape for an empty string", shell_escape(""), "''")
    end)

Устаревшие выражения языка
==========================

Текущим стандартом языка является Lua 5.1. Нельзя использовать в коде
выражения и методы, которые были объявлены в нем устаревшими, даже если они
еще работают. К таким в частности относятся:

* `arg` (таблица переменных, переданных в функцию открытым списком) —
  вместо неё надо использовать select(n, ...)
* `string.len` - вместо него надо использовать оператор длины #
* `table.getn` - вместо него надо использовать оператор длины #


Подключение логгеров
====================

Логгеры должны присутствовать в каждом файле каждой библиотеки
ниже lua-aplicado.

Логгеры подключаются в самом начале файла так:

    local log, dbg, spam, log_error
         = import 'LIBRARY/log.lua' { 'make_loggers' } (
             "update-subtrees", "UST"
           )

Логгеры в файлах тестов именуются аналогично примеру ниже:

    local log, dbg, spam, log_error
         = import 'LIBRARY/log.lua' { 'make_loggers' } (
             "test/config_dsl", "T001"
           )

Вместо LIBRARY подставьте имя библиотеки с нужным вариантом make_loggers.

Если правите файл, в котором они подключены по старой схеме
(с отдельным импортом `make_loggers`),
желательно отдельным коммитом привести его в современный вид.

#### Использование логгеров

В логгерах нет необходимости использовать функции преобразования к строке. Это происходит автоматически

Неверно:

    local t = { key = "value" }
    local n = 123
    local b = false
    log(tstr(t), tostring(n), tostring(b))

Верно:

    local t = { key = "value" }
    local n = 123
    local b = false
    log(t, n, b)

В логгерах запрещено использовать многострочные комментарии, это связано с особенностями парсинга строк
логов сервисов в боевом режиме.

Неверно:

    log("values:\nb = ", b, "\n c = ", c)

Верно:

    log("values: b = ", b, "; c = ", c)


Используйте адекватные ситуации логгеры, для ошибок - log_error, для рутиннной информации - log,
для отладки - dbg.

Неверно:

    log("values: b = ", b)
    log("THIS IS ERROR!!! b = ", b)
    log("debug output: b = ", b)

Верно:

    log("values: b = ", b)
    log_error("wrong value b = ", b)
    dbg("b = ", b) -- TODO: remove after debug is over

По возможности не используйте конкатенацию внутри логгеров, передавайте информацию в виде набора переменных.

Неверно:

    log("values: b = " .. b .. "; c = " .. c)

Верно:

    log("values: b = ", b, "; c = ", c)

#### Обязательное логирование

1. math.randomseed при его установке в какое-либо значение

Обработка ошибок
================

При вызове ошибки стоит использовать `error(...)`, а не `assert(nil, ...)`.
Данная рекомендация введена для улучшения читаемости кода и не имеет иного
практического смысла.

Рекомендуется оставлять комментарий o сути произошедшей ошибки.

Неверно:

    assert(a)

Верно:

    assert(a, "some bad things happened")

Если вам пришёл баг-репорт со стектрейсом, в котором стоит `assert` без
error message, необходимо в обязательном порядке добавить в код error message.

Если комментарий в `assert(...)` требует конкатенации, то стоит использовать
`if not + log_error + error`.

Неверно:

    assert(
        a == b,
        "value of a: " .. tstr(a) .. "  is not equal to value of b: " .. tstr(b)
      )

Верно:

    if not a == b then
      log_error("value of a:", a, "value of b:", b)
      error("a not equal b")
    end
