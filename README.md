# Hey Bro Nice Cat
 Web task for [M*CTF](https://mctf.mtuci.ru) Finals 

**Описание задания:**

Посмотрите на этого довольного котика. Ему точно нечего скрывать.

https://ip:1337

**English**

Look at this happy cat. He definitely has nothing to hide.

https://ip:1337

## Run
```bash
cd mctf-final-secure-templates
docker-compose up
```
## Start
In Browser: localhost:1337

## Writeup 
Нас встречает страница, всё содержание которой- gif с котом.
![image](/images/entry.png)
Открываем код страницы и видим, что помимо котика у нас есть какая-то login-form и button, причём их z-index меньше гифки, а также они невидимые, а значит гифка их перекрывает. 
Убираем стили у всего.
![image](/images/removed.png)
Тепреь посмотрим что передаётся серверу при отправке формы. 
![image](/images/request.png)
Тут стоит обратить внимание на заголовок template, передаваемый в запросе и упоминание PHP в ответе. Не иначе это обработчик шаблонов! Поискав в google можно понять, что обработкой шаблонов в PHP может заниматься шаблонизатор [Twig](https://twig.symfony.com).

После поиска уязвимостей в twig, можно наткнуться на [CVE-2022-23614](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-23614) и PoC репозиторий к ней на [Github](https://github.com/davwwwx/CVE-2022-23614), который ~~украден~~ взят за основу этого задания. В поле можно выполнить производный код, введя следующее выражение:
```bash
{{ ['id','']|sort('system') }}
```
Где id - станадрная Unix команда для вывода имени пользователя и его группы. Удаленный код выполнится и будет выведено:

![image](https://user-images.githubusercontent.com/77790965/189837506-f1373715-5d34-4dec-b8fd-0efe6bc074fc.png)


Удаленный код выполнен, а значит можно попробовать другие команды. Флаг будет находиться в переменных окружения (команда env).

![envs](/images/envs.png)
Для автоматического запроса можно использовать приложенный *exploit.py*. Через него можно запускать единичные команды или пробросить обратную оболочку.

![image](/images/exploit_test.gif)

## Flag
```
mctf{tW1g_C0dE_Ex3c}
```
