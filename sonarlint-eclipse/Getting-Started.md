> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/eclipse/getting-started/installation/**](https://docs.sonarsource.com/sonarlint/eclipse/getting-started/installation/)
>>
>> The following sections (found below) now have dedicated pages:
>> - [Running an analysis](https://docs.sonarsource.com/sonarlint/eclipse/getting-started/running-an-analysis/)
>> - [Investigating issues](https://docs.sonarsource.com/sonarlint/eclipse/using-sonarlint/investigating-issues/)
>> - [Fixing Issues](https://docs.sonarsource.com/sonarlint/eclipse/using-sonarlint/fixing-issues/)
>
>The SonarLint documentation has a new home! Please visit [https://docs.sonarsource.com/sonarlint/eclipse/](https://docs.sonarsource.com/sonarlint/eclipse/) to check out the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after September 1st, 2023* but no worries, we’ll keep them around for a while for those running previous versions of SonarLint for Visual Studio.
>
>

## Quick Installation

SonarLint for Eclipse is a plugin that can be installed in most Eclipse based IDEs (including Spring Tool Suite, PyDev, ...)

1.  In your Eclipse based IDE, open the Marketplace client

[[images/install/open_marketplace_client.png|alt=Open Marketplace Client]]

2. Search for SonarLint, and click _Install_

[[images/install/marketplace_install.png|alt=Install from Marketplace]]

3. Restart your IDE

For more installation methods, look for the advanced [installation](Installation) documentation.

## First taste of SonarLint

Now that you have SonarLint installed, open or create a new project containing source files in a programming language SonarLint can analyze out of the box: Java, PHP, Python, JavaScript or HTML.

For example in Java, you can copy paste this code snippet, with a typical bug when copy/pasting `for` loops:

```java
package org.mycompany;

import java.util.logging.Level;
import java.util.logging.Logger;

public class Main {

  private static final Logger LOGGER = Logger.getLogger(Main.class.getName());

  public static void main(String[] args) {
    for (int left = 0; left < 10; left++) {
      for (int right = 0; right < 10; left++) {
        LOGGER.log(Level.INFO, "Pair: ({0},{1})", new Object[] {left, right});
      }
    }
  }

}
```

If you open this Java file within the Eclipse Java editor, you should see SonarLint reporting the issue:

[[images/analysis/first_time_analysis.png|alt=First time analysis]]

To get more details about the issue, you can simply hover on the issue location, and a popup will display the issue message:

[[images/analysis/sonarlint_java_problem_hover.png|alt=Hover]]

There is also the possibility to use the SonarLint `On-The-Fly` view to display the list of issues found by SonarLint. Simply open the view from the menu Windows -> Show View -> Other...

[[images/views/open_on_the_fly_view.png|alt=Open On-The-Fly view]]
There is also the possibility to use the SonarLint `On-The-Fly` view to display the list of issues found by SonarLint. Simply open the view from the menu Windows -> Show View -> Other...

[[images/views/open_on_the_fly_view.png|alt=Open On-The-Fly view]]
[[images/views/on_the_fly_view.png|alt=On-The-Fly view]]

# Running an analysis

By default, new analyses are automatically triggered on opening a file, and with each save following a change in the code. Automatic analysis can be controlled on a per-project basis: Right-click on a project in the **Project** or **Package Explorer**, open **Properties** > **SonarLint** to select/deselect **Run SonarLint automatically**.

Here are all the ways to trigger a SonarLint analysis in Eclipse:

- **Detect issues on file open and save** (default): When the file is opened, autosaved or manually saved.
- **On-demand**: Selections of one or more files can be analyzed together by right-clicking over a file selection in the Eclipse **Project Explorer**, then select **SonarLint** > **Analyze**.
- **Analyze changed files**: Right-click over a Project folder in the Project/Package Explorer and select **SonarLint** > **Analyze changed files** to run an analysis on all uncommitted files. Your project must be under Git source control and you must have Egit installed. **
- **By selection**: Use this method to get feedback on issues found in _a set of files_ or _set of projects_. Select one or more files/projects in the Project Explorer, then right-click > **SonarLint** > **Analyze with SonarLint**. The **SonarLint Report** view will open automatically and present issues found in your selection. Note that you can also select **Analyze All Project Files** from the **Report** tab, without having to select _all project files_ from the Project Explorer.**

There’s a status bar in the lower right corner to report the state of analysis. Issues found after an analysis of the active file are displayed in the SonarLint view window in the **SonarLint On-The-Fly** tab; note that you can also select multiple files in the Eclipse **Project/Package Explorer** and see them in the **SonarLint On-The-Fly** tab. Issues found after the analysis of multiple files are displayed in the **SonarLint Report** tab. See the documentation about \[Investigating issues]() for more details.

## JavaScript and TypeScript analysis

To perform CSS, JavaScript, or TypeScript analysis, SonarLint must find the file path to your Node.js. If you have troubles, go to **Eclipse** > **Settings** to open the **Preferences** menu, then find **SonarLint** and set your **Node.js executable path**.

## File Exclusions

It’s possible to limit the analysis using this same navigation path (as above). In Windows, go to **Project** > **Properties** > **SonarLint** and select **File Exclusions** (in Mac: **Eclipse** > **Settings** > **SonarLint** > **File Exclusions**). There you can specify files to exclude.

**NOTE**: A custom change to the configuration such as initializing Connected Mode or when modifying your selected rule set, will trigger a new analysis because it could lead to different results. In addition, when binding a project to SonarQube or SonarCloud, a new analysis will be triggered for all open files. See the documentation on [Connected Mode](Connected-Mode) for more details.

# Investigating issues

The **SonarLint Rule Descriptions** view is usually your first step into identifying why you have
an issue. Right-clicking on any issue in a SonarLint view, or exposing the tooltip and selecting
**Open description of rule …** in the code editor will open the **SonarLint Rule Scriptions** view.

The Rule Descriptions includes information about why this causes an issue and noncompliant /
compliant code snippets are usually offered. More serious issues such as security hotspots and
taint vulnerabilities often include information about why it’s an issue and what is the potential
impact.

[[images/views/Rule-Descriptions.png|alt=Rule-Descriptions]]

SonarLint for Eclipse supports syntax highlighting; it’s availability is dependent on the Eclipse
version and plugins you have installed (e.g. [JDT](https://www.eclipse.org/jdt/) is required for
Java syntax highlighting). Currently Java and C / C++ are available.

[[images/views/Rule-Descriptions-2.png|alt=Rule-Descriptions-2]]

Syntax highlighting is not available for languages accessed with external plugins, but an extension
point is provided to plugin developers.

# Fixing Issues
Depending on the nature of your issue, SonarLint for Eclipse offers different fixes. Issues are usually presented in multiple locations and you can typically hover and/or click or right-click over these markers to open a tooltip that reveals your options. Check the \[Investigating issues]() page for more details about how to identify issues in the IDE.

## SonarLint Preferences menu

Navigate to **Window** > **Preferences** > **SonarLint** (or **Eclipse** > **Settings…** > **SonarLInt** for Mac OS) for access to the **SonarLint Preferences** menu. Here you will find 4 menus to:

- Pass additional properties to the SonarLint analyzers.
- Add/remove files to be excluded from the analysis.
- Agree/disagree to share anonymous telemetry statistics.
- And specifically define your rules configuration (when running in stand-alone mode).

### **Rule selection**

Sonar Rules can individually be turned on or off while running SonarLint in standalone mode; there are two ways to do this:

- Right-click on the issue and select the **Remove** rule quick fix in the tooltip.
- Activate and deactivate rules one by one in the **SonarLint Preferences** > **SonarLint** > **Rules Configuration** menu. A full list of rules organized by language is available.

When your project is bound to SonarQube or SonarCloud using [Connected Mode](Connected-Mode), the rule set is managed on the server side as defined by the quality profile. See the [SonarQube](https://docs.sonarqube.org/latest/instance-administration/quality-profiles/) and [SonarCloud](https://docs.sonarcloud.io/standards/managing-quality-profiles/) documentation about quality profiles for more information.

## Quick fixes

Eclipse relies on the language support from the IDE to display quick fixes in different ways. Hovering over the issue in your code editor will reveal the SonarLint tooltip. Sonar Quick Fix options such as _Deactivate rule_ or _Insert placeholder comment_ will be shown when available. Depending on the language type and/or issue type, an action item such as _Show issue data flows_ or _Remove unused local variable_ will be offered. In addition, right-clicking an issue in the **SonarLint On-The-Fly** view will also reveal Quick Fix options.

[[images/getting-started/quick-fixes.png|alt=SonarLint quick-fixes]]

You will always be offered the option in the tooltip and in all SonarLint view panels to open the issue’s rule in the **SonarLint Rule Description** view; the rule description explains why the issue is raised and details how to fix it. 

Sometimes your issue is recognized by additional analyzers. When this occurs, a full list of _all_ quick fixes will appear in the tooltip; SonarLint’s Quick Fixes are distinguishable by the SonarLint icon preceding the text title. 

## Fixing security hotspots and taint vulnerabilities

The use of [Connected Mode](Connected-Mode) is required to identify both security hotspots and taint vulnerabilities. Security hotspots require that your project be bound to SonarQube; Taint vulnerabilities can be found with a Connected Mode binding to either SonarQube or SonarCloud.

By default, a SonarLint hotspot badge and vulnerability padlock are displayed for _Security Hotspot_ and _Taint Vulnerability_ issues (respectively) in the Eclipse **Vertical ruler**. 

If you don’t see the data flow displayed in the code editor for taint issues, make sure that _code minings_ are enabled in the **Preferences > Java > Editor** > **Code Minings** menu.

Please have a look at the SonarLint documentation on [Security hotspots](Security-Hotspots) and [Taint vulnerabilities](Taint-Vulnerabilities) for more details about working with each issue type in SonarLint.

## Deactivating issues

Marking issues as _Safe_ or _Won’t fix_ can only be done in the SonarQube or SonarCloud which will be recognized locally when running in Connected Mode. To ignore a specific issue without deactivating the rule, submit your code to trigger a new analysis in SonarQube where you can mark it as Fixed or Safe on the server; then update your project binding to see the changes locally.