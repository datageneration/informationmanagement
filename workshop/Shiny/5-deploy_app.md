# EPPS6354 Information Management workshop: Shiny

This workshop demonstrates developing a Shiny application using database server (PostgreSQL) and Shiny server.

## IV. Deploy to Shiny server

1. Prerequisites
    * Shinyapps account (connect using GitHub)
    * Shiny
    * Shiny app tested locally

2. Login to [Shinyapps.io](https://www.shinyapps.io/admin/#/login)

   - Signup/Login using your GitHub account

3. Check token and secret (under Account on left hand panel)

   - Add token if you do not have one yet
   - Click Show and Show Secret, copy the statement to clipboard, then OK

4. Publish in RStudio

   - Note to install one more package *rsconnect* to publish/deploy to app
   - Run the following program, when running, click on the Publish button on upper right hand corner
   - Paste the token and secret statement to establish connection
   - Be sure the choose the app.R file and nba.db file for publishing, which is to upload the portable database file to Shinyapps server

```
#install.packages(c("shiny","DBI","RPostgres","RSQLite","rsconnect"))
library(shiny)
library(DBI)
library(RPostgres)
library(RSQLite)
library(rsconnect)

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
    
    sqlite_sql="SELECT p.id, p.first_name, p.last_name, p.full_name, pp.urlplayerheadshot FROM player p INNER JOIN player_photos pp ON pp.idplayer=p.id WHERE p.is_active=1"
    
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

# Deploy


# library(rsconnect)
# rsconnect::setAccountInfo(name='yourShinyappsaccount', token='*', secret='*')
```

<div align="left"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/Shiny/4-export_SQLite.md"><-- Back</a></div>

