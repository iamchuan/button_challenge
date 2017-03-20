# button_challenge

## To create table in mysql database, first create database button in mysql and then in mysql environment do:

mysql> source create_table.sql

mysql> source update_table.sql

## The Rmd file reads data from mysql button database, so be sure to setup the connection with correct credentials:

```
con <- dbConnect(MySQL(),
                user="<user>", 
                password="<password>", 
                dbname="button", 
                host="localhost")
```

## The missing_field_classifier.ipynb uses a csv file generated from R with the following command:

```
customers_with_orders <- customers %>%
  merge(purchases %>% 
          .[, .(first_order_date = min(date),
                last_order_date = max(date)), 
            by = user_id],
        by.x = "id", by.y = "user_id", all.x = TRUE) %>%
  .[, time_between_purchases := diffdays(signup_date, last_order_date) / number_of_purchases] %>%
  .[, average_order_value := value_of_purchases / number_of_purchases] %>%
  .[, time_to_first_purchase := diffdays(signup_date, first_order_date)]
```

