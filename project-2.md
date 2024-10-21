# Project 2 answers

How many users do we have?

Answers: 79.8%

```
 select sum(is_frequent_buyer) / sum(is_buyer) as repeat_rate
  from dev_db.naeemosama921gmailcom.fact_user_orders;



```


What are good indicators of a user who will likely purchase again? What about indicators of users who are likely NOT to purchase again? If you had more data, what features would you want to look into to answer this question?

Answers: To assess whether a user is likely to make another purchase, I would examine their previous ordering patterns, including the quantity of orders, the variety of products bought, and the overall spending. Additionally, I would analyze their activity on the website, such as the number of page views, sessions, and the time spent on the site. If a user made a purchase using a promotion or discount, they may be less inclined to buy again. I would also consider the user’s interaction with other marketing efforts, like email campaigns, as well as their ratings or reviews on the website.

```




More stakeholders are coming to us for data, which is great! But we need to get some more models created before we can help. Create a marts folder, so we can organize our models, with the following subfolders for business units:

Answers: 3.89 days


```
More stakeholders are coming to us for data, which is great! But we need to get some more models created before we can help. Create a marts folder, so we can organize our models, with the following subfolders for business units:

Product: fact_page_views
Core: fact_orders
Marketing: fact_user_orders
```

Explain the product mart models you added. Why did you organize the models in the way you did?
Product:

fact_page_views: The model I created looks at the various events. These events are page_view, add_to_carts, checkouts, packages_shipped, session_length_minutes. The grain is event_id and it is joined to the order items and session timings.


Core:

fact_orders: Contains individual orders as the grain. Contains address and count of order items.


Marketing:

fact_user_orders: At the user level. Contains products purchased and frequent buyer data.

```


Part 2: Tests
What assumptions are you making about each model? (i.e. why are you adding each test?)
I would like to add more tests than just the ones below, but ran out of time this week.

Addresses:

address_guid not null, unique zipcode and not null

Events:

event_guid not null

Order Items:

order_guid not null and product_guid not null

Orders:

order_guid not null and unique

Products:

product_guid not null and unique

Users:

user_guid not null and unique

```

Did you find any “bad” data as you added and ran tests on your models? How did you go about either cleaning the data in the dbt model or adjusting your assumptions/tests?

zipcoda data did not have 5 digits and some contains 4 digits.



Part 3: dbt Snapshots
Run the product snapshot model using dbt snapshot and query it in snowflake to see how the data has changed since last week


  select *
  from dev_db.naeemosama921gmailcom.product_snapshot