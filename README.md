# uBlue Website

This is the MkDocs repository that hosts the website for [ublue.it](https://ublue.it).

## Developing

You will need [Python version 3.10 or higher](https://www.python.org/downloads/) and [Poetry](https://python-poetry.org/docs/).

1. Setup project dependencies `poetry install`
2. Run the local development server `poetry run mkdocs serve`
3. Open a browser to [localhost:8000](http://localhost:8000). This will auto-reload on file changes

## Contributing

1. Create a [fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) of this repository
2. Create a new branch for your contribution `git checkout -b my-new-branch`
3. Add your contributions! Make changes, use `poetry run mkdocs serve` to validate those changes
4. Commit and push your changes to your branch
5. Open [a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) to have it reviewed

## Editing the Image list

Edit `.github/ublue-scan.yml` to add images to the ignore list.
Use this for images that you don't want to be shown on ublue.it/images. 
Typically we only want to show user-facing images on the site. 
