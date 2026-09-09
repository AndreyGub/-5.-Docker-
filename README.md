# Домашнее задание к занятию 5. «Практическое применение Docker» Губайдуллин Андрей Фаритович

---

---

## Задача 0
1. Убедитесь что у вас НЕ(!) установлен ```docker-compose```, для этого получите следующую ошибку от команды ```docker-compose --version```
```
Command 'docker-compose' not found, but can be installed with:

sudo snap install docker          # version 24.0.5, or
sudo apt  install docker-compose  # version 1.25.0-1

See 'snap info docker' for additional versions.
```
В случае наличия установленного в системе ```docker-compose``` - удалите его.  
2. Убедитесь что у вас УСТАНОВЛЕН ```docker compose```(без тире) версии не менее v2.24.X, для это выполните команду ```docker compose version```  
###  **Своё решение к задачам оформите в вашем GitHub репозитории!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!**
---
## Ответ: 
<img width="624" height="91" alt="image" src="https://github.com/user-attachments/assets/de234bf3-d983-4869-96dd-27fcf8d3b6d9" />

<img width="699" height="105" alt="image" src="https://github.com/user-attachments/assets/4366f389-0d1d-4ef5-9cb2-24dc613072e4" />
---

## Задача 1
1. Сделайте в своем GitHub пространстве fork [репозитория](https://github.com/netology-code/shvirtd-example-python).

2. Создайте файл ```Dockerfile.python``` на основе существующего `Dockerfile`:
   - Используйте базовый образ ```python:3.12-slim```
   - Обязательно используйте конструкцию ```COPY . .``` в Dockerfile
   - Создайте `.dockerignore` файл для исключения ненужных файлов
   - Используйте ```CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "5000"]``` для запуска
   - Протестируйте корректность сборки
2.1 Используйте multistage сборку вместо single stage.
3. (Необязательная часть, *) Изучите инструкцию в проекте и запустите web-приложение без использования docker, с помощью venv. (Mysql БД можно запустить в docker run).
4. (Необязательная часть, *) Изучите код приложения и добавьте управление названием таблицы через ENV переменную.
---
## Ответ: 
- 1. <img width="1323" height="625" alt="image" src="https://github.com/user-attachments/assets/9184a9b1-9ce7-4f2b-bdb3-67e4125880c4" />
- 2. <img width="798" height="293" alt="image" src="https://github.com/user-attachments/assets/01a4339b-a4e7-40e8-930d-ec484185bad6" />
 - <img width="781" height="402" alt="image" src="https://github.com/user-attachments/assets/45b0fb63-7ff9-4c40-ab46-d21a419c9515" />
 - Проверка созданных образов
docker images | grep python-app
<img width="840" height="91" alt="image" src="https://github.com/user-attachments/assets/9e027b24-0f46-4a2e-87fd-5281e6f80c97" />
 - тестируйтем корректность сборки 2.1 Используйте multistage сборку вместо single stage
 - Размер образа должен быть минимальным так каак   multistage сборке <img width="827" height="106" alt="image" src="https://github.com/user-attachments/assets/1e852d53-e371-491e-8fad-3add74559980" />
- https://github.com/AndreyGub/shvirtd-example-python/tree/main
- 
### ВНИМАНИЕ!
!!! В процессе последующего выполнения ДЗ НЕ изменяйте содержимое файлов в fork-репозитории! Ваша задача ДОБАВИТЬ 5 файлов: ```Dockerfile.python```, ```compose.yaml```, ```.gitignore```, ```.dockerignore```,```bash-скрипт```. Если вам понадобилось внести иные изменения в проект - вы что-то делаете неверно!
---

## Задача 2 (*)
1. Создайте в yandex cloud container registry с именем "test" с помощью "yc tool" . [Инструкция](https://cloud.yandex.ru/ru/docs/container-registry/quickstart/?from=int-console-help)
2. Настройте аутентификацию вашего локального docker в yandex container registry.
3. Соберите и залейте в него образ с python приложением из задания №1.
4. Просканируйте образ на уязвимости.
5. В качестве ответа приложите отчет сканирования.
---
## Ответ: 
  1.    <img width="495" height="121" alt="image" src="https://github.com/user-attachments/assets/1a140165-c886-4e52-8985-80600a0f37b3" />
  2.  <img width="958" height="605" alt="image" src="https://github.com/user-attachments/assets/f8debad6-1016-482e-bcaa-a7151b110c0e" />
-  <img width="627" height="77" alt="image" src="https://github.com/user-attachments/assets/624a07d3-d833-439c-bcd3-964ff011f2e1" />
- <img width="1349" height="488" alt="image" src="https://github.com/user-attachments/assets/97785cf0-972a-4091-b116-875d63701db1" />

---
## Задача 3
1. Изучите файл "proxy.yaml"
2. Создайте в репозитории с проектом файл ```compose.yaml```. С помощью директивы "include" подключите к нему файл "proxy.yaml".
3. Опишите в файле ```compose.yaml``` следующие сервисы: 

- ```web```. Образ приложения должен ИЛИ собираться при запуске compose из файла ```Dockerfile.python``` ИЛИ скачиваться из yandex cloud container registry(из задание №2 со *). Контейнер должен работать в bridge-сети с названием ```backend``` и иметь фиксированный ipv4-адрес ```172.20.0.5```. Сервис должен всегда перезапускаться в случае ошибок.
Передайте необходимые ENV-переменные для подключения к Mysql базе данных по сетевому имени сервиса ```web``` 

- ```db```. image=mysql:8. Контейнер должен работать в bridge-сети с названием ```backend``` и иметь фиксированный ipv4-адрес ```172.20.0.10```. Явно перезапуск сервиса в случае ошибок. Передайте необходимые ENV-переменные для создания: пароля root пользователя, создания базы данных, пользователя и пароля для web-приложения.Обязательно используйте уже существующий .env file для назначения секретных ENV-переменных!

2. Запустите проект локально с помощью docker compose , добейтесь его стабильной работы: команда ```curl -L http://127.0.0.1:8090``` должна возвращать в качестве ответа время и локальный IP-адрес. Если сервисы не стартуют воспользуйтесь командами: ```docker ps -a ``` и ```docker logs <container_name>``` . Если вместо IP-адреса вы получаете информационную ошибку --убедитесь, что вы шлете запрос на порт ```8090```, а не 5000.

5. Подключитесь к БД mysql с помощью команды ```docker exec -ti <имя_контейнера> mysql -uroot -p<пароль root-пользователя>```(обратите внимание что между ключем -u и логином root нет пробела. это важно!!! тоже самое с паролем) . Введите последовательно команды (не забываем в конце символ ; ): ```show databases; use <имя вашей базы данных(по-умолчанию virtd, как это указано в .env)>; show tables; SELECT * from requests LIMIT 10;```. Примечание: таблица в БД создается после первого поступившего запроса к приложению.

6. Остановите проект. В качестве ответа приложите скриншот sql-запроса.

## Ответ: 
1.  <img width="779" height="643" alt="image" src="https://github.com/user-attachments/assets/d1bbbcc7-33bd-438b-b948-bc80658970c0" />
2. <img width="660" height="59" alt="image" src="https://github.com/user-attachments/assets/4d71a219-d1e0-4e27-99da-2ab2566ddf11" />

3. - Подключаемся к mysql <img width="771" height="226" alt="image" src="https://github.com/user-attachments/assets/dc0a2567-d046-44dd-bd5a-c101ac8bd2ae" />
   - <img width="744" height="696" alt="image" src="https://github.com/user-attachments/assets/73dd415a-ba3c-47b4-971b-82f211aee3e7" />


## Задача 4
1. Запустите в Yandex Cloud ВМ (вам хватит 2 Гб Ram).
2. Подключитесь к Вм по ssh и установите docker.
3. Напишите bash-скрипт, который скачает ваш fork-репозиторий в каталог /opt и запустит проект целиком.
4. Зайдите на сайт проверки http подключений, например(или аналогичный): ```https://check-host.net/check-http``` и запустите проверку вашего сервиса ```http://<внешний_IP-адрес_вашей_ВМ>:8090```. Таким образом трафик будет направлен в ingress-proxy. Трафик должен пройти через цепочки: Пользователь → Internet → Nginx → HAProxy → FastAPI(запись в БД) → HAProxy → Nginx → Internet → Пользователь
5. (Необязательная часть) Дополнительно настройте remote ssh context к вашему серверу. Отобразите список контекстов и результат удаленного выполнения ```docker ps -a```
6. Повторите SQL-запрос на сервере и приложите скриншот и ссылку на fork.
## Ответ:

<img width="1076" height="678" alt="image" src="https://github.com/user-attachments/assets/d424b0bd-8fef-4bf7-b2bb-cbafa35152ae" />


<img width="1206" height="709" alt="image" src="https://github.com/user-attachments/assets/03fef397-a154-41b2-931f-5e44893fc407" />

https://github.com/AndreyGub/shvirtd-example-python.git



## Задача 5 (*)
1. Напишите и задеплойте на вашу облачную ВМ bash скрипт, который произведет резервное копирование БД mysql в директорию "/opt/backup" с помощью запуска в сети "backend" контейнера из образа ```schnitzler/mysqldump``` при помощи ```docker run ...``` команды. Подсказка: "документация образа."
2. Протестируйте ручной запуск
3. Настройте выполнение скрипта раз в 1 минуту через cron, crontab или systemctl timer. Придумайте способ не светить логин/пароль в git!!
4. Предоставьте скрипт, cron-task и скриншот с несколькими резервными копиями в "/opt/backup"

## Задача 6
Скачайте docker образ ```hashicorp/terraform:latest``` и скопируйте бинарный файл ```/bin/terraform``` на свою локальную машину, используя dive и docker save.
Предоставьте скриншоты  действий .


## Ответ:  
 1. создаем контейнер и копируем файл <img width="810" height="38" alt="image" src="https://github.com/user-attachments/assets/37997983-d8fe-4d09-b1ef-799521bea698" />
 <img width="736" height="40" alt="image" src="https://github.com/user-attachments/assets/c13cbf7d-16a8-4119-934e-82bb4ea6d789" />


 2. далее проверяем скопированный файл <img width="851" height="90" alt="image" src="https://github.com/user-attachments/assets/79f3e42b-4bae-4e98-8407-1d1f3c0cbe17" />

 3. смотрим версию terraform <img width="564" height="65" alt="image" src="https://github.com/user-attachments/assets/37243860-d0d9-4aca-8ca3-65460b8e14b4" />

 4. используем docker save <img width="807" height="71" alt="image" src="https://github.com/user-attachments/assets/dd6f9550-7d79-49b1-97ea-2a1156e6be38" />

    
