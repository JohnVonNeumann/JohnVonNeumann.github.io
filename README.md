# My personal website

## Using the repository

Uses `pipenv` to handle the dependencies, which are located in `Pipfile` and `Pipfile.lock`.

### Activating the pipenv

Pelican is packaged inside the pipenv, so use:

        pipenv shell

After this, you will be able to issue the normal `Pelican` commands:

        pelican content

After generating content, you can serve a localhost on port 8000 with:

        pelican --listen
