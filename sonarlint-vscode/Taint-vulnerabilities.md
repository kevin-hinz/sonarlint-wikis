> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/vs-code/using-sonarlint/taint-vulnerabilities/**](https://docs.sonarsource.com/sonarlint/vs-code/using-sonarlint/taint-vulnerabilities/)  
>
>The SonarLint documentation has moved! Please visit [https://docs.sonarsource.com/sonarlint/vs-code/](https://docs.sonarsource.com/sonarlint/vs-code/) to have a look at the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after September 1st, 2023* but no worries, we’ll keep them around a while for those running previous versions of SonarLint for VS Code.
>

# Overview

Taint vulnerabilities are a type of [security-related rules](https://docs.sonarqube.org/latest/user-guide/security-rules/), that can be raised by both SonarCloud and SonarQube (starting with Developer Edition).

Due to technical limitations, SonarLint can not raise taint issues on local analysis. Because SonarLint must pull taint vulnerability issues from SonarQube or SonarCloud following a project analysis, the use of Connected Mode is required.

## Prerequisites

- You must bind your project to an instance of SonarQube Developer Edition (or higher) 8.9+ or to SonarCloud.

- For this feature to be valuable, your project needs to be analyzed frequently (ideally by your CI server when pushing new code).

## How to display taint vulnerabilities in VS Code

1. Bind your project to SonarQube/SonarCloud.
1. In the standard VS Code Panel below the editor region, select the **PROBLEMS** tab.
1. Along with regular issues, the **PROBLEMS** tab should display the list of taint vulnerabilities that are present in the bound folder. SonarLint displays taint vulnerabilities for the entire project.

## How to fix your taint issues

Because detection of taint vulnerabilities requires that you are running in Connected Mode, any changes you make to the code must be resolved by your SonarQube or SonarCloud instance.  Here are two options to resolve taint issues displayed by SonarLint:

- If you fix the issue locally, commit your code to the server and rerun the analysis on SonarQube or SonarCloud. The new status (of the issue) will show up automatically in your local analysis.

- If you go to the issue in SonarQube or SonarCloud and mark it as _safe_ or _won’t fix_, in less than 1 minute, the new status will be updated locally.