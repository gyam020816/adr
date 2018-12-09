# devoops
dev'oops 🤷

## In GitHub
```kotlin
val organization = GitHub.Organization("gyam020816")
val jenkinsUrl = "https://blueocean.ci.duskforest.xyz"

goTo(organization.page, Settings.tab, Webhooks.sidebar, `Add webhook`.button) andConfigure {
  `Payload URL`.text = "$jenkinsUrl/github-webhook/"
  `Content type`.choice = "application/json"
  `Secret`.password = 
  `SSL verification`.choice = "Enable SSL verification"
  `Which events would you like to trigger this webhook?`.multichoice andConfigure {
     `Pull requests`.checkbox = true
     Pushes.checkbox = true
   }
   Active.checkbox = true
}
```
