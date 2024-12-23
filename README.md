Инструкция по применению компилятора и виртуальной машины C$ (Си-доллар).
-
Язык программирования ```С$``` был придуман в целях написания сценариев (особенно хорошее применение найдёт в геймдеве).
Можно рассматривать как альтернативу и замену – Pawn (устаревший и малофункциональный) с Lua (не Си-подобный).
В остальном имеется много всяких годных плюшек, которых нет в том же Pawn/Lua и прочих скриптовых языках.

Файлы для исходных кодов на ```C$``` используют расширение (формат) – `cdlr`, для откомпилированных в байт-код – `bccdlr` <br><br>
Точка выполнения скрипта начинается с создания основной функции. Есть два стандартных подхода к этому: <br>

1]: придумываем любое название для функции (обычно не применяется на практике);<br>
2]: название для функции соответствует имени файла (часто применимо на практике);<br>
<br>
В обоих случаях расположение функции должно быть в самом начале скрипта. <br>

| Вариант | Исходный код: |
|---------|---------------|

| № | на английском | на русском |
|---------|---------------|------------|
| ```1``` | ```1``` ```declare function ExecuteScript(){}```       | ```1``` ```объявить функцию ВыполнитьСкрипт(){}```     |
| ```2``` | ```1``` ```declare function ScriptEntryPoint(){}```    | ```1``` ```объявить функцию точкаВходаВскрипт(){}```   |
| ```3``` | ```1``` ```declare function Script(){}```              | ```1``` ```объявить функцию Скрипт(){}```              |
| ```4``` | ```1``` ```declare function 0(){}```                   | ```1``` ```объявить функцию 0(){}```                    |
<br>
Исходя из того, что функции выполняют какие-либо действия, то и названия у них должны быть соответствующие. На мой взгляд, первый вариант можно считать самым подходящим.<br>
<br>
Вызовем функцию не имеющую названия (безымянная).<br><br>

< файл: ```0.cdlr``` (исходный код на языке ```C$```)><br>
```1``` ```call function 0(); ``` | ```1``` ```вызвать функцию 0();```<br>
<br>
При попытке скомпилировать такой файл, получите семантическую ошибку, о том, что данная конструкция является пустой и бессмысленной, т.к. внутри неё не оказалось ни одной вложенной инструкции.
По этой причине на выходе файл: ```0.bccdlr``` для ```VM-C$``` создан не будет.<br>

Рекурсивный вызов функции (по умолчанию в целях безопасности выключен компилятором, дабы не опытным кодерам не наделать глупостей)<br>
<br>
< файл: ```0.cdlr``` ><br>
```1``` ```declare function 0()```<br>
```2``` ```{```<br>
```3``` ```    call function 0();```<br>
```4``` ```}```

Байт-код сгенерирован не будет, вы получите семантическую ошибку об использовании рекурсии. Рекурсия в программировании – это способ вызвать функцию внутри самой себя.
Если же хотите включить рекурсию, используйте инструкцию: ```recursive function call:```, со флагом: ```enable/disable``` или ```рекурсивный вызов функций: включить/выключить```, но будьте предельно осторожны, помня о том, что необходимо создать условие для выхода из бесконечного вызова.

---------------------
* Продолжение следует
---------------------
