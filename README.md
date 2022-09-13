# Mctf-final-secure-templates
 Web task for [M*CTF]() Finals 

**Описание задания:**

Мне нравится обработчик флаблонов Twig. Мне кажется он довольно безопасный. 

https://ip:1337

**English**

I prefer Twig template engine. I think it's sesure enough.

https://ip:1337

## Build 
```bash
cd mctf-final-secure-templates
./build.sh
```
## Start
In Browser: localhost:1337

## Writeup 

После поиска уязвимостей обработчика шаблонов twig, можно наткнуться на [эту](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2022-23614). После этого найти PoC репозиторий на [Github](https://github.com/davwwwx/CVE-2022-23614), который ~~украден~~ взят за основу этого задания. В поле задания можно выполнить производный код, введя следующее выражение:
```bash
{{ ['id','']|sort('system') }}
```
Где id - станадрная Unix команда для вывода имени пользователя и его группы. Удаленный код выполнится и будет выведено:

вставь картинку тут

Удаленный код выполнен, а значит можно попробовать что-то ещё, например почитать системные файлы. Флаг будет находиться в файле /etc/passwd.

сюда вставь ещё картинку

## Flag
```
mctf{tW1g_C0dE_Ex3c}
```