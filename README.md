# gumtree-scraper

A simple scraper for gumtree Australia

![animation](docs/sample.gif)

## Features

- prettier list of offers (when compared with Gumtree's)
- ability to hide or star particular offer
	- starred offer can't be hidden until it's unstarred
- global seen mark to indicate which offers were already clicked
- offers are only *added*; when something gets removed from Gumtree, it's still
  here
- it's *your* database, and you can do whatever you want with it
- autorefresh for both backend and frontend
- fancy "Hide all" button to get rid of all visible entries when you're done
  (except for starred - those stay no matter what)

## Tech stuff

### Requirements

- Python 3.5 (for running everything)
- npm (for compiling frontend assets)

### Notable libraries used

- Flask
- React
- Redux
- [TinyDB](http://tinydb.readthedocs.org/) (not threadsafe)

### Installation

Pretty straightforward. virtualenv or pyenv (or both) are recommended.

```
pip install -r requirements.txt
npm install
./node_modules/webpack/bin/webpack.js -d
```

### Running

No daemonization yet - meaning you need 2 shells to run these:

```
python scrap.py
python server.py
```

### Architecture

#### Scraper

Resides in `scrap.py`. Crawls over 1st page of Gumtree results and stores them
in DB. Rinses and repeats every 5 minutes. Note: you need to provide URL for
Gumtree results page after running it (as each category has different URL;
that means you may also use filters, because they get appended to URL).

#### Server (Flask)

You can find it in `server.py`. Static page used to bootstrap React and
a couple of endpoints for manipulating entries.

#### Client (React)

Main entry point is in `js/index.jsx` - that's also where application's store
is defined. I followed split between presentation and container components,
which are (respectively) in `js/components.jsx` and `js/containers.jsx`.

## OK, looks great... but why?

Clicking through all offers with their pagination was tiring. Moreover, I think
their interface is not the most readable one I've ever seen; besides, I like to
see *all* opportunities, and most of the offers are added to their site either
1) when I'm at work, or 2) late in the evening. So I could have had a late
start when applying for an apartment - and believe me, the best offers are
grabbed in matter of hours, if not *minutes*.

## License

See [LICENSE.md](LICENSE.md).
