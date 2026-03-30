# Домашнее задание к занятию "`SQL. Часть 2`" - `Пономарев Денис`

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

```
SELECT
    CONCAT(s.first_name, ' ', s.last_name) AS "Сотрудник магазина",
    cm.city AS "Город магазина",
    COUNT(c.customer_id) AS "Кол-во пользователей"
FROM staff s
JOIN store st ON st.manager_staff_id = s.staff_id
JOIN address a ON st.address_id = a.address_id
JOIN city cm ON a.city_id = cm.city_id
JOIN customer c ON c.store_id = st.store_id
GROUP BY s.staff_id, s.first_name, s.last_name, cm.city
HAVING COUNT(c.customer_id) > 300;

```
![Задание1](https://github.com/ddponomarev/11_4/blob/master/img/z1.png)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```
SELECT COUNT(*) AS "кол-во фильмов"
FROM film
WHERE length > (SELECT AVG(length) FROM film);

```
![Задание2](https://github.com/ddponomarev/11_4/blob/master/img/z2.png)

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

```
SELECT
    DATE_FORMAT(payment_date, '%Y.%m') AS "Месяц",
    SUM(amount) AS "Сумма платежей",
    COUNT(rental_id) AS "Кол-во аренд"
FROM payment
GROUP BY DATE_FORMAT(payment_date, '%Y.%m')
ORDER BY SUM(amount) DESC
LIMIT 1;

```

![Задание3](https://github.com/ddponomarev/11_4/blob/master/img/z3.png)

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

```
SELECT
    s.staff_id,
    CONCAT(s.first_name, ' ', s.last_name) AS "Сотрудники",
    COUNT(p.payment_id) AS "Кол-во продаж",
    CASE
        WHEN COUNT(p.payment_id) > 8000 THEN "Да"
        ELSE "Нет"
    END AS "Премия"
FROM staff s
JOIN payment p ON s.staff_id = p.staff_id
GROUP BY s.staff_id, s.first_name, s.last_name;

```

![Задание4](https://github.com/ddponomarev/11_4/blob/master/img/z4.png)

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.

```
SELECT f.title
FROM film f
WHERE f.film_id NOT IN (
    SELECT DISTINCT i.film_id
    FROM inventory i
    JOIN rental r ON i.inventory_id = r.inventory_id);
```

![Задание5](https://github.com/ddponomarev/11_4/blob/master/img/z5.png)
