# devoops
dev'oops 🤷

## In GitHub
```kotlin
val myPersonalGithubAccount = "gyam"
val sharedSecret = goTo(avatar.menu, Settings.menuitem, `Developer settings`.sidebar,
        `Personal access tokens`.sidebar, `Generate new token`.button) andConfigure {
        `repo:status`.choice     = true
        `admin:repo_hook`.choice = true
} andCopyToken()

val organization = GitHub.Organization("gyam020816")
val jenkinsUrl   = "https://blueocean.ci.duskforest.xyz"

goTo(organization.page, Settings.tab, Webhooks.sidebar, `Add webhook`.button) andConfigure {
    `Payload URL`.text        = "$jenkinsUrl/github-webhook/"
    `Content type`.choice     = "application/json"
    `Secret`.password         = sharedSecret
    `SSL verification`.choice = "Enable SSL verification"
    `Which events would you like to trigger this webhook?`.multichoice andConfigure {
         `Pull requests`.checkbox = true
         Pushes.checkbox          = true
     }
     Active.checkbox          = true
}

return GitHubStep(organization, myPersonalGithubAccount, sharedSecret)
```

## In Jenkins (for GitHub)
```kotlin
val previousGitHubStep = githubStep()
val jenkinsProjectName = "some-jenkins-project-name"
goTo(`New Item`.sidebar) andConfigure {
    type.choice = "GitHub Organization"
    name        = jenkinsProjectName
} andConfigure {
    category(Projects) andConfigure {
        category(`GitHub Organization`) andConfigure {
            `API endpoint`.choice = "GitHub"
            `Credentials`.choice  = Add.button andSelect "Jenkins" andConfigure {
                Kind.choice           = "Username with password"
                Username              = previousGitHubStep.myPersonalGithubAccount
                Password              = previousGitHubStep.sharedSecret
                ID                    = "org-${previousGitHubStep.organization}"
            }.andSelect()
            Owner.text            = previousGitHubStep.organization
            Behaviours.bundle     = listOf(
                item(`Discover branches`) andConfigure {
                    Strategy.choice = "All branches"
                }
            )
        }
    }
}
```
