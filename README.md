<h1 align="center">🚀 Colorizer</h1>

**Colorizer** - небольшая библиотека для работы с [цветовыми управляющими кодами](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors)

### Установка

```cmd
composer require krypt0nn/colorizer
```

### Использование

Разные способы подсветки жёлтым цветом слова "World"

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

Для выделения яркости шрифта можно использовать второй параметр *(true/false)*

* `Colors::yellow (true)`
* `new Color ('yellow', true)`
* `Colors::format ('[yellow,1]')`

Так же можно указать использование цвета фона вторым параметром (true/false)

* `Colors::yellow (false, true)`
* `new Color ('yellow', false, true)`
* `Colors::format ('[yellow,0,1]')`

Пример окна ошибки

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