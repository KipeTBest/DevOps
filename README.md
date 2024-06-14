## Описание системы
- **Oracle VM Box (версия: 7.0.14)**
- **Linux Ubuntu (версия: 24.04)**

## Задание 1

### Описание

Написать bash скрипт, который создаст для всех пользователей системы отдельную директорию в корневой директории с именем пользователя и установит для нее права 755. При этом владельцем директории должен быть соответствующий пользователь. Путь до корневого каталога создания директорий должен определяться через ключ `-d` или, если ключ не задан, то должен быть диалог для определения пути пользователем. Лог должен писаться как в `stdout`, так и в файл.

### Использование

1. Создайте файл `creator_users_dirs.sh`.
2. Вставьте код, представленный в файле `Task_01`, и сохраните файл.
3. Дайте скрипту права на выполнение (`chmod +x creator_users_dirs.sh`).
4. Запустите файл в режиме `sudo` (`sudo ./creator_users_dirs.sh`).
5. Скрипт запросит ввести путь до директории (например, `/`).
6. После завершения работы скрипта проверьте корректность выполнения:
    - Убедитесь, что директория создалась: `ls /` (должна быть в списке).
    - Проверьте права доступа: `ls -l /kipet` (в данном случае `kipet` - пользователь). Должно появиться `drw.... kipet kipet data time`.

### Результат

Скрипт успешно выполнен, результат проверки прав: `drwxrwxr-x 2 kipet kipet 4096 дата время файлы`.

**UPD:** Файл со скриптом создан в домашней директории. Там же будет создан второй файл - `script-log.txt`, в который будет записан вывод скрипта, включая создание различных файлов.

## Задание 2

### Описание

Задание по Ansible:
написать playbook который должен будет:
Создать пользователя на удаленной машине
Сделать авторизацию ssh по ключам для пользователя
Отключить авторизацию по паролю на сервере
Создать директорию в /opt/ с правами для пользователя.

### Использование

Установка Ansible:

sudo apt update

sudo apt install ansible -y

Создание файла setup_user.yml:

nano setup_user.yml

Вставляем playbook

Запускаем playbook:

ansible-playbook setup_user.yml

Проверяем:
ssh -i ~/.ssh/id_rsa myuser@localhost
sudo cat /etc/ssh/sshd_config | grep PasswordAuthentication
sudo cat /home/myuser/.ssh/authorized_keys
ls -ld /opt/my_directory

![photo_1_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/88a5c1ca-469a-4270-9347-33c5cf02ec21)
![photo_2_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/f35f418d-f4a3-4e11-8c4f-ffd056a4f234)
![photo_3_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/17a44e39-1432-444d-8eed-80e48fb10883)
![photo_4_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/c71f682d-0bd8-4f7e-a67c-f064711ab561)
![photo_5_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/febe934e-0e37-451d-b9f9-a4c7fa20eaad)
![photo_6_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/8f884b82-e158-41c7-8b3b-14f676046637)
![photo_7_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/45b2fc4b-d2de-48a2-8835-8a9c2664afc1)
![photo_8_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/804de575-ff57-4bda-81d6-af9f40ed223d)
![photo_9_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/03490fb3-bdf6-4905-8299-74731625248e)
![photo_10_2024-06-14_14-55-53](https://github.com/KipeTBest/DevOps/assets/90268471/c9f5116b-8eb4-43e5-8665-28f25a90a7cf)


## Задание 3

### Описание

Напишите Dockerfile для создания образа, который будет содержать веб-сервер Apache или Nginx и базу данных MySQL или postgresql. В Dockerfile должны использоваться инструкции: FROM, MAINTAINER, RUN, CMD, WORKDIR, ENV, ADD, COPY, VOLUME, USER, EXPOSE.
Dockerfile должен содержать комментарии с пояснениями того, что делается. 
Собранный образ должен иметь имя вида <фамилия>_<инициалы>_image_<текущая дата>. Рядом с dockerfile должен быть скрин, на котором будут видны все слои вашего image и их размер на диске и команда, которой вы это выведете.

### Результат
![fcH9gqrAJo](https://github.com/KipeTBest/DevOps/assets/90268471/c99c653e-ccd8-49bc-8c59-7c9ca368bb3d)
![faYAW9sjUn](https://github.com/KipeTBest/DevOps/assets/90268471/55abdeb2-c2cf-48dc-8753-b99ef98497fc)
![kyGpe8wdYH](https://github.com/KipeTBest/DevOps/assets/90268471/216bd780-762d-4bd7-83fc-b872e65fe394)

Сделан в Task_03

## Задание 4

### Описание

Напишите docker compose конфиг, для разворачивания двух контейнеров в одной сети (10.10.10.0/28) типа bridge: 
1 - Nginx или Apache или ваше самописное приложение на выбор, ему должны передаваться конфигурационные файлы через volume, порт 80 из контейнера должен быть доступен на хостовой машине по порту 8080
2 - mysql или postgres, каталог для хранения данных должен монтироваться как docker volume, docker volume должен быть описан в том же конфигурационном файле docker compose. Сервис с БД должен быть доступен из контейнера с веб-сервером по именам new_db, dev_db.

### Результат
![ApplicationFrameHost_LzrXRxQDl6](https://github.com/KipeTBest/DevOps/assets/90268471/2d49ec3a-8382-4ec9-b916-d394060f00c9)

Сделан в Task_04
