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


## Let's Get Reckless!

How to get reckless? Reckless-python is contained in a single python executable. Copy `reckless` into your /usr/local/bin directory.  This should be done automatically if installed with Core-Lightning.

Running the first time will prompt the user that their lightningd's bitcoin config will be appended (or created) to inherit the reckless config file (this config is specific to bitcoin by default.) Management of plugins will subsequently modify this file.

Start with a simple installation such as `reckless install sumary`


## Troubleshooting tips

Plugins must be executable. For python plugins, the shebang is invoked, so `python3` should be available in your environment. This can be verified with `which Python3`. The default reckless directory is /home/<user>/.lightning/reckless and it should be possible for the lightningd user to execute files located here.  If this is a problem, the option flag `reckless -d=<my_alternate_dir>` may be used to relocate the reckless directory from its default. Consider creating a permanent alias in this case.


## For Developers

Tips for making your plugin compatible with reckless install:
- Choose a unique plugin name.
- The plugin entrypoint is inferred.  Naming your plugin executable the same as your plugin name will allow reckless to identify it correctly (file extensions are okay.)
- For python plugins, a requirements.txt is the preferred medium for python dependencies. A pyproject.toml will be used as a fallback, but test installation via `pip install -e .` - Poetry looks for additional files in the working directory, whereas with pip, any references to these will require something like `packages = [{ include = "*.py" }]` under the `[tool.poetry]` section.
- Additional repository sources may be added with `reckless source add https://my.repo.url/here` however, https://github.com/lightningd/plugins is included by default. Consider adding your plugin lightningd/plugins to make installation simpler.
- If your plugin is located in a subdirectory of your repo with a different name than your plugin, it will likely be overlooked.


## To Do

Reckless is a work in progress. Right now it handles the basics of installing, validating, and activating python plugins. Recommened future work may include:
- Option flag(s) for non-bitcoin network (regtest, signet, etc.)
- Support for non-python plugins.
- Install by specifying url/dir directly.
- Possibly support installing a virtual environments for python plugins.

