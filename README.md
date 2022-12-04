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




---

### Задание 2

 Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```
select count(film_id) AS 'Количество фильмов'
from (select *, AVG(length) OVER () AS time FROM film) t
where time < length;

```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 2](ссылка на скриншот 2)`


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

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`


