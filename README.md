# HTCondor Website

This git repository contains the source code for the (in-progress) refactored HTCondor website.  If you want to learn more about HTCondor, [visit the website itself](https://htcondor.org).

# Installation

### Installing Ruby & Jekyll
 
If this is your first time using Jekyll, please follow the [Jekyll docs](https://jekyllrb.com/docs/installation/) and make sure your local environment (including Ruby) is setup correctly.

### Using Docker for Development

Depending on your environment, it may be more useful to run Jekyll inside a container.  To do this, run the following from your laptop while inside the checked-out copy of the website source:

```
docker run -p 8000:8000 --rm --volume $PWD:/srv/jekyll -it jekyll/jekyll:latest /bin/sh
```

This will utilize the latest Jekyll version and map port `8000` to your host.  Within the container, a small HTTP server can be started with the following command:

```
jekyll serve --watch -H 0.0.0.0 -P 8000
```

This will build and serve the website; it can be viewed by navigating your web browser to <http://localhost:8000>.

With the `--watch` flag set, any changes you make to the website source will cause a new version of the website to be built; it usually takes 4-5 seconds between hitting "Save" and then "Refresh" on the website.

