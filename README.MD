# whatsapp-api
This is my version of the project [repository here](https://github.com/pranavms13/whatsapp-node-api), intended to run on the free tier of heroku, since most of the problems that were detected could be solved in some way.

## Running Puppeteer on Heroku
Running Puppeteer on Heroku requires some additional dependencies that aren't included on the Linux box that Heroku spins up for you. To add the dependencies on deploy, add the Puppeteer Heroku buildpack to the list of buildpacks for your app under Settings > Buildpacks.

The url for the buildpack is [here](https://github.com/jontewks/puppeteer-heroku-buildpack)

Ensure that you're using `'--no-sandbox'` mode when launching Puppeteer. This can be done by passing it as an argument to your .launch() call:
```
 puppeteer: { args: ['--no-sandbox'] }
```

To use the latest stable version run:

```
heroku buildpacks:add jontewks/puppeteer
```

When you click add buildpack, simply paste that url into the input, and click save. On the next deploy, your app will also install the dependencies that Puppeteer needs to run.

For more information about this project, [go to](https://github.com/puppeteer/puppeteer/blob/main/docs/troubleshooting.md#running-puppeteer-on-heroku), or official GitHub [repository](https://github.com/jontewks/puppeteer-heroku-buildpack)

## Other problems
Other problems are related to cache data stored in the `node_modules` folder, to fix this problem just run the commands

```
heroku plugins:install heroku-builds
```

```
heroku builds:cache:purge -a example-app
```

```
git commit --allow-empty -m "Purge cache"
git push heroku master
```
For more information about go to [how-do-i-clear-the-build-cache](https://help.heroku.com/18PI5RSY/how-do-i-clear-the-build-cache) or [nodejs-support](https://devcenter.heroku.com/articles/nodejs-support#cache-behavior)
## License
MIT