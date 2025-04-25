## Agent-Based Linux Migration to AWS
🔄 Подключение локального Linux-сервера к AWS MGN через агент

После подготовки Linux-сервера следующим этапом стало подключение его к AWS Application Migration Service через агент репликации.

🖥️ **Почему я использовала VirtualBox**  
Я не хотела переносить свой основной Windows-профиль в облако. Вместо этого я установила Ubuntu в VirtualBox и именно эту виртуальную машину использовала в качестве исходного сервера. Таким образом, я могла безопасно экспериментировать и настраивать окружение без риска.

### 📦 Установка агента репликации на Ubuntu VM

1. Перешла на страницу официальной документации AWS и скопировала **региональную ссылку** на скрипт установки агента.
2. Выполнила загрузку установочного скрипта:
   ```bash
   curl -o aws-replication-installer-init.py https://aws-application-migration-service-us-east-1.s3.us-east-1.amazonaws.com/latest/linux/aws-replication-installer-init.py
   Подтвердила, что скрипт скачался:

bash
Copy
Edit
ls -l
Запустила установку агента, указав:

регион (--region)

account-id

access-token

Пример команды:

bash
Copy
Edit
sudo python3 aws-replication-installer-init.py \
  --region us-east-1 \
  --account-id 9135-2492-2182 \
  --token <ваш_токен> \
  --no-prompt
Агент начал установку, но несколько раз возникали ошибки, связанные с некорректным ключом доступа или истёкшим токеном.
🛠️ Решение: пришлось удалить старый ключ доступа и создать новый, затем скопировать его с локальной Windows в виртуальную Ubuntu (см. ниже).

🔄 Копирование из Windows в VirtualBox Ubuntu
📌 Чтобы иметь возможность копировать и вставлять из Windows в гостевую Ubuntu:

Убедилась, что установлены Guest Additions (через меню Устройства → Установить дополнения гостевой ОС)

Включила буфер обмена:
Устройства → Общий буфер обмена → Двусторонний

Перезапустила Ubuntu VM

✅ Успешное подключение к AWS MGN
Когда команда с новым ключом прошла успешно, в консоли появилось сообщение:

python-repl
Copy
Edit
The installation of the AWS Replication Agent has started.
AWS Region Name: us-east-1
...
На стороне AWS MGN статус сервера изменился на:

Data replication status: Initial sync 4% | 37 min left

Migration lifecycle: Not ready

Next step: Wait for initial sync to complete

🌱 Это означало, что мой сервер действительно загружен в песочницу AWS, и процесс синхронизации запущен.

📷 Скриншоты

Сервер успешно зарегистрирован, начата синхронизация

![Step 1](screenshots/4%20day/1.png)  
![Step 2](screenshots/4%20day/2.png)
![Step 3](screenshots/4%20day/3.png)
![Step 4](screenshots/4%20day/4.png)  
