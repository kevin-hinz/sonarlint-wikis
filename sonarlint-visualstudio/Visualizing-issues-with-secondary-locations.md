> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/visual-studio/using-sonarlint/investigating-issues/#issues-with-secondary-locations**](https://docs.sonarsource.com/sonarlint/visual-studio/using-sonarlint/investigating-issues/#issues-with-secondary-locations)  
>
>The SonarLint documentation has moved! Please visit [https://docs.sonarsource.com/sonarlint/visual-studio/](https://docs.sonarsource.com/sonarlint/visual-studio/) to have a look at the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after October 1st, 2023* but no worries, we’ll keep them around a while for those running previous versions of SonarLint for Visual Studio.
>

## Feature requirements
* SonarLint version 4.26 or higher.

Supported languages for in-IDE analysis: C, C++, JavaScript, TypeScript

Supported languages for [Hotspots](https://github.com/SonarSource/sonarlint-visualstudio/wiki/Security-Hotspots-Investigation) and [Taint Vulnerabilities](https://github.com/SonarSource/sonarlint-visualstudio/wiki/Security-Taint-Vulnerabilities-Investigation): C, C++, C#, VB.NET

## Feature Overview
All SonarLint issues specify a location in the code showing where the issue occurs. However, some of the more complex rules produce issues for which a single location is not enough to adequately explain why the issue has occurred. These more complex rules often identify additional locations in the code to help understand the problem. These additional locations are referred to as secondary locations.

For some rules (i.e. [cpp:S3529](https://rules.sonarsource.com/cpp/RSPEC-3529)) the secondary locations identify a ‘flow’ through the code that leads to the issue. For other rules (i.e. [cpp:S1871](https://rules.sonarsource.com/cpp/RSPEC-1871)), the secondary locations indicate other locations that are related to the issue.

SonarLint for Visual Studio shows these secondary locations in the editor and in a separate tool window.

### SonarLint Issue Visualization tool window

[[images/SecondaryLocations/SecondaryLoc_toolwindow_v4_26.png|alt=SonarLint Issue Visualization tool window screenshot]]

By default, the tool window will only be visible in the following cases:
* When a Taint Vulnerability is selected in the [Taint list](https://github.com/SonarSource/sonarlint-visualstudio/wiki/Security-Taint-Vulnerabilities-Investigation).
* When a Hotspot containing secondary locations is selected in the [Hotspots list](https://github.com/SonarSource/sonarlint-visualstudio/wiki/Security-Hotspots-Investigation).
* When an issue with secondary locations is selected in the Error List i.e. the window will automatically appear and disappear as the Error List selection changes.
* When lightbulb suggested action "SonarLint: Show Issue Visualization" is invoked. The suggested action will appear when hovering over an issue with secondary locations in the Editor as shown in the following screenshot:

[[images/SecondaryLocations/SecondaryLoc_lightbulb.png|alt=Issue Visualization lightbulb screenshot]]

#### Manually re-opening SonarLint Issue Visualization tool window

If you manually close the tool window it will no longer appear and disappear automatically. You can show the window again using one of three menu commands:
* The menu command `Extensions → Sonar Lint → Show Issue Visualization`, which is always visible
* The lightbulb suggested action "SonarLint: Show Issue Visualization" when hovering over an issue in the Editor (see screenshot above)
* The Show SonarLint Issue Visualization command on the Error List context menu, which is available for issues with secondary locations as shown in the following screenshot:

[[images/SecondaryLocations/SecondaryLoc_errorlist_contextmenu.png|alt=Issue Visualization Error List context menu screenshot]]


### Navigating between secondary locations
Selecting a secondary location in the tool window will move the edit cursor to the specified location in the code.

It is also possible to navigate between secondary locations using the keyboard with the following shortcuts:
* Go to next location: Ctrl+Shift+Alt+Q, Ctrl+Shift+Alt+Right Arrow
* Go to next location: Ctrl+Shift+Alt+Q, Ctrl+Shift+Alt+Left Arrow

These shortcut key combinations were chosen to avoid conflicts with existing Visual Studio shortcuts and shortcuts in popular third-party extensions. As always, it is possible to customize these shortcuts in Visual Studio. See the MS documentation for more information.

#### Non-navigable locations
It is not always possible to navigate to a location in the code e.g. because the code has been changed since the file was analyzed, or the source file has been deleted. The tool window will show which locations are non-navigable:

[[images/SecondaryLocations/SecondaryLoc_nonnavigable_location_v4_26.png|alt=Non-navigable location shown the the tool window screenshot]]


### Known issues

* [Issues list](https://github.com/SonarSource/sonarlint-visualstudio/issues?q=is%3Aopen+is%3Aissue+label%3A%22Area%3A+Secondary+Locations%22)

* Issue Visualization panel no longer appears and disappears automatically: the panel was likely closed manually and therefore needs to be re-open manually (see “Manually re-opening SonarLint Issue Visualization tool window” section for more information).

