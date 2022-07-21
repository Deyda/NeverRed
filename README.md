# About


![Evergreen icon](/img/NeverRed.png)

NeverRed is a simple PowerShell script to download and install the latest version for several common enterprise Windows applications. The script consists a number of simple functions to use in EUC environments like:

* Disabling the auto update of the software (e.g. Adobe Reader, Microsoft Edge, Google Chrome, etc.)
* Right installers or parameters during installation (e.g. machine-based install for Microsoft OneDrive, Slack or Microsoft Teams)
* Add customizations after installation (e.g. reg hacks or customizations to files at Microsoft FSLogix or Microsoft Teams)
* Search for current versions on obscure pages (e.g. Cisco Webex)

Exactly this is where I wanted to remedy with NeverRed.

* No more searching for the current version on the confusing manufacturer pages.
* Comparison of the installed version, with the current one from the Internet
* Automatic download of the current version (and for some software, even the current ADMX files)
* Uninstalling (if necessary) the software and installing (with the correct parameters) the current new version
* Adjustment of the scheduled tasks and services, so that no automatic updates can interfere with them
* Adaptation of the new software to the specifics of the operating system (e.g. addition of the Scheduled Task for Windows Server 2019 and newer when installing Microsoft FSLogix for the “Event ID 2 wsearch” bug)

## How NeverRed Works

NeverRed uses several approaches to automatically get the version number and download URL for the applications.

Various strategies and PowerShell modules are used for this purpose:

1. [Evergreen PowerShell Module by Aaron Parker](https://github.com/aaronparker/evergreen)
2. [Nevergreen PowerShell Module by Dan Gough](https://github.com/DanGough/Nevergreen)
3. [Custom web scraping functions by Manuel Winkel](https://www.deyda.net)

## Why

There are community and commercial products that manage application deployment and updates already. This script isn't intended to compete against those.

NeverRed's focus is on a simple solution to keep standard software up to date without having to package it or search and compare versions on vendor sites.

## Documentation

Documentation for NeverRed, including usage examples, is located here: [Documentation](https://www.deyda.net/index.php/en/neverred/).

## Versioning

The script uses an enumerated version notation. It can be assumed that the script undergoes changes on a regular basis. The version numbering is therefore intended to make it as easy as possible to track whether you are using the current version. See the [Changelog](https://www.deyda.net/index.php/en/neverred-changelog/) for details of each change.

The script automatically detects if it is up to date when started on a system with internet, and if it is not, an automatic update is offered.

## "Installing the Script"

### PowerShell Support

NeverRed supports Windows PowerShell 5.1 and PowerShell 7.0+. NeverRed should work on PowerShell Core 6.x; however, I'm not actively testing on that version of PowerShell, so support cannot be guaranteed.

### Download from GitHub

The NeverRed script is published to GitHub and can be found here: [NeverRed](https://github.com/Deyda/NeverRed/). This is the best and recommend method to get NeverRed.

### Start the script

The script can be started directly after download in an administrative PowerShell window.

#### GUI Method

```administrative powershell
.\NeverRed.ps1
```
#### Unattended Method

```administrative powershell
.\NeverRed.ps1 -ESFile LastSetting.txt
```
#### Third-Party Method (e.g. BIS-F)

Adaptation of the StartNeverRed.ps1 script to the correct path and the required configuration file. Store the customized script, for example, in BIS-F under Custom Scripts.

### Updating the Script

If you have start a previous version of the script in GUI Mode, you get a message that an update is available and whether it should be executed.
With the parameter -ESFile and -GUIFile the update is performed automatically.
