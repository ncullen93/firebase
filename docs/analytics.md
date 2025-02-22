# Analytics

One might want to integrate the authentication with Google
Analytics.

You can conditionally log event with the `log_events` method as 
well as register custom user properties with `set_user_properties`.

!!! Note Toggle Analytics
    Toggle the analytics on in your Firebase console.

## Example

```r
library(shiny)
library(firebase)

ui <- fluidPage(
  useFirebase(),
  firebaseUIContainer()
)

server <- function(input, output){
  f <- FirebaseUI$
    new()$
    set_providers(
      google = TRUE
    )$
    launch()

  a <- Analytics$
    new()$
    launch()

  observeEvent(f$get_signed_in(), {
    f$req_sign_in()

    a$log_event('notification_received');
    a$set_user_properties(level = "free")
  })
}

shinyApp(ui, server)
```
