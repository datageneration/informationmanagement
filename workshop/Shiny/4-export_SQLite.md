# EPPS6354 Information Management workshop: Shiny

This workshop demonstrates developing a Shiny application using database server (PostgreSQL) and Shiny server.

## IV. Export database to SQLite for deployment

### Convert database from SQL file (DLL + DML) using DB Browser

  - Open DB Browser, import NBAplayers.sql (File --> Import --> Database from SQL file)
  - Choose a filename to save under (use nba)

Now, you have the nba database file (nba.db) in SQLite format!


### Import SQLite database in RStudio

Use the following R program (app.R) to import and run Shiny app.  

**Note**: This is primarily the same as last program using PostgreSQL (local) except changing the connect to SQLite.  Be sure you store the nba.db file in the same folder as app.R!
```
#install.packages(c("shiny","DBI","RPostgres","RSQLite"))
library(shiny)
library(DBI)
library(RPostgres)
library(RSQLite)

# Define UI for application
ui <- fluidPage(
  sliderInput("nrows", "Enter the number of rows to display:",
              min = 1,
              max = 519,
              value = 15),
  # tableOutput("tbl")
  dataTableOutput("tbl")
)

# Define server logic
server <- function(input, output) {
  table <- renderDataTable({

    # sqllite
    # Be sure the data file must be in same folder
    sqlite_conn <- dbConnect(RSQLite::SQLite(), dbname ='nba.db')
    
    # Create SQL commmand to join variables from tables for query
    
    sqlite_sql="SELECT p.id, p.first_name, p.last_name, p.full_name, pp.urlPlayerHeadshot FROM player p INNER JOIN player_photos pp ON pp.idplayer=p.id WHERE p.is_active=1"

    conn=sqlite_conn
    str_sql = sqlite_sql
    
    on.exit(dbDisconnect(conn), add = TRUE)
    table_df = dbGetQuery(conn, paste0(str_sql, " LIMIT ", input$nrows, ";"))
    table_df$headshot<-c(paste0('<img src="', table_df$urlplayerheadshot, '"></img>'))
    table_df<-table_df[c('full_name', 'headshot')]
  }, escape = FALSE)
  
  output$tbl <- table
}

# Run the application 
shinyApp(ui = ui, server = server)

```
<div align="left"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/Shiny/3-connect_NBAdatabase.md"><-- Back</a></div>
<div align="right"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/Shiny/5-deploy_app.md">--> Next</a></div>

