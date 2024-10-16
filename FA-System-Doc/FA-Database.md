- **MySQL Engine**
## Tables
### Product:

| Column              | Data Type    | Characteristics |
| ------------------- | ------------ | --------------- |
| ID                  | int          | PRIMARY_KEY     |
| name                | varchar(50)  |                 |
| category_id         | int          | FOREIGN_KEY     |
| provider_id         | int          | FOREIGN_KEY     |
| description         | varchar(200) |                 |
| metric_unit         | varchar(50)  |                 |
| unit_per_box        | double       |                 |
| quality             | varchar(50)  |                 |
| measures            | varchar(50)  |                 |
| price               | double       |                 |
| discount_percentage | int          |                 |
| discounted_price    | double       |                 |
### Category:

| Column          | Data Type   | Characteristics |
| --------------- | ----------- | --------------- |
| ID              | int         | PRIMARY_KEY     |
| name            | varchar(50) |                 |
| products_amount | int         |                 |
### Provider:

| Column          | Data Type   | Characteristics |
| --------------- | ----------- | --------------- |
| ID              | int         | PRIMARY_KEY     |
| name            | varchar(50) |                 |
| products_amount | int         |                 |
### Stock:

| Column     | Data Type | Characteristics |
| ---------- | --------- | --------------- |
| product_id | int       | FOREIGN_KEY     |
| stock      | int       |                 |
### Sale:

| Column      | Data Type | Characteristics |
| ----------- | --------- | --------------- |
| product_id  | int       | FOREIGN_KEY     |
| total_price | double    |                 |
