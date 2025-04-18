# Day 2 – Application Migration Service (Part 1)

## 🚀 Шаг 1: Инициализация Application Migration Service

Перед тем как работать с replication template, нужно один раз инициализировать сервис в нужном регионе. Это действие:

- создаёт все нужные IAM роли (например, `AWSApplicationMigrationServiceRole`)
- активирует MGN в регионе
- даёт доступ к разделу **Settings → Replication template**

✅ Так как я нахожусь под root-пользователем, мне не нужно переключаться — у меня есть все права.

👉 Я нажимаю кнопку **Set up service** на стартовом экране.

---

## 🛠 Шаг 2: Настройка replication template

После инициализации перехожу в:

**Settings → Replication template → Edit**

### Основные параметры шаблона:
- **Subnet** → выбираю `Staging1` (создана мной заранее)
- **Instance type** → по умолчанию `t3.small`
- **Volume type** → `gp3`
- **Encryption** → по умолчанию
- **Security group** → использую стандартную
- **Use private IP** → включено
- **Public IP** → по желанию (оставляю как есть)

🔒 Важно: всё это влияет на то, как будет проходить репликация машин из on-premises в AWS.

---

## ✅ Шаг 3: Сохранение и проверка

- Нажимаю **Save template**
- Вижу подтверждение, что шаблон сохранён
- Повторно захожу в **Edit**, чтобы убедиться, что выбрана нужная подсеть `Staging1`

---

### 📸 Скриншоты
📸 Скриншоты:
![Step 1](screenshots/2%20day/1.png)  
![Step 2](screenshots/2%20day/2.png)

---
from pathlib import Path

# Markdown content with image links
markdown_content = """
# Day 2 – Part 1: Изучение и редактирование Replication Template

Когда мы заходим в **Replication Template**  
(*replication — это процесс копирования и синхронизации данных из одного источника в другой*),  
мы можем видеть **шаблон по умолчанию (default template)**.

Если настройки по умолчанию не подходят под наши требования, мы можем внести изменения с помощью кнопки **Edit**.

В данном случае я изменила **Subnet**, выбрав подсеть, которую создала ранее — `Staging1`.

---

## 🔧 Что можно изменить в шаблоне:

- Подсеть для staging-серверов
- Тип инстанса для репликации (по умолчанию `t3.small`)
- Тип EBS-томов (например, `gp3`)
- Использование публичного или приватного IP
- Применение шифрования
- Группы безопасности и ширина пропускной способности

---

## 📸 Скриншоты

> Файлы размещены в папке `screenshots/2 day`

- **Edit Replication Template**  
  ![Edit Replication Template](screenshots/2%20day/1.png)

- **Replication Settings Overview**  
  ![Replication Settings Overview](screenshots/2%20day/2.png)

- **Sidebar: Settings Section**  
  ![Settings Section](screenshots/2%20day/3.png)

- **Source Servers Section**  
  ![Source Servers](screenshots/2%20day/4.png)

- **Template with Updated Subnet**  
  ![Updated Subnet](screenshots/2%20day/5.png)

- **Template Saved Confirmation**  
  ![Saved Configuration](screenshots/2%20day/6.png)
"""


-------------------
Продолжение следует во второй части второго дня 🌐


