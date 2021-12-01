# EBANX Challenge

API that handles **deposit**, **withdraw** and **transfer** events.  
It also displays account balances and reset the system if requested.  
    
### Project Setup

Clone this repository

    git clone https://github.com/JeanGT/ebanx-test.git

Access the project directory

    cd ebanx-test

Install dependencies

    composer install

Copy the example env file

    cp .env.example .env

Create an empty database and put the access credentials in .env

Perform table migration

    php artisan migrate

Run the server locally

    php artisan serve

You can now access the server at http://localhost:8000

## Database

Although a persistent storage system was not required for this challenge, I decided to use a relational database given the following structure:  

![Imgur](https://i.imgur.com/3kkK6rZ.png)


The **transfer** table records balance transfers between accounts, the **transactions** table records both withdrawals and deposits (they are differentiated by the **type** column) and the **account** table records the accounts created in which these operations are performed.  

An important point to note from the **account** table is the **balance** column: it is a column that represents the balance available on each account.  
It is possible to acquire the same information by adding up all transfers, withdrawals and deposits related to that account. However, this approach starts to become time-consuming as the system grows.  
With that in mind, this database denormalization was created together with a trigger that keeps it updated whenever there is any change in the **transfer** and **transaction** tables.  

## System Architecture

The system uses MVC architecture.  
The controllers deals with the HTTP layer and basic request input validation,  
while the models have the business logic and maintain data integrity.  

## License
[MIT](https://choosealicense.com/licenses/mit/)
