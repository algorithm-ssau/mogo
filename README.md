# Инструкция по размещению сайта в интернете с хостингом на вашем компьютере

Перед вами пример сайта mogo созданный BrainsCloud. 12 видеоуроков по созданию этого сайте доступны по ссылке https://www.youtube.com/watch?v=ltMSrSis9ww

## Требования
* Windows 10 c включенным WSL или
* Ubuntu 16.04 или
* MacOS или
* Виртуализация 

## Видео помощь
https://www.youtube.com/watch?v=vzojwG7OB7c&t=764s

## Установка
Далее рассматривается вариант установки хостинга на Windows 10 c включенным WSL. Для других опреационных систем какие-то шаги можно пропустить либо заменить на соответствующие команды.

1. Склонировать репозиторий на ваш компьютер

2. Включить Windows Subsystem for Linux (подсистема Linux в Windows 10)
    > Меню пуск -> Turn Windows features on or off -> Windows Sybsystem for Linux

3. Установить Ubuntu 16.04 через Microsoft Store
    > Меню пуск -> Store -> Ubuntu 16.04

4. Запустить Ubuntu 16.04 через меню Пуск, придумать логин, пароль и подтвердить пароль
    > Меню пуск -> Ubuntu 16.04

5. Обновить Ubuntu 16.04
    > sudo apt-get update && sudo apt-get upgrade

6. Установить web-сервер apache2
    > sudo apt-get install apache2

7. Запустить сервер apache2
    > sudo service apache2 restart

8. Зайти в браузер и набрать localhost и убедиться, что доступна страница apache

9. Ваша подсистема Linux доступна в Winodws по адресу (пример – какие-то цифры могут отличаться)
    > %USERPROFILE%\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu16.04onWindows_79rhkp1fndgsc\LocalState\rootfs

    Внутри этого раздела доступны раздел пользователя
    > \home\your_login

    И раздел с вашей вебстраничкой
    > \var\www

10. Заменить index.html в разделе \var\www файлами из готового макета (index.html + assets)

11. Зайти в браузер и набрать localhost и убедиться, что доступна новая страница

13. В настройках вашего домашнего роутера сделать переадресацию порта 80 роутера порт 80 вашего ноутбука – смотри видео 32 минута + Как открыть порт 80 в Windows Firewall https://pureinfotech.com/open-port-firewall-windows-10/

13. В Google Domains выбрать и приобрести домен (цена 12 долларов в год), в настройках разрешить динамическую привязку DNS (Dynamic DNS) – смотри видео 35 минута

14. Скопировать скрипт dns_update_script.sh в /home/your_login для уведомления Google о вашем динамическом IP. Замените в скрипте username, password, www.youname.domain вашими данными из Google Domains

15. Запустить скрипт по расписанию (будет выполняться раз в час) как указано в видео 46 минута. Это не обязательно если у вас статичный IP или просто вы хотите просто попробовать, тогда достаточно выполнить скрипт 1 раз
    > chmod +x dns_update_script.sh

    > ./dns_update_script.sh

16. Зайти на Google Domains и проверить в каком формате получен IP от вашей системы. Если в формате IPv6 (Type AAAA), то в WSL нужно поменять формат на IPv4

    > sudo nano /etc/gai.conf

    и убрать комментарий в строке precedence ::ffff:0:0/96  100

    > precedence ::ffff:0:0/96  100
    

17. Подождать до полчаса пока Google найдет ваш хостинг и пользоваться новым сайтом



