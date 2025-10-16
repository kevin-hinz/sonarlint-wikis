> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/eclipse/team-features/connected-mode/**](https://docs.sonarsource.com/sonarlint/eclipse/team-features/connected-mode/)
>
>The SonarLint documentation has a new home! Please visit [https://docs.sonarsource.com/sonarlint/eclipse/](https://docs.sonarsource.com/sonarlint/eclipse/) to check out the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after September 1st, 2023* but no worries, we’ll keep them around for a while for those running previous versions of SonarLint for Visual Studio.
>
>

# Overview

You can connect SonarLint to SonarQube 7.9+ or SonarCloud to aim at having consistent issues reported on both sides. Setting up Connected Mode will permit the transmission of information SonarLint needs, such as URLs and user credentials, to communicate with SonarQube or SonarCloud.

Features when connected mode is used:
* use the same analyzers than the server, assuming they are supported in SonarLint (except for JS/TS and HTML analyzers where SonarLint keep using its embedded version)
* use the same quality profile (same rules activation, parameters, severity, ...)
* reuse some settings defined on the server (rule exclusions, analyzer parameters, ...)
* automatically suppress issues that are marked as _Won’t Fix_ or _False Positive_ on the server

**Note**: Connected Mode does not push issues to the server. Rather, its purpose is to configure the IDE so that it uses the same settings as the server.

# Configure a connection

A connection is the set of informations needed to communicate with the SonarQube server or SonarCloud (URL, credentials, ...).

## Connection setup

1. From SonarLint for Eclipse 7.8+, it is possible to open the Sonar connection wizard using one of these two methods to set up Connected Mode:

   1. Go to **File** > **New** > **Other…** to open Eclipse’s **Select a wizard** menu. Then, find **SonarLint** > **New SonarQube/SonarCloud Connection** and select **Next**.

   2. Right-click in the **SonarLint Bindings** tasks view tab and select **New Connection…**. This method will start the wizard right away.

[[images/connected/file_new_connection.png|alt=New Connection]]

2. Choose either SonarCloud or SonarQube, then select the **Next** button to continue:

[[images/connected/wizard_select_sonarqube.png|alt=Select SonarQube]]

3. For SonarQube, Enter your SonarQube server URL:

[[images/connected/wizard_set_url.png|alt=Set URL]]

4. 4. Choose the authentication method:

   - Token: generate a user token on [SonarQube](https://docs.sonarqube.org/latest/user-guide/user-token/), to be used by SonarLint as an authentication method. This is the preferred way to avoid the risk of compromising your username/password. Note that a _user token_ is the only token type that works with Connected Mode.

   - Username + Password: use directly your SonarQube credentials (not recommended)

[[images/connected/wizard_choose_auth.png|alt=Choose auth]]

5. Enter your SonarQube token or username/password. Then continue with step 6 below.

6. Give your connection a name

## Configure a connection to SonarCloud

4. Generate a token on [SonarCloud](https://docs.sonarcloud.io/advanced-setup/user-accounts/#user-tokens), to be used by SonarLint as the authentication method. The connection wizard will provide this link: [https://sonarcloud.io/account/security](https://sonarcloud.io/account/security), as a shortcut.

5. Select your organization; a filtered list will appear as you start typing.

6. Name your Connection.

7. Then, choose if you want to receive Notifications. See the [SonarQube](https://docs.sonarqube.org/latest/user-guide/sonarlint-connected-mode/#smart-notifications) and [SonarCloud](https://docs.sonarcloud.io/advanced-setup/sonarlint-smart-notifications/) documentation for details about what information is in a notification.

8. And select **Finish** to complete the Connection wizard, before moving on to the binding wizard.

Once set up, SonarLint will check your SonarQube or SonarCloud organization’s project list against open or newly opened projects in your workspace to suggest a binding. 
[[images/connected/binding-detection.png|alt=Binding Suggestion]]

# Configure project binding

If you just created a new connection, the _Connection wizard_ will transition into a _Binding wizard_ where you can add projects that you want to bind. Or, you can select your SQ or SC server in the **SonarLint Bindings** tab, right-click, and select **Bind Projects…** to open the wizard, then **Add…** to open the **Project selection** window.

1. The **Project selection** window presents a list of projects open in the Eclipse workspace. 

2. In the next window, start typing the name of a project you have on the server; double-click on the matching project and the wizard will grab and load the Project Key.3. Click **Finish** and check the progress bar in the lower right corner.


## View configured connections

Connections and their bindings can be retrieved from the **SonarLint Bindings** view tab which is found by navigating to the **File Menu** > **Window** > **Show View** > **Other...** > **SonarLint** > **SonarLint Bindings**:

Right-clicking on a connection will open a tooltip to edit or delete the connection and can be useful for example to update credentials and bindings if they have changed.

[[images/connected/binding-configurations.png|alt=Bindings View]]

Right-clicking on a connection will reveal an option to select **Update All Project Bindings**.

# Notifications while in Connected Mode

When you are using Connected Mode and connected to the server, you can be notified in your IDE with smart notifications as soon as something appears on the server that something failed, or when the Sonar Quality Profile is updated, for example. The notification will include a link to call back to SonarQube or SonarCloud where you can learn more about the issues that were introduced. Sonar Smart Notifications are available in all editions of SonarQube and SonarCloud.

Activation and Deactivation of Sonar Smart Notifications occurs in the IDE during the binding process. To change your notification settings, go to the **SonarLint Bindings** view, right-click the connection you want to change, and select **Edit Connections…**.
