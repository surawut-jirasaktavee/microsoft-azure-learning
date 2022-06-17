# Azure CLI
---

## Install Azure CLI on macOS

The Azure Command-Line Interface (CLI) allows the execution of commands through a terminal using
interactive command-line prompts or script. You can install the Azure CLI locally on macOS.

## Install with Homebrew

[**Homebrew**](https://brew.sh/) is the easiest way to manage you CLI install. It provides conveient
-ways to install, update, and uninstall. If you don't have `homebrew` available on your system,
[install homebrew](https://docs.brew.sh/Installation.html).

After install homebrew, You can install the Azure CLI on macOS by updating your brew repository 
information, and then running the install command.

````bash
brew update && brew install azure-cli
````

**IMPORTANT**
The Azure CLI has a dependency on the Homebrew `python@3.10` package, and will install it.

For **Troubleshooting** please see file an issue on github [here](https://github.com/Azure/azure-cli/issues)

## Unable to find Python or installed packages

There may be a minor version mismatch or other issue during homebrew installation. The CLI doesn't use a Python virtual environment, so it relies on finding the installed Python version
A possible fix is to install and relink the `python@3.10 dependency from homebrew.

````bash
brew update && brew install python@3.10 && brew upgrade python@3.10
brew link --overwrite python@3.10
````

## UpdateThe 

CLI is regularly updated with bug fixes, improvements, new features, and preview functionality. A new release is available roughly every three weeks.

The CLI provides an in-tool command to update to the latest version:

````Azure CLI
az upgrade
````

You can also update you local Homebrew repo and then upgrade the `azure-cli` package.

````Bash
brew update && brew upgrade azure-cli
````

## Uninstall

````Bash
brew uninstall azure-cli
````

## Remove data

````Bash
rm -rf ~/.azure
````


