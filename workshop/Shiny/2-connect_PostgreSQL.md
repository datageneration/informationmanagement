# EPPS6354 Information Management workshop: Shiny

This workshop demonstrates developing a Shiny application using database server (PostgreSQL) and Shiny server.

## II. Connect to PostgreSQL server (local)

1. Prerequisites
    * PostgreSQL server setup locally
    * Sample database uploaded to server

2. Sample R program (copy and paste into RStudio and save the file as app.R):

```

# install.packages(c("DBI", "RPostgres"))
library(DBI)
library(RPostgres)

# connect to postgres database
postgre_con <- dbConnect(RPostgres::Postgres(),
                 dbname = 'university', # name of the database from textbook
                 host = '127.0.0.1', 
                 port = 5432, 
                 user = 'postgres',
                 password = 'YOURPASSWORD') # type in your PostgreSQL/pgAdmin password

postgres_sql <- "SELECT * FROM department" # Create SQL query object

dbGetQuery(postgre_con, postgres_sql) 

department_df <- dbGetQuery(postgre_con, postgres_sql)
class(department_df)

```
<div align="left"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/Shiny/1-setup-shiny.md"><-- Back</a></div>
<div align="right"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/Shiny/3-connect_NBAdatabase.md">--> Next</a></div>

