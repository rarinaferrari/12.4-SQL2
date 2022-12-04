# Домашнее задание к занятию 12.4 "Реляционные базы данных: SQL. Часть 2" - Станкевич Андрей



---

### Задание 1
Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей и выведите в результат следующую информацию:
фамилия и имя сотрудника из этого магазина,
город нахождения магазина,
количество пользователей, закрепленных в этом магазине.


```
SELECT  s.store_id, count(c.customer_id) AS "Количество покупателей",  ci.city, concat(st.last_name, ' ', st.first_name) AS "Фамилия и имя продавца"
FROM store s 
JOIN customer c ON c.store_id = s.store_id
JOIN address a ON a.address_id = s.address_id
JOIN city ci ON ci.city_id = a.city_id
JOIN staff st ON st.store_id = s.store_id
GROUP BY s.store_id, ci.city_id, st.staff_id 
HAVING count(c.customer_id) > 300

```
![изображение](https://user-images.githubusercontent.com/97339527/205489052-15a88d5a-61c5-4ecf-b4d8-0a2e6332f5d4.png)




---

### Задание 2

 Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```
select count(film_id) AS 'Количество фильмов'
from (select *, AVG(length) OVER () AS time FROM film) t
where time < length;

```

![изображение](https://user-images.githubusercontent.com/97339527/205489085-148bf996-5148-4e83-96d8-c6dad0b46d27.png)



---

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей и добавьте информацию по количеству аренд за этот месяц.


```
SELECT MONTH(p.payment_date) AS Месяц, SUM(p.amount) AS 'общая сумма', count(p.rental_id)  AS 'аренд за месяц'
from payment p
GROUP BY MONTH(p.payment_date)
ORDER BY sum(p.amount) DESC
LIMIT 1

```
![изображение](https://user-images.githubusercontent.com/97339527/205489103-2638586e-e302-4a23-9605-d31d90ec09d9.png)



