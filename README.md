# Universal Blue Website

This is the MkDocs repository that hosts the website for [Universal Blue](https://universal-blue.org).

## Developing

You will need [Python version 3.10 or higher](https://www.python.org/downloads/) and [Poetry](https://python-poetry.org/docs/).

1. Setup project dependencies `poetry install`
2. Run the local development server `poetry run mkdocs serve`
3. Open a browser to `localhost:8000`. This will auto-reload on file changes

If you have access to mkdocs-material-insiders, run the following to install it:

```sh
poetry run pip install git+ssh://git@github.com/squidfunk/mkdocs-material-insiders.git@29bd630bf94c3a3c0eef8118cf1289c226252636
```

Then use

```sh
poetry run mkdocs serve -f mkdocs.insiders.yml
```

## Contributing

1. Create a [fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) of this repository
2. Create a new branch for your contribution `git checkout -b my-new-branch`
3. Add your contributions! Make changes, use `poetry run mkdocs serve` to validate those changes
4. Commit and push your changes to your branch
5. Open [a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) to have it reviewed

## Editing the Image list

Edit `.github/ublue-scan.yml` to add images to the ignore list.
Use this for images that you don't want to be shown on [ublue.it/images](https://ublue.it/images/). 
Typically we only want to show user-facing images on the site. 

## [![Repography logo](https://images.repography.com/logo.svg)](https://repography.com) / Recent activity [![Time period](https://images.repography.com/35181738/ublue-os/website/recent-activity/SdqIfcQSR-z77fWYqUAaMF4VLejiPo7SjYuESFGqH1w/JQCzzJexnEhmDyF4qC8VF6W5CVe79qKT2EkOcS4F2Is_badge.svg)](https://repography.com)
[![Timeline graph](https://images.repography.com/35181738/ublue-os/website/recent-activity/SdqIfcQSR-z77fWYqUAaMF4VLejiPo7SjYuESFGqH1w/JQCzzJexnEhmDyF4qC8VF6W5CVe79qKT2EkOcS4F2Is_timeline.svg)](https://github.com/ublue-os/website/commits)
[![Issue status graph](https://images.repography.com/35181738/ublue-os/website/recent-activity/SdqIfcQSR-z77fWYqUAaMF4VLejiPo7SjYuESFGqH1w/JQCzzJexnEhmDyF4qC8VF6W5CVe79qKT2EkOcS4F2Is_issues.svg)](https://github.com/ublue-os/website/issues)
[![Pull request status graph](https://images.repography.com/35181738/ublue-os/website/recent-activity/SdqIfcQSR-z77fWYqUAaMF4VLejiPo7SjYuESFGqH1w/JQCzzJexnEhmDyF4qC8VF6W5CVe79qKT2EkOcS4F2Is_prs.svg)](https://github.com/ublue-os/website/pulls)
[![Activity map](https://images.repography.com/35181738/ublue-os/website/recent-activity/SdqIfcQSR-z77fWYqUAaMF4VLejiPo7SjYuESFGqH1w/JQCzzJexnEhmDyF4qC8VF6W5CVe79qKT2EkOcS4F2Is_map.svg)](https://github.com/ublue-os/website/commits)

## [![Repography logo](https://images.repography.com/logo.svg)](https://repography.com) / Top contributors
[![Top contributors](https://images.repography.com/35181738/ublue-os/website/top-contributors/SdqIfcQSR-z77fWYqUAaMF4VLejiPo7SjYuESFGqH1w/JQCzzJexnEhmDyF4qC8VF6W5CVe79qKT2EkOcS4F2Is_table.svg)](https://github.com/ublue-os/website/graphs/contributors)
