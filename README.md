# About

![NeverRed icon](/img/NeverRed.png)

**NeverRed** is a PowerShell-based solution for automatically downloading, installing, and updating the latest versions of commonly used enterprise Windows applications.

It was designed primarily for **EUC (End-User Computing) environments**, where simply installing the latest application version is often not enough. Enterprise environments typically require additional configuration, specific installation parameters, or modifications to prevent applications from updating themselves.

NeverRed handles many of these tasks automatically, including:

* Disabling automatic application updates, for example for Adobe Acrobat Reader, Microsoft Edge, and Google Chrome.
* Using the appropriate installers and installation parameters, such as machine-based installations of Microsoft OneDrive, Slack, or Microsoft Teams.
* Applying application-specific customizations after installation, including registry modifications and configuration changes for products such as Microsoft FSLogix and Microsoft Teams.
* Determining current application versions and download URLs even when vendors do not provide a straightforward download source, such as Cisco Webex.

This is exactly the problem NeverRed was created to solve.

Instead of manually checking vendor websites, comparing versions, downloading installers, and applying the required enterprise configuration, NeverRed automates the process.

Key functionality includes:

* Detecting the currently installed application version.
* Determining the latest available version from the Internet.
* Automatically downloading the latest installer.
* Downloading current ADMX templates for supported applications where applicable.
* Uninstalling an existing version when required.
* Installing the latest version using the appropriate enterprise installation parameters.
* Configuring scheduled tasks and services to prevent unwanted automatic updates.
* Applying application- and operating-system-specific modifications after installation.
* Handling known application or operating-system issues, such as creating the required Scheduled Task on Windows Server 2019 and later when installing Microsoft FSLogix to address the **Event ID 2 / Windows Search (WSearch)** issue.

## How NeverRed Works

NeverRed uses several methods to determine the latest available application version and its corresponding download URL.

Depending on the application, NeverRed uses established PowerShell modules or its own application-specific detection logic.

The primary sources and methods include:

1. [Evergreen PowerShell Module by Aaron Parker](https://github.com/aaronparker/evergreen)
2. [Nevergreen PowerShell Module by Dan Gough](https://github.com/DanGough/Nevergreen)
3. [Custom web scraping and application detection functions by Manuel Winkel](https://www.deyda.net)

This combination allows NeverRed to support applications regardless of whether vendors provide a clean API, a static download URL, or only a dynamically generated download page.

## Why NeverRed?

There are already excellent community and commercial products available for application deployment, packaging, and update management. NeverRed is **not intended to compete with or replace these solutions**.

Its goal is different: to provide a simple and lightweight way to keep standard applications in Windows and EUC environments up to date **without having to package every application or manually search vendor websites and compare versions**.

NeverRed is particularly useful for administrators maintaining:

* Citrix Virtual Apps and Desktops environments
* Azure Virtual Desktop environments
* Windows 365 environments
* Golden or master images
* Other standardized Windows and EUC deployments

## Documentation

Documentation for NeverRed, including configuration information and usage examples, is available here:

[NeverRed Documentation](https://www.deyda.net/index.php/en/neverred/)

## Versioning

NeverRed uses an enumerated versioning scheme.

Because the script is regularly updated to accommodate new application versions, changed vendor download mechanisms, and additional functionality, the version number makes it easy to determine whether the installed copy of NeverRed is current.

Detailed information about changes between versions is available in the:

[NeverRed Changelog](https://www.deyda.net/index.php/en/neverred-changelog/)

When NeverRed is started on a system with Internet access, it automatically checks whether a newer version of the script is available.

When running interactively, the user is notified and can choose whether to update NeverRed.

When NeverRed is executed unattended using an existing configuration file, script updates can be performed automatically.

## Installing NeverRed

### PowerShell Support

NeverRed supports:

* **Windows PowerShell 5.1**
* **PowerShell 7.0 and later**

NeverRed should also work with PowerShell Core 6.x. However, this version is no longer actively tested, so compatibility cannot be guaranteed.

### Download from GitHub

NeverRed is published on GitHub and can be downloaded from:

[NeverRed on GitHub](https://github.com/Deyda/NeverRed/)

Downloading NeverRed directly from the GitHub repository is the **recommended method** for obtaining the latest version.

### Starting NeverRed

After downloading NeverRed, the script can be started from an **elevated PowerShell session**.

#### Interactive GUI Mode

```powershell
.\NeverRed.ps1
```

#### Unattended Mode

To run NeverRed unattended using a previously saved configuration:

```powershell
.\NeverRed.ps1 -ESFile LastSetting.txt
```

#### Third-Party Integration

NeverRed can also be integrated into third-party image-management or automation solutions such as **BIS-F**.

For example, adapt the `StartNeverRed.ps1` script to reference the appropriate NeverRed installation path and configuration file. The customized script can then be stored and executed as a **Custom Script** within BIS-F.

### Updating NeverRed

When a previous version of NeverRed is started in **GUI mode**, the script checks whether a newer version is available. If an update is found, the user is prompted to install it.

When NeverRed is executed using the `-ESFile` or `-GUIFile` parameters, available NeverRed updates are applied automatically.
```
