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

- Application Migration Service: Launch Template Customization

В этом шаге мы перешли к **Launch Template**, который управляет параметрами запуска инстансов EC2 после миграции с использованием **Application Migration Service** (MGN).

## Что мы сделали:

1. Перешли в `Settings > Launch template`.
2. Нажали на кнопку **Edit**, чтобы изменить настройки шаблона.
3. Активировали:
   - `Instance type right sizing` — AWS автоматически подбирает оптимальный тип инстанса.
   - `Start instance upon launch` — инстанс автоматически запускается после миграции.
4. Выбрали:
   - `Use AWS provided license` — используем лицензию AWS.
   - `Boot mode` — используем `Use source`.
5. В блоке **Default EC2 Launch Template**:
   - Изменили **Default target subnet** на `Staging 2`.
   - Можно добавить **Additional security groups** (по желанию).
   - Настроили **Default instance type**, если необходимо.

> Все изменения применяются только к новым серверам, добавленным после сохранения шаблона.

---

## Скриншоты

- ![Launch template изменён](/screenshots/2%20day/7.png)
- ![Настройки шаблона - Target Subnet](/screenshots/2%20day/8.png)
- ![Выбор Subnet из выпадающего списка](/screenshots/2%20day/9.png)
- ![Редактирование шаблона запуска](/screenshots/2%20day/10.png)
- ![Сохранённый шаблон запуска](/screenshots/2%20day/11.png)
-------------------


Post-Launch Template Overview

## Описание

На этом этапе мы настраиваем **Post-launch template** в AWS Application Migration Service. Данный шаблон позволяет задать действия, которые будут выполнены **после запуска серверов**, реплицированных в AWS.

## Основные настройки

### Post-launch actions

- ✅ *Install the Systems Manager agent and allow executing actions on launched servers*
    - Это включает установку AWS SSM Agent и разрешение выполнения post-launch действий.
    - ![SSM Agent Enabled](/screenshots/2%20day/13.png)

- ⚠️ При отключении этого параметра **SSM agent не устанавливается**, и никакие действия после запуска не выполняются.
    - ![SSM Agent Disabled](/screenshots/2%20day/12.png)

### Deployment

- Выбор между:
  - `Test and cutover instances (recommended)` – рекомендуется выполнять действия на обоих типах инстансов.
  - `Cutover instances only`
  - `Test instances only`

  - ![Deployment Options](/screenshots/2%20day/14.png)

### Encryption

- ⚪ *Encrypt action parameters* — можно включить для шифрования параметров действия.
    - ![Encryption Options](/screenshots/2%20day/15.png)

## Вывод

В рамках урока **никакие изменения внесены не были**. Цель заключалась в том, чтобы **показать**, как выглядит страница настройки Post-launch template и какие параметры можно изменить при необходимости.

> Это обзорный шаг. Все изменения будут применяться **только к вновь добавленным серверам** после настройки шаблона.
# AWS Application Migration - Post-launch Template

## Post-launch Template Overview

Перед началом миграции рекомендуется проверить настройки **Post-launch template**. Этот шаблон позволяет конфигурировать действия, которые будут автоматически выполняться **после запуска сервера** в AWS.

---

## Основные Настройки

### Post-launch actions
- ✅ *Install the Systems Manager agent and allow executing actions on launched servers*  
  При включении, AWS установит **SSM Agent** на целевые серверы, чтобы выполнять автоматические действия.  
  📌 Также создаются необходимые IAM роли.

![Post-launch enabled](/screenshots/2%20day/12.png)

---

### Deployment
- ✅ *Test and cutover instances (recommended)* — Рекомендуется активировать для тестов и рабочих инстансов.

![Deployment setting](/screenshots/2%20day/13.png)

---

### Encryption
- Можно опционально включить **Encrypt action parameters**, что зашифрует параметры действия по умолчанию.

---

### Сценарий Без Активированной Опции
Если не активировать агент, как видно на скрине ниже — ни одно пост-действие не будет выполнено:

![Post-launch disabled warning](/screenshots/2%20day/14.png)

---

## Подтверждение Сохранения
После сохранения настроек:

![Saved post-launch](/screenshots/2%20day/15.png)

---

## Вывод по Уроку

В этом разделе мы не изменяли никаких настроек вручную. Основная цель — убедиться, что все параметры по умолчанию подходят под нужды проекта.

Также:

- При необходимости можно изменить Deployment или включить шифрование.
- Убедитесь, что опция **Migration tips** включена в разделе `User preferences`. Это поможет во время миграции получать подсказки от AWS:

![User preferences - tips off](/screenshots/2%20day/16.png)
![User preferences - tips on](/screenshots/2%20day/17.png)

---

## Резюме

- Проверили **Post-launch template**.
- Убедились, что включён **SSM Agent**.
- Активированы советы по миграции.
- Все изменения сохраняются и применяются к новым серверам.

---



