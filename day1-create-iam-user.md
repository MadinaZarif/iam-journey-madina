# 📘 Day 1: Создание IAM пользователя `MigrationAgent`

**Дата:** 2025-04-18

---

## ✅ Что я сделала

- Перешла в IAM Console
- Создала пользователя `MigrationAgent`
- Отключила доступ к AWS Management Console
- Перешла к шагу назначения политик

---

## 💡 Что я поняла

- Пользователю нужен только **программный доступ**, через Access Key
- Это безопаснее, чем давать доступ к Console
📸 Скриншот: 
![Шаг 1 – Создание IAM пользователя](screenshots/1.png)

![Шаг 2 – Назначение политики](screenshots/2.png)

![Шаг 3 – Подтверждение доступа](screenshots/3.png)


2: Назначение IAM политик
## ✅ Что я сделала

- Назначила пользователю две политики:
  - `AWSApplicationMigrationAgentPolicy`
  - `AWSApplicationMigrationFullAccess`


---

## 💡 Что я поняла

- Агент использует эти политики для подключения к AWS и миграции машин
- После миграции желательно ограничить права пользователя

📸 Скриншот: 
![Назначение политик пользователю – Permissions tab](screenshots/3a.png)

![Подтверждение добавления политик AWSApplicationMigration...](screenshots/7.png)


3: Создание Access Key для MigrationAgent

## ✅ Что я сделала

- Перешла в IAM → Users → MigrationAgent
- Перешла во вкладку "Security credentials"
- Создала Access Key:
  - Use case: Command Line Interface
- Сохранила Access Key и Secret Access Key в защищённый файл

📸 Скриншоты:
- 

---

## 💡 Что я поняла

- Secret Access Key **можно увидеть только один раз**
- Лучше **не использовать этот ключ дольше, чем нужно**
- После миграции ключ можно **деактивировать или удалить**
![Профиль пользователя - отключённый Console Access](screenshots/9.png)

![Раздел Access Keys – пока нет ключей](screenshots/10.png)

![Выбор use case для ключа (CLI, локальный код и т.д.)](screenshots/11.png)

![Подтверждение безопасности перед созданием ключа](screenshots/12.png)

![Генерация Access Key и рекомендации](screenshots/13.png)


4. Создание VPC
✅ Перешла в раздел VPC Dashboard

✅ Нажала Create VPC

✅ Выбрала опцию VPC only

✅ Указала CIDR-блок 10.10.0.0/16

✅ Назначила тег Staging Area

✅ Успешно создала VPC

💡 Что я поняла
Опция VPC only создаёт только VPC, без дополнительных ресурсов (Subnets, IGW и т.д.)

CIDR 10.10.0.0/16 даёт возможность создать до 65,536 IP-адресов

VPC можно помечать тегами для удобного поиска и учёта

После создания — можно подключать Internet Gateway, Subnet и т.д.
![Переход в Recently Visited и VPC](screenshots/16.png)

![VPC Dashboard с разделами и ресурсами по регионам](screenshots/17.png)

![Создание VPC – выбор VPC only, CIDR, имя](screenshots/18.png)

![Настройка CIDR, отключение IPv6, тег "Staging Area"](screenshots/19.png)

![Финальные параметры и создание](screenshots/20.png)

![VPC создана – статус Available и информация](screenshots/21.png)

![Просмотр списка всех VPC, новая появилась](screenshots/22.png)
