library(tidyverse)
library(CodeClanData)
library(shiny)
library(bslib)

game_sales <- CodeClanData::game_sales

user_score <- game_sales %>% 
  distinct(user_score) %>% 
  arrange(user_score) %>% 
  pull()

critic_score <- game_sales %>% 
  distinct(critic_score) %>% 
  arrange(critic_score) %>% 
  pull()

years <- game_sales %>% 
  distinct(year_of_release) %>% 
  arrange(year_of_release) %>% 
  pull()

publisher <- game_sales %>% 
  distinct(publisher) %>% 
  pull()

ui <- fluidPage(
  
  titlePanel("Games"), 
  
  sidebarLayout(
    sidebarPanel(
      selectInput ("publisher_input", 
                       "Name", 
                       choices = publisher),

      sliderInput("years_input", 
                       "Year of release",
                       min=1988, max=2016, value = 1, step=1), 
      
  ),
  mainPanel(
    DT::dataTableOutput("table_output")
  )
)
)

server <- function(input, output) {
  
  output$table_output <- DT::renderDataTable({
    game_sales %>%
      filter(year_of_release == input$years_input) %>% 
      filter(publisher == input$publisher_input)
      
  })
}

shinyApp(ui = ui, server = server)