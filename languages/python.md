# Python

### Editing Python in Zed

When editing Python, Zed provides code intelligence using the [Pyright](https://github.com/microsoft/pyright) language server.

#### Virtual environments

A python [virtual environment](https://docs.python.org/3/tutorial/venv.html) allows you to store all of a project's dependencies, including the Python interpreter and package manager, in a single directory that's isolated from any other Python projects on your computer.

By default, the Pyright language server will look for Python packages in the default global locations. But you can also configure Pyright to use the packages installed in a given virtual environment.

To do this, create a JSON file called `pyrightconfig.json` at the root of your project. This file must include two keys:

* `venvPath`: a relative path from your project directory to any directory that _contains_ one or more virtual environment directories
* `venv`: the name of a virtual environment directory

For example, a common approach is to create a virtual environment directory called `.venv` at the root of your project directory with the following commands:

```bash
# create a virtual environment in the .venv directory
python3 -m venv .venv
# set up the current shell to use that virtual environment
source .venv/bin/activate
```

Having done that, you would create a `pyrightconfig.json` with the following content:

```json
{
  "venvPath": ".",
  "venv": ".venv"
}
```

For more information, see the Pyright [configuration documentation](https://github.com/microsoft/pyright/blob/main/docs/configuration.md).

#### Code formatting

The Pyright language server does not provide code formatting. If you want to automatically reformat your Python code when saving, you'll need to specify an _external_code formatter in your settings. See the [configuration](../configuration/configuring-zed.md) documentation for more information.

A common tool for formatting python code is [Black](https://black.readthedocs.io/en/stable/). If you have Black installed globally, you can use it to format Python files by adding the following to your `settings.json`:

```json
{
  "language_overrides": {
    "Python": {
      "format_on_save": {
        "external": {
          "command": "black",
          "arguments": ["-"]
        }
      }
    }
  }
}
```

#### Troubleshooting

The Pyright language server is built in TypeScript and requires Node.js and npm to run. Therefore, ensure you have Node.js and npm globally accessible in case IntelliSense is missing your Python files or Zed logs report as the following.
```
Language server error: Python

failed to run npm info

Caused by:
    No such file or directory (os error 2)
```
