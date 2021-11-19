# Ghidra Processor Specification - Quick(er) Start Guide #

## Introduction ##

This repo is meant to be used as a quick-start tutorial for specifying a new processor for [Ghidra](https://ghidra-sre.org/). Other tutorials are (in my opinion) lacking in detail, examples, screenshots, or just content in general. I will try to remedy some of this here.

## Source Material ##

In order write this guide, I referenced the following sources:

1. [Ghidra's website](https://ghidra-sre.org/)
   1. [Ghidra installation guide](https://htmlpreview.github.io/?https://github.com/NationalSecurityAgency/ghidra/blob/stable/GhidraDocs/InstallationGuide.html)
   2. [Ghidra's GitHub](https://github.com/NationalSecurityAgency/ghidra)
   3. [Ghidra's developer guide](https://github.com/NationalSecurityAgency/ghidra/blob/master/DevGuide.md)
2. [Ghidra documentation](https://ghidra.re/docs/)
   1. [Sleigh](https://ghidra.re/courses/languages/html/sleigh.html)
   2. [P-Code](https://ghidra.re/courses/languages/html/pcoderef.html)
3. Other Tutorials
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
2. Go to *Help->Install New Software...*

   ![eclipse - install new software](images/eclipse_install_new_software.png)

3. Select *Add...* then *Archive...*

   ![eclipse - add local archive](images/eclipse_add_local.png)

4. Navigate to `<GHIDRA_PATH>Extensions/Eclipse` where `<GHIDRA_PATH>` is the folder you unzipped Ghidra into. `<GHIDRA_PATH>` should look something like the following:

   ![ghidra folder content](images/ghidra_folder_content.png)

5. Install GhidraDev and Ghidra Sleigh Editor

   ![eclipse - install GhidraDev](images/eclipse_ghidradev.png)

   ![eclipse - install Ghidra Sleigh Editor](images/eclipse_ghidrasleigheditor.png)

6. Restart, enable open ports

   ![GhidraDev - open ports](images/eclipse_ghidradev_openports.png)

## Creating a Project ##

1. Go to *File->New->Project...*

   ![eclipse - new project](images/eclipse_newproject.png)

2. Select *Ghidra Module Project*

   ![eclipse - ghidra module project](images/eclipse_newproject_ghidra.png)

3. Keep all Ghidra options selected

   ![ghidra module options](images/eclipse_newproject_ghidraoptions.png)

4. Add you Ghidra install location to the plugin. This is the same `<GHIDRA_PATH>` mentioned elsewhere in this readme.

   ![ghidra install path](images/eclipse_newproject_ghidrainstall.png)

5. Let Eclipse finish creating the project