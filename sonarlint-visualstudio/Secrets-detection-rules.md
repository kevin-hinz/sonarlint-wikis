> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/visual-studio/using-sonarlint/rules/#secrets-detection**](https://docs.sonarsource.com/sonarlint/visual-studio/using-sonarlint/rules/#secrets-detection)  
>
>The SonarLint documentation has moved! Please visit [https://docs.sonarsource.com/sonarlint/visual-studio/](https://docs.sonarsource.com/sonarlint/visual-studio/) to have a look at the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after October 1st, 2023* but no worries, we’ll keep them around a while for those running previous versions of SonarLint for Visual Studio.
>

## Secrets detection

Starting with [v6.4](https://github.com/SonarSource/sonarlint-visualstudio/releases/tag/v6.4.0.47562), SonarLint for Visual Studio will detect and report hard-coded cloud secrets as issues.

[[images/Secrets/slvs_secrets_errorlist_v6_4.png|alt=Error list showing detected secrets]]

All types of text files are analysed, irrespective of the type of content (code, configuration, documentation etc). 
Analysis is triggered whenever a text file is opened or saved. 

Documentation for individual rules can be found on the [Rules website](https://rules.sonarsource.com/secrets).

### IDE-only
Secrets detection rules are only run in the IDE.

They do not appear in SonarQube/SonarCloud i.e. they can only be configured locally, and the secrets detection rules will not be run by the various Sonar scanners.


### Configuration
The rules can be enabled and disabled locally. It is not currently possible to suppress individual issues.
See the [rules configuration page](https://github.com/SonarSource/sonarlint-visualstudio/wiki/Choosing-which-C,-Cpp,-JavaScript,-TypeScript-or-Secrets-detection-rules-to-run-in-Standalone-mode) for more information.






