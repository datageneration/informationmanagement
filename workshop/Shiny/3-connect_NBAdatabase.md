# EPPS6354 Information Management workshop: Shiny

This workshop demonstrates developing a Shiny application using database server (PostgreSQL) and Shiny server.

## III. Connect to sample NBA database (local)

1. Prerequisites
    * Sample NBA database uploaded to server

2. Sample SQL program in Shiny directory

    * Create database named NBAplayers in PostgreSQL (using pgAdmin) and populate data using the NBAplayers.sql file (combined with DDL and data insert) 
    * Check data in pdAdmin

3. 
```
library(shiny)
library(DBI)
library(RPostgres)

# Define UI
ui <- fluidPage(
  sliderInput("nrows", "Enter the number of rows to display:",
              min = 1,
              max = 519,
              value = 15),
  tableOutput("tbl")
)

# Define server logic 
server <- function(input, output) {
  output$tbl <- renderTable({

    # postgres
    postgres_conn <- dbConnect(RPostgres::Postgres(),dbname = 'NBAplayers', 
                    #  host = '127.0.0.1',
                      port = 5432, 
                      user = 'postgres',
                      password = 'YOURPASSWORD')
    postgres_sql="SELECT * FROM player Where is_active = '1' "

    conn=postgres_conn
    str_sql = postgres_sql
    
    
    on.exit(dbDisconnect(conn), add = TRUE)
    dbGetQuery(conn, paste0(str_sql, " LIMIT ", input$nrows, ";"))
  })
}

# Run the application 
shinyApp(ui = ui, server = server)

```
<div align="left"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/Shiny/2-connect_PostgreSQL.md"><-- Back</a></div>
<div align="right"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/Shiny/4-deploy_NBAdatabase.md">--> Next</a></div>

