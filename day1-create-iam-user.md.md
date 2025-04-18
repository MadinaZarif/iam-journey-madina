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



# 📘 5: Создание Subnet

---

## ✅ Что я сделала

1. **Перешла в раздел Create Subnet** и выбрала VPC `Staging Area`  
   ![Выбор VPC при создании Subnet](screenshots/26.png)

2. **Ввела имя** Subnet `Stading 1`, выбрала **CIDR-блок** `10.10.0.0/20`  
   ![Имя и начальный CIDR Subnet](screenshots/27.png)

3. **Уточнила зону доступности** `us-east-1a` и задала CIDR `10.10.1.0/24`  
   ![Указание зоны и точного CIDR](screenshots/28.png)

4. **Нажала Create Subnet**  
   ![Кнопка для завершения создания Subnet](screenshots/29.png)

5. **Успешное создание Subnet**, она отобразилась в списке  
   ![Подтверждение успешного создания Subnet](screenshots/30.png)

6. Проверила в VPC Dashboard — всё отображается корректно  
   ![Информация по VPC после создания Subnet](screenshots/21.png)  
   ![VPC список с новой подсетью](screenshots/22.png)

---

## 💡 Что я поняла

- Subnet создаётся внутри выбранной VPC  
- CIDR-блок Subnet должен быть вложен в CIDR-блок VPC  
- Можно указать зону доступности (AZ) для распределения ресурсов по зонам  
- Название Subnet и теги помогают ориентироваться при работе с несколькими подсетями

6:  Создание второй подсети и просмотру карты ресурсов

1. Выбор VPC для новой подсети.
2. Ввод имени подсети `Staging 2`.
3. Выбор зоны доступности (например, `us-east-1b`).
4. Назначение блока IPv4 CIDR `10.10.2.0/24`.
5. Добавление тега `Name = Staging 2`.
6. Нажатие кнопки **Create subnet**.
7. Убедились, что подсеть успешно создана и отображается в списке.
8. Проверка карты ресурсов — обе подсети `Staging 1` и `Staging 2` подключены к одной таблице маршрутов.

### 📸 Скриншоты

![Step 1](screenshots/31.png)  
![Step 2](screenshots/32.png)  
![Step 3](screenshots/33.png)  
![Step 4](screenshots/34.png)  
![Step 5](screenshots/35.png)  
![Step 6](screenshots/36.png)  
![Step 7](screenshots/37.png)  
![Step 8](screenshots/38.png)

## 7: Создание и привязка Internet Gateway к VPC

1. Переход в раздел **Internet gateways** в AWS VPC Dashboard.  
2. Нажатие кнопки **Create internet gateway**.  
3. Ввод имени Internet Gateway: `Stading-Internet-Gateway`.  
4. Добавление тега `Name = Stading-Internet-Gateway`.  
5. Нажатие кнопки **Create internet gateway**.  
6. Убедились, что Internet Gateway создан, но пока **не привязан** к VPC.  
7. Выбор созданного IGW → **Actions** → **Attach to VPC**.  
8. Выбор VPC `Staging Area` (`vpc-06e47771d6f9f4370`) и привязка IGW.  
9. Убедились, что Internet Gateway успешно привязан (статус **Attached**).  
10. Проверка в списке Internet Gateways — новый IGW теперь привязан к нужной VPC.

### 📸 Скриншоты

![Step 1](screenshots/39.png)  
![Step 2](screenshots/40.png)  
![Step 3](screenshots/41.png)  
![Step 4](screenshots/42.png)  
![Step 5](screenshots/43.png)  
![Step 6](screenshots/44.png)  
![Step 7](screenshots/45.png)  
![Step 8](screenshots/46.png)  
![Step 9](screenshots/47.png)
## 🌐 7: Настройка маршрутов и интернет-шлюза для VPC

Настроим таблицу маршрутов для связи подсетей с интернет-шлюзом `Stading-Internet-Gateway`.

---

### ✅ Шаги выполнения

1. Перейдите в раздел **Route tables** в консоли AWS.
2. Найдите таблицу маршрутов, связанную с VPC `Staging Area`.
3. Откройте её и нажмите **Edit routes**.
4. Убедитесь, что маршрут `10.10.0.0/16 → local` уже присутствует.
5. Добавьте новый маршрут:
   - `Destination`: `0.0.0.0/0`
   - `Target`: `Internet Gateway` → `Stading-Internet-Gateway`
6. Нажмите кнопку **Save changes**.
7. Убедитесь, что маршрут появился в таблице.
8. Перейдите в **Resource map** и проверьте, что обе подсети (`Staging 1`, `Staging 2`) связаны с этой таблицей маршрутов и интернет-шлюзом.

---

### 📸 Скриншоты процесса

| Шаг | Изображение |
|-----|-------------|
| 1. Открываем Route Tables | ![Step 1](screenshots/48.png) |
| 2. Таблица маршрутов | ![Step 2](screenshots/49.png) |
| 3. Детали таблицы | ![Step 3](screenshots/50.png) |
| 4. Проверка локального маршрута | ![Step 4](screenshots/51.png) |
| 5. Добавление маршрута к IGW | ![Step 5](screenshots/52.png) |
| 6. Выбор IGW | ![Step 6](screenshots/53.png) |
| 7. Успешное обновление маршрутов | ![Step 7](screenshots/54.png) |
| 8. Карта ресурсов — проверка связей | ![Step 8.1](screenshots/55.png)<br>![Step 8.2](screenshots/56.png) |

---

📘 **Итог:** теперь оба сегмента вашей VPC (`Staging 1` и `Staging 2`) имеют доступ к интернету через интернет-шлюз `Stading-Internet-Gateway` и правильно настроенную таблицу маршрутов.
