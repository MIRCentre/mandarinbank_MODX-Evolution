**protocol** - Протокол по которому пользователи заходят на ваш сайт(http или https)

**domain** - Домен вашего сайта

**port** - Порт вашего сайта, если ваш сайт находится на 80 порте, т.е. в адрессной строке после домена через двоеточие не указано число, то данный параметры указывать не прийдётся!

**protocol://domain:port/** - Может быть как `https://example.com/` так и `https://example.com:80/`

## Установка


1. Распаковываем содержимое репозитория в корень сайта
2. В системе управления переходим в `Элементы` > `Управление элементами` > `Сниппеты` > `Новый сниппет`
3. Указываем название сниппета - `mandarin`, описание - `Онлайн-оплата покупок`
4. Вставляем код приведённый ниже в поле сниппет:
```php
<?php
$output = '';
$session_mid='merchantid';#id мерчанта
$session_msec='secret';#secret мерчанта
require_once "assets/snippets/mandarin/mandarin.inc.php";

return $output;
?>
```
5. Заменяем `merchant-id` на ваш ID мерчанта(ковычки оставляем), `secret` на Ваш секретный ключ(ковычки оставляем)
6. Нажимаем кнопку `Сохранить`
7. В системе управления открываем для редактирования страницу, которая открывается после оформления заказа (&gotoid в eForm). В данном примере страница `Спасибо!`
8. Вставляем в поле `Содержимое ресурса` вызов сниппета: `[!mandarin!]`
9. Нажимаем `сохранить + продолжить`
**ВАЖНО!** не `сохранить + закрыть`, а `сохранить + продолжить`
10. Переходим в `Чанки` > форма `shopOrderForm`
11. В форме должен быть выпадающий список для выбора метода оплаты. Добавляем опцию с значением mandarin, например:
```html
<select name="payment">
  <option value="При получении">При получении</option>
  <option value="mandarin">Оплатить через MandarinBank</option>
</select>
```
12. Сохраняем сниппет
13. В системе MandarinPay указываем
- callbackURL **protocol://domain:port/assets/snippets/mandarin/callback.php**

13.1. Снова находим страницу `Спасибо!`. Допустим, её id - `16`, тогда returnURL будет выглядеть так:
- returnURL **protocol://domain:port/index.php?id=16**
