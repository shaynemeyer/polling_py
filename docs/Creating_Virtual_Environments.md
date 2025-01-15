# Creating Virtual Environments
I use venv because I've used it for many years and have not found anything better. Feel free to use whatever you like but these docs will follow how I set things up. I also work on Macs and Linux so for Windows instructions you will need to do a little research.

## Create a virtual environment

```shell
python3 -m venv .venv
```

---
## Activate the virtual environment

```shell
source .venv/bin/activate
```

---
## Verify the virtual environment

```shell
which python3
```

You should see something like this: `/Users/<user>/<path_to_app>/.venv/bin/python3`

I've also included a `.python-version` file and set the python version to `3.10`

