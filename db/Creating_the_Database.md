# Creating the database

I use PostgreSQL for most everything, I sometimes use SQLite for prototyping, but generally lean towards PostgreSQL. These instructions are for setting up on your local machine. Again you can do this however you feel comfortable with, this is just how I do it. 

## Running Postgres - Postgres.app
I've used the [Postgres.app](https://postgresapp.com/) for years. I manage the setup of databases and users with `psql` so using Postgres.app installs the Postgres engine and tooling I need to interact my databases from the cli. 

You can also use Docker or an online service such as Neon or any other Online PostgreSQL service. There are many free options available. 

---
## Database IDE - DBeaver
I use [DBeaver Community Edition](https://dbeaver.io/download/) as my tool of choice for interacting with databases for verifying structure, connectivity, and testing sql queries. I use [Jetbrains Datagrip](https://www.jetbrains.com/datagrip/) at my day job and love it. But for my side projects and learning, I prefer to use community tools and DBeaver is one of the best I've come across for databases in the free tier.

## Connect to the master database (`postgres`)

```shell
psql -d postgres -U postgres
```
NOTE: while not required (at the time of this writing anyway), it is best practice to set the password for the `posgres` user. <https://www.w3resource.com/PostgreSQL/snippets/postgresql-default-password.php>

---
## Create Database

```shell
create database polling_app;
```

---
## Create Service Account User

```shell
create user polling_svc with encrypted password '<your_secure_password>';
```

>  NOTE: Do not use `@` in your password, this will mess up Postgres connection strings. Save yourself lots of heart ache and dont include `@` symbols in your postgres passwords. 

---
## Grant Permissions to user

```shell
grant all privileges on database polling_app to polling_svc;
alter database polling_app owner to polling_svc;
```

---
## Additional Permissions
If you are using an ORM you may need to grant additional permissions. This is common for Prisma to be able to create the shadow database for migrations.

```shell
ALTER USER polling_svc CREATEDB CREATEROLE;
```
