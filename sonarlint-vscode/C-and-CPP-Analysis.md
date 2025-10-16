> ## ⓘ **Information**
>
>>**The content on this page has moved**: [**https://docs.sonarsource.com/sonarlint/vs-code/getting-started/running-an-analysis/#analyze-c-and-cpp-code**](https://docs.sonarsource.com/sonarlint/vs-code/getting-started/running-an-analysis/#analyze-c-and-cpp-code)  
>
>The SonarLint documentation has moved! Please visit [https://docs.sonarsource.com/sonarlint/vs-code/](https://docs.sonarsource.com/sonarlint/vs-code/) to have a look at the new documentation website. We’ve improved the documentation as a whole, integrated the four SonarLint IDE extension docs together, and moved everything under the sonarsource.com domain to share a home with the SonarQube docs (SonarCloud to come in Q3 of 2023).
>
>*These GitHub wikis will no longer be updated after September 1st, 2023* but no worries, we’ll keep them around a while for those running previous versions of SonarLint for VS Code.
>

# Prerequisite

To analyze C and C++ code, you need to:
1. [Generate a compilation database](#1)
2. [Be on one of the supported enviroments](#2)

<h2 id="1">
Generate a Compilation Database
</h2>

[Compilation Database](https://clang.llvm.org/docs/JSONCompilationDatabase.html) is a JSON file format introduced by the LLVM project.
It contains the compile commands used to build a project.

<details>
<summary>Generating Compilation Database Using the Build System</summary>
<p>

Many build systems support the automatic generation of compilation databases. For example:
* CMake by simply setting this option `CMAKE_EXPORT_COMPILE_COMMANDS`
* VS Code [Makefile Tools](https://devblogs.microsoft.com/cppblog/makefile-tools-december-2021-update-problem-matchers-and-compilation-database-generation/) extension
* Ninja by setting the `compdb` flag
* Xcode through Clang's `-gen-cdb-fragment-path` feature:
  ```
  # Add the following "OTHER_CFLAGS" option to the xcodebuild command
  xcodebuild clean build <additional args> OTHER_CFLAGS="\$(inherited) -gen-cdb-fragment-path \$(PROJECT_DIR)/CompilationDatabase"
  # After the build, aggregate the fragments into "compile_commands.json"
  cd CompilationDatabase && sed -e '1s/^/[\'$'\n''/' -e '$s/,$/\'$'\n'']/' *.json > ../compile_commands.json && cd ..
  ```
* Clang using the -MJ option. Note that this will generate a compilation database entry by input. The merge of all entries can be done through something like `sed -e '1s/^/[\'$'\n''/' -e '$s/,$/\'$'\n'']/' *.o.json > compile_commands.json`

When different choices are available, generating a compilation database through the build system should be preferred.

</p>
</details>

<details>
<summary>Generating Compilation Database Using Open Source Wrappers</summary>
<p>

Many open-source projects can help in generating a compilation database. For example:
*  [Bear](https://github.com/rizsotto/Bear)
*  [Bazel compile commands extractor](https://github.com/hedronvision/bazel-compile-commands-extractor)

</p>
</details>

<details>
<summary>Generating Compilation Database Using a Custom Script</summary>
<p>

A compilation database is just a JSON file that describes how to compile a project. If none of the previous approaches is feasible, for example, in the case of an internal build system, writing a script that generates a compilation database that describes how source files are supposed to be compiled can be the last resort.

</p>
</details>

<details>
<summary>Best Practices</summary>
<p>

* Make sure that the compilation database contains the actual compile commands. This can be checked by running the compilation commands inside the `compile_commands.json` and verifying that they succeed
* Make sure that the compilation database is up to date. It should be refreshed as part of the development cycle
* If the build system uses environment variables, make sure that they are set in the VS Code environment
* The compilation database should not contain header files entries. We use internal heuristics to analyze header files
</p>
</details>

<h2 id="2">
Supported Environments
</h2>

<details>
<summary>Supported Compilers</summary>
<p>

* Any version of Clang, GCC, and Microsoft C/C++ compilers
* Any version of Intel compiler for Linux and macOS
* ARM5 and ARM6 compilers
* IAR compilers for ARM, Atmel AVR32, Atmel AVR, Renesas H8, Renesas RL78, Renesas RX, Renesas V850, Texas Instruments MSP430, and 8051
* QNX compilers
* Texas Instruments compilers on Windows and macOS for ARM, C2000, C6000, C7000, MSP430, and PRU
* Wind River Diab and GCC compilers
* Compilers based wholly on GCC, including, for instance, Linaro GCC, are also supported
</p>
</details>

<details>
<summary>Supported Language Standards</summary>
<p>

* C standards: C89, C99, C11, C18
* C++ standards: C++03, C++11, C++14, C++17, and C++20 standards
* GNU extensions

</p>
</details>

<details>
<summary>Supported Runtime Environments</summary>
<p>

* Microsoft Windows on x86-64
* Linux on x86-64
* macOS with version 10.14.3 and later on x86-64

</p>
</details>

# Activating the Analysis

The analysis can be activated by simply pointing to a compilation database that describes the project to be analyzed. This can be done through a notification that pops up when a folder that contains a file named `compile_commands.json` is opened, or through the SonarLint embedded action that lists all compilation database files in the folder, or by manually assigning the `sonarlint.pathToCompileCommands` option in the settings to the full path of the compilation database.

Note that the SonarLint embedded action can be used to switch the active compilation database. 

# Troubleshooting

In case the analysis is not working or obvious false positives are raised, here are the recommended actions in order:

<details>
<summary>1. Investigate the Logs</summary>
<p>

First, enable SonarLint `Analyzer Logs` and look if there is any error or failures that indicate what went wrong.
If there is no obvious sign in the logs, enable `Verbose Logs` and check again.

</p>
</details>

<details>
<summary>2. Make Sure that the Compilation Database is Credible</summary>
<p>

* Make sure that the compilation database is up to date: It doesn't contain outdated commands or points to files that no longer exist.
* Make sure that the compilation database contains the actual compilation commands. This can be done by running the `commands` inside the `compile_commands.json` and verifying that they succeed.
* Make sure that the VS Code environment has the environment variables required to build the project

</p>
</details>

<details>
<summary>3. Enable the Rule `S2260`</summary>
<p>

In case of obvious false positives in the raised issues, Enable the `cpp:S2260`/`c:S2260` rule and check if it raises issues on the culprit file. 
This rule indicates that the analyzer failed to parse part of the code and might give hints or indicate a configuration problem. Follow the description of the rule if it raises issues. If not move to the step in troubleshooting.

</p>
</details>

<details>
<summary> 4. Generate the CFamily reproducer File and Report the Issue</summary>
<p>

When non of the previous suggestions help solve the issue, please report the faced problem on the [Sonar Community](https://community.sonarsource.com/) to help.

In case of a false positive or an analysis failure, we need the CFamily reproducer file to investigate the issue. To generate the reproducer file, add the following analyzer option to the `settings.json`:

` "sonarlint.analyzerProperties": {"sonar.cfamily.reproducer" : "C:\\replace\\by\\path\\to\\file.cpp"}`

`sonar.cfamily.reproducer` should point to the source or header file on which you face the issue. After setting that option, trigger the analysis on the culprit file. You should see in the logs that a file name `sonar-cfamily.reproducer` is generated in a temporary directory. Upload that file in your community report or ask us to share it privately if it contains sensitive information.

</p>
</details>