# reckless-python

A Core-Lightning plugin manager

## Features

Love Core-Lightning? Want to install and test a CLN plugin with only three words and a command line? Reckless has you covered!

- Install a plugin from the lightningd/plugins repository
- Add additional source repos to search/install
- Automatically install dependencies and verify installation
- Dynamically enable/disable reckless-managed plugins
- Persists plugin state by managing a config file inherited by lightningd

## Commands

`reckless install <plugin>` searches available repositories, if one matches, clones it, installs dependencies, and tests that the plugin executes and exits normally.  If so, the plugin is permanently installed, added to the CLN config, and dynamically activated.

`reckless uninstall <plugin>` disables the plugin, removes the directory.

`reckless search <plugin>` looks through all available sources for a plugin matching this name.

`reckless enable <plugin>`/`reckless disable <plugin>` dynamically enables/disables the reckless-installed plugin and updates the config to match.

`reckless source list` list all plugin repositories.

`reckless source add <repo url>` add another plugin repo for reckless to search or install from.

## To Do

Reckless is a work in progress. Right now it handles the basics of installing, validating, and activating python plugins. Recommened future work may include:
- option flag for non-bitcoin network (regtest, signet, etc.)
- Support for non-python plugins
- Installation to a virtual environment for each plugin
