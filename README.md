# powershell-docset : A dash docset for powershell modules

Based on [lucasg](https://github.com/lucasg)'s [powershell-docset](https://github.com/lucasg/powershell-docset).

Added support for running on GitHub actions and local dependency installation via `poetry`.

Updated the default Powershell documentation version to 7.2.

### Status

[![Build Status](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Factions-badge.atrox.dev%2Ftddschn%2Fpowershell-docset%2Fbadge%3Fref%3Dmaster&style=flat)](https://actions-badge.atrox.dev/tddschn/powershell-docset/goto?ref=master)
<!-- [![Build Status](https://travis-ci.org/lucasg/powershell-docset.svg?branch=master)](https://travis-ci.org/lucasg/powershell-docset) -->

`posh-to-dash.py` scrapes the newly announced `https://docs.microsoft.com/en-us/powershell/module/` website in order to create an offline dash-compatible archive to be viewed in `Dash`, `Zeal` or `Velocity` :

<p align="center">
<img alt="Powershell docset in Velocity" src="screenshots/posh-docset.PNG"/>
</p>

## Releases

<!-- - [v0.1 -- Minimal working version](https://github.com/lucasg/powershell-docset/releases/tag/v0.1)
- [v0.2 -- Offline mode supported](https://github.com/lucasg/powershell-docset/releases/tag/v0.2)
- [v0.3 -- travis setup](https://github.com/lucasg/powershell-docset/releases/tag/v0.3)
- [v0.4 -- user contributed docset](https://github.com/lucasg/powershell-docset/releases/tag/v0.4)
- [v0.5 -- versioned docsets](https://github.com/lucasg/powershell-docset/releases/tag/v0.5)
- [v0.6 -- windows 10 modules documentation](https://github.com/lucasg/powershell-docset/releases/tag/v0.6) -->
<!-- - [v0.7.2 -- powershell 7.1 documentation](https://github.com/lucasg/powershell-docset/releases/tag/v0.7.2) -->
- [v7.2.5 -- powershell 7.2.5 documentation](https://github.com/tddschn/powershell-docset/releases/tag/v7.2.5)

## Running on GitHub Actions

The [Scrape Powershell doc and build docset](https://github.com/tddschn/powershell-docset/actions/workflows/scrape-and-build.yaml) action crawls the powershell 7.2 documentation, builds the docset, and uploads the built artifact.

Modify the doc version in [posh-to-dash.py](./posh-to-dash.py) to scrape another version of the powershell documentation.
## Local Installation & Execution

`posh-to-dash.py` relies on :

- `requests` for http(s) downloads
- `selenium` and `phantomjs` for webscraping
- `bs4` for html parsing and rewriting

1. Clone the repository
2. Install the dependencies from requirements.txt, use a virtualenv to avoid problems with dependencies and versions. Alternatively if you use `poetry`, run `poetry install`.
3. Download the geckodriver from [Mozilla's Repo](https://github.com/mozilla/geckodriver/releases), download the version that matches your OS.
4. Place the geckodriver in your path

- If Windows, grab the executable an place it in `%USERPROFILE%\AppData\Local\Microsoft\WindowsApps`

- If Linux, move it to your `~/.local/bin` or wherever you have your path

5. Start scraping by typing : `posh-to-dash.py --output=$outputfile --version=6 --temporary`

- if `--output` is not provided, `posh-to-dash.py` will output "Powershell.tgz' into the working directory
- the `--version` switch support only Powershell API versions `5.1`, `7.2` (default) and `7.3` , the rest are obsolete by Microsoft.
- `--temporary` specify to download the web scraping resources in a temporary folder instead of clobbering the current directory. However if the download fail, the results will be thrown out.

**NOTE: The process takes 15+ minutes to run. The more versions you download increases the time.**

## Add your docset to Zeal

With the Powershell.tar file, unzip it and place it in `C:\Users\<your-username>\AppData\Local\Zeal\Zeal\docsets`

## Limitations

The powershell modules API endpoint is quite new, so it may be subject to breakage by the `docs.microsoft.com` people.
