# Домашнее задание к занятию "`SQL. Часть 2`" - `Пономарев Денис`

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

```
SELECT DISTINCT district
FROM address
WHERE district LIKE 'K%a'
  AND district NOT LIKE '% %';

```

![Задание1](https://github.com/ddponomarev/11_4/blob/master/img/z1.png)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```
SELECT *
FROM payment
WHERE DATE(payment_date) BETWEEN '2005-06-15' AND '2005-06-18'
  AND amount > 10.00;

```

![Задание2](https://github.com/ddponomarev/11_4/blob/master/img/z2.png)

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

```
SELECT *
FROM rental
ORDER BY rental_date DESC
LIMIT 5;

```

![Задание3](https://github.com/ddponomarev/11_4/blob/master/img/z3.png)

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом. Добавьте вычисляемую колонку «Премия». Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

```
SELECT
    LOWER(first_name),
    LOWER(last_name),
    REPLACE(LOWER(first_name), 'll', 'pp')
FROM customer
WHERE active = 1
  AND first_name IN ('Kelly', 'Willie');

```

![Задание4](https://github.com/ddponomarev/11_4/blob/master/img/z4.png)

### Задание 5*

Найдите фильмы, которые ни разу не брали в аренду.

```
SELECT
    email,
    SUBSTRING_INDEX(email, '@', 1) AS email_local_part,
    SUBSTRING_INDEX(email, '@', -1) AS email_domain
FROM customer;
```

![Задание5](https://github.com/ddponomarev/11_4/blob/master/img/z5.png)
