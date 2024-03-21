# EPPS6354 Information Management workshop: Shiny

This workshop demonstrates developing a Shiny application using database server (PostgreSQL) and Shiny server.

## I. Setup environment in RStudio

1. Prerequisites
    * R 4.x
    * RStudio 2022.x

2. Install packages
    * Start up Rstudio
    * ```install.packages(c("shiny","DBI","RPostgres"))``` 
    * ```use library() function to load packages``` # e.g. library(shiny)
    * [Documentation](https://shiny.rstudio.com)
    * [Class slides](https://slides.com/karlho/im_introductiontoshiny)

3. Start up program (copy and paste into RStudio and save the file as app.R):

```
# install.packages("shiny") # If you have not installed this package, remove the # sign and run
library(shiny)

# Define UI for app that draws a histogram ----
ui <- fluidPage(
  # App title ----
  titlePanel("EPPS6354 Shiny workshop 1"),
  # Sidebar layout with input and output definitions ----
  sidebarLayout(
    # Sidebar panel for inputs ----
    sidebarPanel(
      # Input: Slider for the number of bins ----
      sliderInput(inputId = "bins",
                  label = "Number of bins:",
                  min = 1,
                  max = 50,
                  value = 30)
      
    ),
    
    # Main panel for displaying outputs ----
    mainPanel(
      
      # Output: Histogram ----
      plotOutput(outputId = "distPlot")
      
    )
  )
)

# Define server logic required to draw a histogram ----
server <- function(input, output) {
  
  # Histogram of the Old Faithful Geyser Data ----
  # with requested number of bins
  # This expression that generates a histogram is wrapped in a call
  # to renderPlot to indicate that:
  #
  # 1. It is "reactive" and therefore should be automatically
  #    re-executed when inputs (input$bins) change
  # 2. Its output type is a plot
  output$distPlot <- renderPlot({
    
    x    <- faithful$waiting
    bins <- seq(min(x), max(x), length.out = input$bins + 1)
    
    hist(x, breaks = bins, col = "forestgreen", border = "white",
         xlab = "Waiting time to next eruption (in mins)",
         main = "Histogram of waiting times")
    
  })
  
}

shinyApp(ui = ui, server = server)

```

<div align="right"><a href="https://github.com/datageneration/informationmanagement/blob/master/workshop/Shiny/2-connect_PostgreSQL.md">--> Next</a></div>

