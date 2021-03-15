# HTCondor Website

This git repository contains the source code for the refactored HTCondor website.If you want to learn more about HTCondor, [visit the website itself](https://htcondor.org).


# Installation

## Installing Ruby & Jekyll
 
If this is your first time using Jekyll, please follow the [Jekyll docs](https://jekyllrb.com/docs/installation/) and make sure your local environment (including Ruby) is setup correctly.

Many versions of Linux do not have repository support for the required versions of ruby and gem. For this reason, we encourage using our Docker container to build and deploy the Jekyll website.

## Obtaining Docker image

Grab the **htcondor-web** image from our Docker Hub:
```
docker pull dockerreg.chtc.wisc.edu:443/htcondor/web
```

## Setting up a GitHub SSH key

To deploy changes to the live site, you'll need to set up a GitHub SSH key as described here: https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent


# Development

After making changes to the source files, use the Docker image to preview your changes. Run the following from your computer while inside the checked-out copy of the website source:

```
docker run -p 8000:8000 --rm --volume $PWD:/srv/jekyll:Z -it dockerreg.chtc.wisc.edu:443/htcondor/web
```

This will utilize the latest Jekyll version and map port `8000` to your host.  Within the container, a small HTTP server can be started with the following command:

```
jekyll serve --watch -H 0.0.0.0 -P 8000
```

This will build and serve the website; it can be viewed by navigating your web browser to <http://localhost:8000>.

With the `--watch` flag set, any changes you make to the website source will cause a new version of the website to be built; it usually takes 4-5 seconds between hitting "Save" and then "Refresh" on the website.


# Deploying

Start by building the website. This needs to happen using the Docker container:

```
docker run -p 8000:8000 --rm --volume $PWD:/srv/jekyll:Z -it dockerreg.chtc.wisc.edu:443/htcondor/web /srv/jekyll/script/cibuild
```

From outside the container, run the *cideploy* script to deploy your changes to the live website. Note this must be run from the *htcondor-web* root folder:

```
script/cideploy
```