> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/eclipse/**](https://docs.sonarsource.com/sonarlint/eclipse/)
>
>The SonarLint documentation has a new home! Please visit [https://docs.sonarsource.com/sonarlint/eclipse/](https://docs.sonarsource.com/sonarlint/eclipse/) to check out the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after September 1st, 2023* but no worries, we’ll keep them around for a while for those running previous versions of SonarLint for Visual Studio.
>
>

# SonarLint for Eclipse

SonarLint is an IDE extension that helps you detect and fix quality issues as you write code. Like a spell checker, SonarLint squiggles flaws so they can be fixed before committing code. You can get it directly from the [Eclipse Marketplace](https://marketplace.eclipse.org/content/sonarlint) and it will then detect new bugs and quality issues as you code.


## Supported languages

Out of the box, SonarLint for Eclipse automatically checks against the following rules:
- [C rules](https://rules.sonarsource.com/c)
- [HTML rules](https://rules.sonarsource.com/html)
- [Java rules](https://rules.sonarsource.com/java) (requires a Java development tool (JDT))
- [JavaScript rules](https://rules.sonarsource.com/javascript)
- [PHP](https://rules.sonarsource.com/php)
- [Python rules](https://rules.sonarsource.com/python)
- [TypeScript rules](https://rules.sonarsource.com/typescript)
- [XML](https://rules.sonarsource.com/xml)
- [Secrets detection rules](https://rules.sonarsource.com/secrets)

When using [Connected Mode](Connected-Mode) with [SonarQube](https://www.sonarqube.org/) or [SonarCloud](https://sonarcloud.io/), you can unlock these rules:
- [ABAP rules](https://rules.sonarsource.com/abap)
- [Apex rules](https://rules.sonarsource.com/apex)
- [C++ rules](https://rules.sonarsource.com/cpp)
- [COBOL rules](https://rules.sonarsource.com/cobol) (requires a COBOL IDE based on the Eclipse platform)
- [Kotlin](https://rules.sonarsource.com/kotlin)
- [PL/I rules](https://rules.sonarsource.com/pli)
- [PL/SQL rules](https://rules.sonarsource.com/plsql)
- [RPG rules rules](https://rules.sonarsource.com/rpg)
- [Ruby rules](https://rules.sonarsource.com/ruby)
- [Scala rules](https://rules.sonarsource.com/scala)
- [T-SQL rules](https://rules.sonarsource.com/tsql)

The full list of available rules is visible in the **Rules Configuration** preferences tab found by navigating the UI to **Window** > **Preferences** > **SonarLint** (or **Eclipse** > **Settings…** > **SonarLint** for Mac OS) for access to **Rules Configuration**. Here you can activate and deactivate rules to match your conventions. SonarLint will also show a code action on each issue to quickly deactivate the corresponding rule.

For more details about languages and new features under consideration for all SonarLint IDEs (including Eclipse), please refer to the [SonarLint roadmap](https://portal.productboard.com/sonarsource/4-sonarlint/tabs/8-under-consideration) where we list our *coming soon* and *newly released* features.

SonarLint is also available for [Visual Studio](https://github.com/SonarSource/sonarlint-visualstudio/wiki), [VS Code](https://github.com/SonarSource/sonarlint-vscode/wiki), [IntelliJ](https://github.com/SonarSource/sonarlint-intellij/wiki) (the languages supported vary from IDE to IDE).