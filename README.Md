
# Template for BDDs Automation Repository

Use this template to create a new module of the node js framework to test a new feature.





## Installation

1.- Create a new repository in Bitbucket using following naming convention:

```bash
  <PROJECT-NAME>-BDDS-TESTS
```

2.- Create a new folder locally

```bash
  mkdir my-project
  cd my-project
```

3.- Clone this template with following command so the project folder is not cloned.


```bash
  git clone git@bitbucket.org:printerlogicDev/template-bdds-tests.git .
```

4.- Copy the url of the new repository created in step 1 and set as remote url for this project.


```bash
  git remote set-url origin git@bitbucket.org:printerlogicDev/<newproject>-bdds-tests.git
```

5.- Run this command to ensure the remote url is set correctly.


```bash
  git remote -v
```
    
6.- Run this command to install dependencies.


```bash
  npm run setup
```


## Running Tests

To run all tests locally, run the following command

```bash
  npm run local-test
```


## Environment Variables

To run this project, you will need to add the following environment variables to your .env file

`INSTANCE_URL`

`DEFAULT_USER`

`DEFAULT_PASSWORD`

`DEFAULT_DOMAIN`

`CHROME_HEADLESS`

`SELENIUM_REMOTE_URL`

`JIRA_SERVER`

`JIRA_PROJECT_ID`

`JIRA_API_KEY`

`RESULTS_FILE`


## Questions

If you have any question, please reach out to eduardo.guardado@vasion.com


## Tech Stack

**Client:** NodeJS, Cucumber, JavaScript, Selenium



## Feature/Examples

```javascript
Feature: Quota Management settings

      @settings
      Scenario: User click in settings button and sees the Settings modal and all expected elements
            Given a user log in to admin console and get the session id
            And quota management is set to custom time period
            And quota management is enable
            And user navigates to Quota Management
            And wait for element with locator "xpath" and locator value "//button[contains(text(),'Settings') and not(@disabled)]"
            And clicks in the element with locator "xpath" and locator value "//button[contains(text(),'Settings') and not(@disabled)]"
            Then the following elements are displayed
                  | Locator | Locator_Value                                        |
                  | xpath   | //span[contains(text(),'Quota Management Settings')] |
                  | id      | qm-settings-toggle-box                               |
                  | id      | unrestricted-printing-toggle-box                     |
                  | xpath   | //h6[contains(text(),'Manage Quota by')]             |
                  | xpath   | //span[contains(text(),'Recurring Time Period')]     |
                  | xpath   | //span[contains(text(),'Custom Time Period')]        |
                  | xpath   | //span[contains(text(),'Time zone:')]                |
```

