# wireapps_backend

#Q1
| HTTP Method | URL                        | Description                                                             |
|-------------|----------------------------|-------------------------------------------------------------------------|
| POST        | /login                     | Authenticate a user by username and password                            |
| GET         | /medications               | Retrieve a list of all medications                                       |
| GET         | /medications/{id}          | Retrieve a specific medication by ID                                     |
| POST        | /medications               | Add a new medication (Only the Owner can perform this action)            |
| PUT         | /medications/{id}          | Update an existing medication (Managers and Cashiers can perform this action)|
| PATCH       | /medications/{id}          | Soft delete a medication record (Managers and Cashiers can perform this action)|
| DELETE      | /medications/{id}          | Permanently delete a medication record (Only the Owner can perform this action)|
| GET         | /customers                 | Retrieve a list of all customers                                         |
| GET         | /customers/{id}            | Retrieve a specific customer by ID                                       |
| POST        | /customers                 | Add a new customer (Only the Owner can perform this action)              |
| PUT         | /customers/{id}            | Update an existing customer (Managers and Cashiers can perform this action)|
| PATCH       | /customers/{id}            | Soft delete a customer record (Managers and Cashiers can perform this action)|
| DELETE      | /customers/{id}            | Permanently delete a customer record (Only the Owner can perform this action)|
