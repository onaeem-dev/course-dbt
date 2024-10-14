# Project 1 answers

How many users do we have?

Answers: 130

```
select count(*)
from dev_db.naeemosama921gmailcom.stg_postgres__users
```


On average, how many orders do we receive per hour?

Answers: 7.520833

```

with orders_per_hour as (
  select
    date_trunc('hour', created_at) as order_hour
  , count(distinct(order_id)) as number_of_orders
  from dev_db.naeemosama921gmailcom.stg_postgres__orders
  group by order_hour
)

select
  avg(number_of_orders) AS avg_orders_per_hour
from orders_per_hour;
```



On average, how long does an order take from being placed to being delivered?

Answers: 3.89 days


```
with delivery_time AS (
  select
    order_id
  , created_at
  , delivered_at
  , timestampdiff(day, created_at, delivered_at) AS delivery_days
  from dev_db.naeemosama921gmailcom.stg_postgres__orders
  where delivered_at is not null
)

select
  avg(delivery_days) AS avg_delivery_days
from delivery_time;
```



How many users have only made one purchase? Two purchases? Three+ purchases?

Answers:
25, 28, 71

```
with orders_per_user AS (
  select
    user_id
  , count(distinct order_id) AS number_of_orders
  from dev_db.naeemosama921gmailcom.stg_postgres__orders
  group by user_id
)

select
  count(user_id) as users
, case
    when number_of_orders = 1 then '1 order'
    when number_of_orders = 2 then '2 orders'
    when number_of_orders >= 3 then '3 or more orders'
  end as orders_per_user
from orders_per_user
group by orders_per_user
order by orders_per_user;
```




On average, how many unique sessions do we have per hour?
Answers: 16.33

with sessions_per_hour as (
  select
    date_trunc('hour', created_at) as session_hour
  , count(distinct(session_id)) as number_of_sessions
  from dev_db.naeemosama921gmailcom.stg_postgres__events
  group by session_hour
)

select
  avg(number_of_sessions) AS avg_sessions_per_hour
from sessions_per_hour;