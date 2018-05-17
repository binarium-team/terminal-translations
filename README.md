# terminal-translations

### Ключи особого назначения
Такие ключи начинаются с символа "@"

### Конфигрурирование плюрализации
@PLURAL - ключ, описывающий правило плюрализации слов для текущего языка.
- Пример для русского языка:
```json
"@PLURAL" : "ends(1)#ends(range(2,4))#or(ends(range(5, 19)), ends(0))"
```
Здесь описываются 3 правила. У них есть приоритет, который возрастает слева направо.
```json
ends(1)
```
Форма для слова привязанного к числительному, которое заканчивается (ends) единицей (1).
Например, 21 самолёт, 441 самолёт.

```json
ends(range(2,4))
```
Форма для слова привязанного к числительному, которое заканчивается (ends), на цифры от () 2 до 4 (включительно) (range)
Например, 2 самолёта, 33 самолёта, 1004 самолёта.

```json
or(ends(range(5, 19)), ends(0))
```
Форма для слова привязанного к числительному, которое заканчивается (ends), на цифры от 5 до 19 (включительно), либо (or) заканчивается цифрой 0
Например, 0 самолётов, 111 самолётов (3-е правило приоритетнее 1-го), 10419 самолётов. 

- Пример для английского языка:
```json
"@PLURAL" : "any()#equals(1)",
```

Здесь описываются две формы слова:
```json
any()
```
Форма для слова привязанного к любому (any) числительному.
Например, 2 apples, 33 apples, 112 apples, 0 apples.

```json
equals(1)
```
Форма для слова привязанного к числительному, которое конкретно равно (equals) 1-нице.
Например, 1 apple

### Применение плюрализации
Токен, который должен плбюрализироваться в соотвествии с правилами плюрализации, выглядит следующим образом:
#{форма-для-правила-1@форма-для-правила-2@...@форма-для-правила-n?привязанная-перменная}
Пример для русского:
```json
"{{@count}} #{сделка@сделки@сделок?count}"
```
Итог:
```javascript
"1 сделка"; 
"33 сделки"; 
"12 сделок";
```

### Дополнительная информация
Создал: [sanyabeast](http://github.com/sanyabeast)
