# HTCondor Website

This git repository contains the source code for the refactored HTCondor website.If you want to learn more about HTCondor, [visit the website itself](https://htcondor.org).


# Development

The HTCondor website is implemented in [Jekyll](https://jekyllrb.com/). We've provided a Docker image which contains all the necessary libraries to build the website and preview it in a web browser.

## Obtaining Docker image

Grab the **htcondor/web** image from our Docker Hub:
```
docker pull dockerreg.chtc.wisc.edu:443/htcondor/web
```

## Building the website

After making changes to the Jekyll source files, use the Docker image to preview your changes. Run the following from your computer while inside the checked-out copy of the website source:

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

To deploy any changes you've made to the website, simply commit them to your local git repo, then push the changes to master:

```
git push origin master
```

From there, a combination of GitHub actions and cron jobs will take care of the rest. You should see your changes appear on http://htcondor.org within the next 10 minutes.