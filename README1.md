﻿# Дипломная работа по курсу Инженер по тестированию+
# Работа с базой данных
Задание 1

Представь: тебе нужно проверить, отображается ли созданный заказ в базе данных.

Для этого: выведи список логинов курьеров с количеством их заказов в статусе «В доставке» (поле inDelivery = true). 

Запрос:

     SELECT c.login, COUNT(o.id) AS "deliveryCount"
       FROM "Couriers" AS c
       LEFT JOIN "Orders" AS o ON c.id = o."courierId"
       WHERE o."inDelivery" = true
       GROUP BY c.login;
       
Скриншот результата находится в файле - sql1task.png

Задание 2

Ты тестируешь статусы заказов. Нужно убедиться, что в базе данных они записываются корректно.

Для этого: выведи все трекеры заказов и их статусы. 

Статусы определяются по следующему правилу:

Если поле finished == true, то вывести статус 2.

Если поле canсelled == true, то вывести статус -1.

Если поле inDelivery == true, то вывести статус 1.

Для остальных случаев вывести 0.

Запрос:

    SELECT track,
              CASE
            WHEN finished = true THEN 2
            WHEN cancelled = true THEN -1
            WHEN "inDelivery" = true THEN 1
      ELSE 0 END AS status
          FROM "Orders";
       
Скриншот результата находится в файле - sql2task.png

# Автоматизация теста к API

Задание:

Теперь автоматизируй сценарий, который подготовили коллеги-тестировщики:

Клиент создает заказ.

Проверяется, что по треку заказа можно получить данные о заказе.

Шаги автотеста:

Выполнить запрос на создание заказа.

Сохранить номер трека заказа.

Выполнить запрос на получения заказа по треку заказа.

Проверить, что код ответа равен 200.

# Запуск теста

Для запуска необходимо в файл configuration.py скопировать ссылку стенда в переменную URL_SERVICE без слеша в конце.

Тест запускается в файле create_orders.py