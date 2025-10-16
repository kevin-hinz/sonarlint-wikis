> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/intellij/using-sonarlint/taint-vulnerabilities/**](https://docs.sonarsource.com/sonarlint/intellij/using-sonarlint/taint-vulnerabilities/) 
>
>The SonarLint documentation has a new home! Please visit [https://docs.sonarsource.com/sonarlint/intellij/](https://docs.sonarsource.com/sonarlint/intellij/) to check out the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after September 1st, 2023* but no worries, we’ll keep them around a while for those running previous versions of SonarLint for IntelliJ.
>

# Overview

Taint vulnerabilities are a type of [security-related rules](https://docs.sonarqube.org/latest/user-guide/security-rules/), that can be raised by both SonarCloud and SonarQube (starting with Developer Edition).

Due to technical limitations, SonarLint for IntelliJ can not raise such issues on local analysis.
Nevertheless, it is possible for a project to display within the IDE vulnerabilities detected by SonarCloud/SonarQube.

# Prerequisites

* You need to bind to SonarCloud or SonarQube Developer Edition (or higher) 8.6+
* For this feature to be valuable, your project needs to be analyzed frequently (ideally by your CI server when pushing new code)
* Only issues detected on the current branch will be displayed in the IDE
* Only issues detected on open files will be displayed in the IDE

# How to display taint vulnerabilities in IntelliJ

1. [[Bind your project to SonarQube/SonarCloud|Bind to SonarQube or SonarCloud]]
2. Open the SonarLint tool window and select the _Taint Vulnerabilities_ tab
3. The tab should display the list of taint vulnerabilities that are present on open files.