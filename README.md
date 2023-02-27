# Домашнее задание к занятию 12.4. «SQL. Часть 2» - `Мальцев Виктор`

---

Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

    фамилия и имя сотрудника из этого магазина;
    город нахождения магазина;
    количество пользователей, закреплённых в этом магазине.

Ответ:

SELECT a.first_name, a.last_name, c.city, COUNT(c2.customer_id)  
FROM sakila.staff a, sakila.store s, sakila.address a2, sakila.city c, sakila.customer c2  
where a.store_id = s.store_id and s.address_id = a2.address_id and a2.city_id = c.city_id and a.store_id = c2.store_id 
group by a.staff_id 
having COUNT(c2.customer_id) > 300;

![alt text](https://github.com/vmmaltsev/screenshot2/blob/main/Screenshot_26.png)

---

Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

Ответ:

select COUNT(film_id) 
FROM sakila.film
where `length` > (SELECT AVG(`length`) FROM sakila.film);

![alt text](https://github.com/vmmaltsev/screenshot2/blob/main/Screenshot_28.png)

---

Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, 
и добавьте информацию по количеству аренд за этот месяц.

Ответ:

select YEAR (payment_date), MONTH (payment_date), count(rental_id) 
from sakila.payment a
group by YEAR (payment_date), MONTH (payment_date)
order by sum(amount) DESC 
limit 1;

![alt text](https://github.com/vmmaltsev/screenshot2/blob/main/Screenshot_29.png)
