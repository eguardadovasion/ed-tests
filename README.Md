
# Template for BDDs Automation Repository

🤖 Welcome to the BDDs Automation Repository template! This template is designed to help you create a new module for the Node.js framework that can be used to test a new feature.


## Table of Contents

- [Project Structure](#project-structure)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [Running Tests](#running-tests)
- [Tests Results](#test-results)
- [Questions](#questions)
- [Tech Stacks](#tech-stacks)
- [Features Examples](#examples)

## 🛠️ Project Structure {#project-structure}

```sh

├── .vscode
│   └── steps.code-snippets
├── features/
│   ├── template.feature
├── pl-api-bdd-steps/
│   ├── submodule content
├── pl-saas-web-bdd-steps/
│   ├── submodule content
├── report/
│   ├── cucumber_report.json
│── .env
│── .gitignore
│── .gitmodules
│── .npmrc
│── .package.json

```




 `.vscode/`: This folder contains code snippets for feature files, which are used in the Visual Studio Code (VS Code) integrated development environment (IDE) to suggest autocompletion for feature steps.

 `features/`: This folder will contains the feature files for the feature that is being tested. The feature files define the behavior and requirements for a specific feature. Each project have their own feature files. For example: https://github.com/PrinterLogic/qm-ui-bdd-tests/tree/master/features 

 `pl-api-bdd-steps/`: This folder is a submodule that contains functions and methods used to perform actions against the Printerlogic APIs. These steps are written in a Behavior-Driven Development (BDD) style and are used in conjunction with the feature files to test the functionality of the APIs.

 `pl-saas-web-bdd-steps/`: This folder is also a submodule that contains functions and methods used to interact with a website, specifically Printerlogic's self-service portal and admin console. These steps are also written in a BDD style and are used in conjunction with the feature files to test the functionality of the website.

 `report/`: This folder is where the test results are stored by default. The test results include information about the status of the tests, any errors or failures that occurred, screenshots and any other relevant information.

 `.env`: This file is used to configure the environment variables required to run this project. Environment variables are used to store sensitive information such as passwords and API keys.

 `.gitignore`: This file lists the files and folders that should not be pushed to GitHub. These files are typically temporary or generated files that are not necessary for the project to function.

 `.gitmodules`: This file contains the configuration of the URLs for the submodules used in this project.

 `.npmrc`: This file is used to register global and internal npm registries to use when installing dependencies for this project.

 `package.json`: This file contains scripts that are used to set up the environment, run tests, and publish the test results. It also lists the dependencies required for the project to function.


## 🛠️ Installation {#installation}

Follow these steps to get started with your new repository:

1.- Create a new repository in Github under PrinterLogic organization https://github.com/PrinterLogic and using following naming convention:

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
  git clone git@github.com:PrinterLogic/template-bdd-tests.git .
```

4.- Copy the url of the new repository created in step 1 and set as remote url for this project.


```bash

  git remote set-url origin git@github.com:PrinterLogic/<project_name>-bdd-tests.git

```

5.- Run this command to ensure the remote url is set correctly.


```bash
  git remote -v
```
    
6.- Before setting up the environment, make sure you are connected to the VPN. 

Once you are connected to the VPN, run the following command to install dependencies:

- Dependencies will be installed from 3 sources: Github submodules, npm global registry and npm vasion registry ( https://verdaccio.pl-labs.com/ )


```bash
  npm run setup
```




## 🌐 Environment Variables {#environment-variables}

To run this project, you will need to add the following environment variables to your .env file

### Instance configuration

`INSTANCE_URL`: The URL of the instance to be tested. For example: https://edtesting.gw.service.pl-labs.com/. If you want to run in parallel against multiple instances you can add up to 6 instances comma separated. For example: https://edtesting.gw.service.pl-labs.com/, https://auto.gw.service.pl-labs.com/, https://auto2.gw.service.pl-labs.com/, https://auto4.gw.service.pl-labs.com/, https://auto5.gw.service.pl-labs.com/, https://qmnew.gw.service.pl-labs.com/, https://qm-ed.gw.service.pl-labs.com/, https://newqm.gw.service.pl-labs.com/

`DEFAULT_USER`: The username of the default user to be used for testing. For example: root.

`DEFAULT_PASSWORD`: The password of the default user to be used for testing. For example: password1.

### Selenium server configuration

`CHROME_HEADLESS`: Set this variable to true to run tests in headless mode, or false to run in normal mode. For example: true. 
#### WARNING: CHROME_HEADLESS is not currently functional. Uncomment the following line to run without headless mode.
#### CHROME_HEADLESS=false


`SELENIUM_REMOTE_URL`: The URL of the Selenium server to be used for remote testing. For example: http://localhost:4444/wd/hub.

### Jira Assert that plug in

`JIRA_SERVER`:The URL of the JIRA server to be used for logging test results. For example: https://jira.printerlogic.com.

`JIRA_PROJECT_ID`: The ID of the JIRA project to be used for logging bugs. For example: 10600.

`JIRA_API_KEY`: The API key to be used for accessing the JIRA server. For example: myjiraapikey.

`DEFAULT_DOMAIN`: The name of the exection to display in Jira results. For example: IDP-VERSION-2.

`RESULTS_FILE`: The name of the file where the test results are stored locally. For example: "report/cucumber_report.json". These are the results that will be send to Jira and only json files are supported.


Here's an example .env file:

```
INSTANCE_URL=https://edtesting.gw.service.pl-labs.com/
DEFAULT_USER=root
DEFAULT_PASSWORD=password1
CHROME_HEADLESS=true
SELENIUM_REMOTE_URL=http://ec2qa-selenium5.printerlogic.local:4444/wd/hub
JIRA_SERVER=https://jira.printerlogic.com
JIRA_PROJECT_ID=10600
JIRA_API_KEY=<jirauser:password@base64encode>
RESULTS_FILE="report/cucumber_report.json"
DEFAULT_DOMAIN=API-GW:1.270.2,QM-UI:1.1.323,QMS:1.0.162
```


## 🏃 Running Tests {#running-tests}

To run all tests locally, run the following command

```bash
  npm run local-test
```

There are two scripts available to run tests: 

- `npm run local-test`: This command runs tests without parallel execution and is primarily intended for testing a specific script locally. By adding the tag of a specific scenario to the command, only that script can be executed. For instance, "npm run local-test -- -t @debugTest".

- `npm run test`: This command runs tests in parallel execution using six processors by default. To use this command, six instances need to be added to the INSTANCE_URL env variable. By default, this command does not use the "@skip" tag. It is mainly used by Github Actions workflows as part of the Continuous Integration and Continuous Deployment (CI/CD) process.

## Test Results {#test-results}

Once you execute the tests if you want to send the results to Jira run the following command:

```bash
  npm run publishResults
```

This will upload the results to Jira at following link: https://jira.printerlogic.com/projects/PI?selectedItem=com.assertthat:assertthat-project-report-overview&projectId=10600 with the name given in DEFAULT_DOMAIN env variable.

## ❓ Questions {#questions}

If you have any question, please reach out to eduardo.guardado@vasion.com


## 🛡️ Tech Stack {#tech-stacks}

**Client:** NodeJS, Cucumber, JavaScript, Selenium



## 📚 Feature/Examples {#examples)}

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

