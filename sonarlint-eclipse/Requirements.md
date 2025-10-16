> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/eclipse/getting-started/requirements/**](https://docs.sonarsource.com/sonarlint/eclipse/getting-started/requirements/)
>
>The SonarLint documentation has a new home! Please visit [https://docs.sonarsource.com/sonarlint/eclipse/](https://docs.sonarsource.com/sonarlint/eclipse/) to check out the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after September 1st, 2023* but no worries, we’ll keep them around for a while for those running previous versions of SonarLint for Visual Studio.
>
>

# Overview

Here are the requirements for SonarLint to work properly.

* Eclipse Platform Requirement: the minimal version of the Eclipse platform that SonarLint supports. If you are not familiar with Eclipse versioning scheme, see [here](https://en.wikipedia.org/wiki/Eclipse_(software)#Releases).
* JVM requirement: the minimal version of the JVM that is used to [run Eclipse](https://wiki.eclipse.org/Eclipse.ini#Specifying_the_JVM).
* Node.js requirement: only for JavaScript analysis
* SonarQube minimal requirement: only if using connected mode. Usually means that the next LTS is also supported.

| SonarLint Version | Eclipse Platform Requirement | JVM Requirement | Node.js Requirement | SonarQube Min Requirement (for connected mode) |
| --- | --- | --- | --- | --- |
| 6.x | 4.6+ (Neon+) | 1.8+ | | 7.9+ |
| 7.x | 4.8+ (Photon+) | 11+ | | 7.9+ |
| 7.4 | 4.8+ (Photon+) | 11+ | 12.22+ | 7.9+ |
| 7.6+ | 4.8+ (Photon+) | 11+ | 14.20+ (16+ or 18+ recommended) | 7.9+ |

# Other requirements

* Analysis of Java code requires JDT
* Analysis of C and C++ requires CDT
* Analysis of Cobol requires specific integration provided only by some Cobol IDEs, like [IBM Developer for z Systems (IDz)](https://community.ibm.com/community/user/ibmz-and-linuxone/blogs/blog-entry1/2017/07/07/sonarlint-integration-with-developer-for-zsystems) or [BMC Compuware Topaz Workbench](https://devops.api.bmc.com/guidelines/ispw/ispw_projects.html#setting-up-usage-of-sonar-lint).

Please also note that recent versions of SonarLint and of our analyzers require a JRE 11+ in order to run, and IBM IDz only supports JRE 11 starting from [version 16](https://www.ibm.com/common/ssi/ShowDoc.wss?docURL=/common/ssi/rep_ca/2/899/ENUSLP22-0372/index.html).
