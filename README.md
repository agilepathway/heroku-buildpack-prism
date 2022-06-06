# heroku-buildpack-prism
[Heroku](https://www.heroku.com/) [Buildpack](https://devcenter.heroku.com/articles/buildpacks) for 
[Prism's HTTP mock server](https://stoplight.io/open-source/prism)

Prism creates a mock server from any [OpenAPI](https://oai.github.io/Documentation/introduction.html) spec.

This Heroku buildpack enables Prism mock servers to be deployed easily on Heroku.

The premise is to have **a Heroku app dedicated for the Prism mock of one OpenAPI spec** i.e. if you have three OpenAPI specs that you want to have Prism mocks on Heroku for, you will have three corresponding Heroku apps.  If you also have an implementation of your OpenAPI spec that you also want to deploy on Heroku, you would use an entirely separate Heroku app for that.

## Installation

1. Tell your Heroku app to use this `heroku-buildpack-prism` buildpack

   Setting the buildpack can either be done at 
   [Heroku app creation time](https://devcenter.heroku.com/articles/heroku-cli-commands#heroku-apps-create-app), e.g:

   `heroku create --region eu --buildpack https://github.com/agilepathway/heroku-buildpack-prism.git my-heroku-app`

   or at any time by using [`heroku buildpacks:set`](https://devcenter.heroku.com/articles/heroku-cli-commands#heroku-buildpacks-set-buildpack), e.g:

   `heroku buildpacks:set https://github.com/agilepathway/heroku-buildpack-prism.git`

2. Specify the Prism mock server startup command in the Heroku Procfile

   Heroku apps include a [Procfile](https://devcenter.heroku.com/articles/procfile) that specifies the commands that are executed by the app on startup.

   Create a file called `Procfile` (no file extension), with the following content - replacing `openapi.yaml` with the path to your YAML or JSON OpenAPI spec.

   `web: prism mock openapi.yaml --errors -h 0.0.0.0 -p $PORT`

   Note that the host has to be specified as `0.0.0.0` and the port has to be Heroku's dynamically assigned `$PORT`

That's it! :sunglasses:




