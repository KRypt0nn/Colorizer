<h1 align="center">🚀 Colorizer</h1>

**Colorizer** - небольшая библиотека для работы с [цветовыми управляющими кодами](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors)

### Установка

```cmd
composer require krypt0nn/colorizer
```

### Использование

За реализацию подсветки текста отвечают классы `Colorizer\Color` и `Colorizer\Colors`. Класс `Colorizer\Colors` реализует 8 базовых функций добавления цвета в текст:

| Функция | Возвращаемый цветовой код |
| - | - |
| Colors::black | Чёрный |
| Colors::red | Красный |
| Colors::green | Зелёный |
| Colors::yellow | Жёлтый |
| Colors::blue | Синий |
| Colors::magenta | Фиолетовый |
| Colors::cyan | Голубой |
| Colors::white | Белый |

У каждой из описанных выше функций есть два дополнительных аргументы: `bool $bright = false` и `bool $background = false`. Первый отвечает за яркость цвета. К примеру, если вызвать `Colors::black()` - текст станет чёрным, а если `Colors::black(true)` - серым

Второй параметр отвечает за то, куда данный цвет должен применяться - в качестве цвета текста или цвета фона текста. Так, конструкция `Colors::red(false, true) . Colors::yellow()` будет выводить весь последующий текст с красным фоном и жёлтым цветом текста

Чтобы вернуть настройки цвета по умолчанию можно воспользоваться функцией `Colors::reset()`

Для упрощения подсветки какого-то текста существует метод `Colors::format`, принимающий в качестве аргумента строку, содержащую основной текст и необходимые к добавлению цвета в формате `[название цвета,яркость=0,фон=0]`. К примеру, `Colors::format('Hello, [yellow]World[reset]!')` вернёт строку, в которой слово "World" будет подсвечено жёлтым. А из примера выше `Colors::format('Hello, [red,0,1][yellow]World[reset]!')` сделает "World" написанным жёлтым цветом по красному фону

> Обратите внимание на то, что все методы данной библиотеки возвращают управляющие символы, задающие цвета для текста внутри CLI. Это значит, что функция `Colors::yellow()` не делает весь выводимый на экран текст жёлтым. Она возвращает управляющий код, который можно дописать в нужное вам место внутри вашего текста и уже самостоятельно вывести этот текст на экран. Аналогично функция `Colors::format()` лишь заменяет цвета, написанные внутри квадратных скобок, на управляющие коды. Чтобы вывести подсвеченный текст - используйте стандартные операторы вывода, к примеру, функцию `echo`. Примеры этого можно посмотреть ниже

#### Разные способы подсветки жёлтым цветом слова "World"

```php
<?php

use Colorizer\Colors;

echo 'Hello, '. Colors::yellow () .'World'. Colors::reset () .'!';
```

```php
<?php

use Colorizer\Color;

echo 'Hello, '. new Color ('yellow') .'World'. new Color ('reset') .'!';
```

```php
<?php

use Colorizer\Colors;

echo Colors::format ('Hello, [yellow]World[reset]!');
```

#### Пример окна ошибки

```php
<?php

use Colorizer\Colors;

echo Colors::format ('[red,0,1][white]                                            
    [yellow,1]WARNING![white]                                
    Something went wrong                    
                                            [reset]');
```

```php
<?php

use Colorizer\Dialog;

echo (new Dialog ('Something went wrong', 'WARNING!'))
    ->background ('red')
    ->foregroundCaption ('yellow')
    ->width (30);
```

```php
<?php

use Colorizer\Dialog;

echo Dialog::new ('Something went wrong', 'WARNING!')
    ->background ('red')
    ->foregroundCaption ('yellow')
    ->width (30);
```

Автор: [Подвирный Никита](https://vk.com/technomindlp). Специально для [Enfesto Studio Group](https://vk.com/hphp_convertation)
