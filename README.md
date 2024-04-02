# index
# Задание 1
Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.

# Ответ 1

![alt text](https://github.com/StepanovSA/index/blob/main/index1.png)


# Задание 2
Выполните explain analyze следующего запроса:
```
select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id, f.title)
from payment p, rental r, customer c, inventory i, film f
where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id
```
перечислите узкие места;
оптимизируйте запрос: внесите корректировки по использованию операторов, при необходимости добавьте индексы.

# Ответ 2
Время до оптимизации: 

![alt text](https://github.com/StepanovSA/index/blob/main/index2.1.png)

Оптимизировав запрос:
```
select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id)
from payment p, customer c
where date(p.payment_date) = '2005-07-30' and p.customer_id = c.customer_id 
```
получаем время запроса гораздо меньше 
![alt text](https://github.com/StepanovSA/index/blob/main/index2.2.png)

