# Secure templates
 Web task for [M*CTF](https://mctf.mtuci.ru) Finals 

**Описание задания:**

Кажется я забыл убрать строку ввода на своём сайте. Думаю с ней ничего не случится 

https://ip:1337

**English**

It seems I forgot to remove the input line on my site. I don't think anything will happen to it.

https://ip:1337

## Run
```bash
cd mctf-final-secure-templates
sudo docker-compose up -d 
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

В качестве альтернативы можно использовать *exploit.py*. Через него можно запускать единичные команды или пробросить обратную оболочку.

![image](/images/exploit_test.gif)

## Flag
```
mctf{tW1g_C0dE_Ex3c}
```
