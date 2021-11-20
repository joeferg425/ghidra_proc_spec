# Ghidra Processor Specification - Quick(er) Start Guide #

## Table of Contents ##

- [Ghidra Processor Specification - Quick(er) Start Guide](#ghidra-processor-specification---quicker-start-guide)
  - [Introduction](#introduction)
  - [Source Material](#source-material)
  - [First Steps](#first-steps)
  - [Install Software](#install-software)
  - [Install Eclipse Plugins](#install-eclipse-plugins)
  - [Creating a Project](#creating-a-project)

## Introduction ##

This repo is meant to be used as a quick-start tutorial for specifying a new processor for [Ghidra](https://ghidra-sre.org/). Other tutorials are (in my opinion) lacking in detail, examples, screenshots, or just content in general. I will try to remedy some of this here.

## Source Material ##

In order write this guide, I referenced the following sources:

### [Ghidra's website](https://ghidra-sre.org/) ###

  1. [Ghidra installation guide](https://htmlpreview.github.io/?https://github.com/NationalSecurityAgency/ghidra/blob/stable/GhidraDocs/InstallationGuide.html)
  2. [Ghidra's GitHub](https://github.com/NationalSecurityAgency/ghidra)
  3. [Ghidra's developer guide](https://github.com/NationalSecurityAgency/ghidra/blob/master/DevGuide.md)

### [Ghidra documentation](https://ghidra.re/docs/) ###

  1. [Sleigh](https://ghidra.re/courses/languages/html/sleigh.html)
  2. [P-Code](https://ghidra.re/courses/languages/html/pcoderef.html)

### Other Tutorials ###

  1. [ghidra.re](https://ghidra.re/online-courses/)
  2. [spinsel.dev](https://spinsel.dev/2020/06/17/ghidra-brainfuck-processor-1.html)
  3. [swarm.ptsecurity.com](https://swarm.ptsecurity.com/creating-a-ghidra-processor-module-in-sleigh-using-v8-bytecode-as-an-example/)

## First Steps ##

### Install Software ###

1. Install a Ghidra-compatible [Java](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html) version
2. Install [Ghidra](https://ghidra-sre.org/InstallationGuide.html)
3. Install [Eclipse](https://www.eclipse.org/downloads/)

### Install Eclipse Plugins ###

1. Launch Eclipse
2. Go to *Help->Install New Software...* \
  ![eclipse - install new software](images/eclipse_install_new_software.png)

3. Select *Add...* then *Archive...* \
  ![eclipse - add local archive](images/eclipse_add_local.png)

4. Navigate to `<GHIDRA_PATH>Extensions/Eclipse` where `<GHIDRA_PATH>` is the folder you unzipped Ghidra into. `<GHIDRA_PATH>` should look something like the following: \
  ![ghidra folder content](images/ghidra_folder_content.png)

5. Install GhidraDev and Ghidra Sleigh Editor \
  ![eclipse - install GhidraDev](images/eclipse_ghidradev.png) \
  ![eclipse - install Ghidra Sleigh Editor](images/eclipse_ghidrasleigheditor.png)

6. Restart, enable open ports \
  ![GhidraDev - open ports](images/eclipse_ghidradev_openports.png)

## Creating a GhidraDev Project ##

1. Go to *File->New->Project...* \
  ![eclipse - new project](images/eclipse_newproject.png)

2. Select *Ghidra Module Project* \
  ![eclipse - ghidra module project](images/eclipse_newproject_ghidra.png)

3. Keep all Ghidra options selected \
  ![ghidra module options](images/eclipse_newproject_ghidraoptions.png)

4. Add you Ghidra install location to the plugin. This is the same `<GHIDRA_PATH>` mentioned elsewhere in this readme. \
  ![ghidra install path](images/eclipse_newproject_ghidrainstall.png)

5. Let Eclipse finish creating the project

## GhidraDev Project Tour ##

### Default Package Content ##

- A new project should have the following folder structure

  ![ghidradev package content](images/ghidradev_packageexplorer.png)

### Debugging ###

- Clicking the bug or using the debugging keyboard shortcut will let you run ghidra in debug mode and enable breakpoints. Just select your project for debugging and if you have pointed the GhidraDev plugin at your Ghidra folder it should launch Ghidra for you.

  ![ghidradev debugging](images/ghidradev_debugging.png)

### Primary Plugin classes ###

&nbsp;&nbsp;&nbsp;&nbsp; ![ghidradev plugin classes](images/ghidradev_mainjava.png)

- `Analyzer` determines if/when your new code will run, then defines the main functionality.
- `Exporter` allows for exporting content from the binary
- `FileSystem` lets you define custom file system interaction
- `Loader` is where you define custom memory blocks and peripheral modules
- `Plugin` is where you define the plugin name and description and link up the other classes


### Script folder ###

&nbsp;&nbsp;&nbsp;&nbsp; ![ghidradev script location](images/ghidradev_relatedscripts.png)

- You can add scripts to your plugin

  - Scripts are accessible through the script manager window in the code browser in Ghidra \
  ![ghidra script manager window](images/ghidra_scriptmanager.png)

### Data/Languages Folder ###

&nbsp;&nbsp;&nbsp;&nbsp; ![ghidradev data/languages](images/ghidradev_languages.png)

- `cspec` is the compiler specification. It lets you define default aspects of your processor your compiler will use.
- `ldefs` is the initial language definition. It enables Ghidra to load your language specification.
- `opinion` lets you specify optional logic for sub-processor families and behaviors.
- `pspec` is the definition for default register values and specific register names for common processor functions (such as the program counter and stack pointer).
- `sinc` is the 'header' file for sleigh language specification.
- `slaspec` is the main specification file for the processor. This is where the memory, registers, opcodes, and opcode functionality are all defined (functionality can be split/moved into the 'sinc' file).
- `Building` you can build the processor specification by right-clicking the `BuildLanguage.xml` file and running 'Ant Build' \
  ![ghidradev ant build](images/ghidradev_antbuild.png)
  - This will provide you with error messages and line numbers while writing your processor specification
    - Successful build \
    ![ghidradev successful ant build](images/ghidradev_antbuild_success.png)
    - Failed build \
    ![ghidradev failed ant build](images/ghidradev_antbuild_fail.png)