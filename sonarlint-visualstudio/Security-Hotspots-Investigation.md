> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/visual-studio/using-sonarlint/security-hotspots/**](https://docs.sonarsource.com/sonarlint/visual-studio/using-sonarlint/security-hotspots/)  
>
>The SonarLint documentation has moved! Please visit [https://docs.sonarsource.com/sonarlint/visual-studio/](https://docs.sonarsource.com/sonarlint/visual-studio/) to have a look at the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after October 1st, 2023* but no worries, we’ll keep them around a while for those running previous versions of SonarLint for Visual Studio.
>

# Overview

A security hotspot highlights a security-sensitive piece of code that the developer needs to review. Upon review, you'll either find there is no threat or you need to apply a fix to secure the code. For more information about Security Hotspots, take a look at the [SonarQube](https://docs.sonarsource.com/sonarqube/latest/user-guide/security-hotspots/) and [SonarCloud](https://docs.sonarcloud.io/digging-deeper/security-hotspots/) documentation.

## Local hotspot analysis

From SonarLint for Visual Studio version 7.1, it is possible to detect and report hotspots locally for C, C++, and JS/TS languages. Requirements include running SonarLint in Connected Mode and being bound to a project in SonarQube 9.7+ or to a project in SonarCloud. 

Note that security hotspots have been reported by SonarLint since version 4.29, but only when running in Connected Mode with SonarQube 8.9+. 

Improvements with v7.1 include the local detection of security hotspots and the option to report hotspots found by SonarCloud. When running in [Connected Mode](https://github.com/SonarSource/sonarlint-visualstudio/wiki/Connected-Mode) with SonarQube or SonarCloud, security hotspot analysis rules for the applicable languages will be run each time a local analysis is triggered.


### Newly detected Hotspots

Locally found hotspots will be highlighted in the editor using the charecteristic SonarLint squiggles. In addition, a list of all locally found hotspots will be found in the new Local Security Hotspots tool window, which will open and close automatically when there is a local hotspot to report. Selecting the rule key of your hotspot in the Local Security Hotspots tool window will open the [Sonar Rule Help](https://github.com/SonarSource/sonarlint-visualstudio/wiki#sonar-rule-help) window where you can review descriptive and educational content associated with the hotspot.


### Already known hotspots

Hotspots already detected by SonarQube/SonarCloud server are shown in the Sonar Local Security Hotspot tool window. Newly detected hotspots that are matched to already known hotspots marked as Fixed or Safe on the server, will not be shown. 

Note that previous behaviors of already known hotspots, such as SonarQube’s Open in IDE feature, remain unchanged; only the name of the tool window is updated in SonarLint v7.1.

## Open in IDE from SonarQube

From SonarLint for Visual Studio version 4.29, SonarLint provides a way to investigate [Security Hotspots](https://docs.sonarqube.org/latest/user-guide/security-hotspots/) found on your [SonarQube](https://www.sonarqube.org/) server. This is an integration feature: when viewing a hotspot on your SonarQube server, you will notice a button named **Open in IDE**; selecting that button while Visual Studio is running will open the hotspot's code file in the IDE. 

## Feature requirements

* SonarQube version 8.6 or higher.
* SonarLint version 4.29 or higher.
* The correct solution must be open in Visual Studio and it must be in [Connected Mode](https://github.com/SonarSource/sonarlint-visualstudio/wiki/Connected-Mode). SonarQube will not open Visual Studio if it is closed.

## Feature overview

When an “Open in IDE” request is received from the browser, SonarLint will verify that the correct solution is open in Connected Mode. If not, a gold bar will be displayed with additional information being logged in the Output Window:

[[images/Hotspots/SLVS_HostpotsGoldbar_v4_29.PNG|alt=Request gold bar]]
[[images/Hotspots/SLVS_HotspotsOutputWindowError_v4_29.PNG|alt=Request error details in the output window]]

If the correct solution is open and the hotpot's code location can be found in the solution, SonarLint will open the file and navigate to the relevant code. In addition, the hotspot will be added to a new tool window, `SonarLint Security Hotspots`, where you can see additional information:

[[images/Hotspots/SLVS_NavigableHotspot_v4_29.PNG|alt=Hotspot code in the IDE]]

However, it is possible that the code in your SonarQube server does not match your local code version, e.g. if code changes have been made since the last analysis or if the relevant code project is not included in the solution. In this case, SonarLint will not be able to locate the hotspot and it will be added to the list with an indication that it is not navigable:

[[images/Hotspots/SLVS_NotNavigableHotspot_v4_29.PNG|alt=Hotspot code cannot be found in the IDE]]

### Security Hotspots list functionality

Once a hotspot has been added to the list, you can navigate to it using a double-click or the Enter key.
In order to remove a hotspot from the list, use the right-click context menu or the Del key. This will only remove the hotspot from the list - it will not have any effect on the hotspot in your SonarQube server.

[[images/Hotspots/SLVS_RemoveHotspot_v4_29.PNG|alt=Remove a hotspot from the list]]

## Implementation notes

When Visual Studio starts, SonarLint will start listening in the background for “Open in IDE” requests originating from your local browser. This listener does not require a lot of resources and should not affect your machine's performance and memory consumption in any way, nor should it interfere with your work. 
SonarLint will try to find an available port in the range 64120-64130 inclusive. Information about the port selection will be logged in the SonarLint pane in the Output Window. If a port cannot be found then “Open in IDE” will not be handled. The port range is not configurable.

