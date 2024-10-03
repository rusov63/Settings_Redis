## Установка, настройка и работа с Redis

### Операционная система Ubuntu.

1. [ ] Обновляем список пакетов:

        apt-get update
2. [ ] Выполняем установку:

        apt-get install redis-server
3. [ ] Разрешаем автозапуск сервиса:

        systemctl enable redis-server
4. [ ] Запуск сервиса:

        systemctl start redis-server
5. [ ] Перезагрузка Redis сервера:

        systemctl restart redis-server

6. [ ] Проверка состояния сервера:
Если в строке Active: active (ranning) значит сервер работает.

        service redis-server status
7. [ ] Посмотреть версию установленной СУБД можно командой:

        redis-server --version


### Операционная система Linux Manjaro.
1. [ ] Обновление системы:

        sudo pacman -Suy
2. [ ] Установка:

        sudo pacman -Sy redis
3. [ ] Проверяем работоспособность:

        sudo systemctl status redis

4. [ ] Запустить Redis:

        sudo systemctl start redis

5. [ ] Перезапуск:
        
        sudo systemctl restart redis   

### Проверка работоспособности:

1. [ ] Подключаемся удаленно к серверу:

        redis-cli -h 192.168.43.37 -p 6379 -a 37DQhAt5MBq34Lj24Ppn5LI/UZksAZJQ==
        
        Локальное подключение: redis-cli
2. [ ] Пропингуем СУБД: 
192.168.43.37:6379>

        PING
        Если команда выполнена успешно, получим: PONG
3. [ ] Проверяем функционал создания ключей:
        
       set test "Hello, world"
4. [ ] После этого сервер отдаст ответ OK. Запросим файл:

       get test
       На экране отобразится сообщение "Hello, world"
5. [ ] Закрываем консоль: exit. 

6. [ ] Чтобы убедиться в том, что изменения сохраняются после перезагрузки Redis, перезапускаем:

       sudo systemctl restart redis
7. [ ] И еще раз запрашиваем сохраненные ключи: get test. Если все выполненные действия завершились без ошибок, 
       Redis работает корректно.


### Установка. Docker.

* Выполняем загрузку образа Redis:

        docker pull redis

* Запускаем контейнер:
для первого раза запуска уберем флаг -d и посмотрим логи программы, возможно выйдет ошибка, что нет подключения к redis.

        docker run -d --name redis-server -p 6380:6379

* Проверим, что наш контейнер запустился:

        docker ps

* Мы должны увидеть: наш сервис запущен на порту 6380; к нему можно обращаться по имени redis-server или ID a8c30431268c.

        CONTAINER ID   IMAGE   COMMAND    CREATED    STATUS   PORTS      NAMES
        a8c30431268c   redis   "docke…"   4 sec...   Up 3...  6380/tcp   redis-server

* Чтобы войти в контейнер Redis, порт указываем тот, что указали в redis.conf

         docker exec -it redis-server redis-cli -p 6380

* 127.0.0.1:6380> ping
         (error) NOAUTH Authentication required.
* 127.0.0.1:6380> auth 6OPD4ltb39S80UT7swbhkYdyoH2jAKBM8g==%
OK
* 127.0.0.1:6380> ping
PONG
* 127.0.0.1:6380> set test 'ffff'
OK
* 127.0.0.1:6380> get test
"ffff"


Настройки Redis для бота смотри в проекте:
* generalmedical_bot (Dockerfile, Docker_and_Redis.txt, и локально на компьютере)

Дополнительная литература
* https://help.reg.ru/support/servery-vps/oblachnyye-servery/ustanovka-programmnogo-obespecheniya/kak-ustanovit-i-nastroit-redis-na-linux#5
* https://timeweb.cloud/tutorials/redis/ustanovka-i-nastrojka-redis-dlya-raznyh-os
* https://habr.com/ru/articles/821363/
* https://www.dmosk.ru/miniinstruktions.php?mini=redis-ubuntu#examples
