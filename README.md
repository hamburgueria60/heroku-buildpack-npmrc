# heroku-buildpack-npmrc
A Heroku buildpack for overriding the .npmrc file in the build directory with the contents of a config var. Necessary for authorizing with npm when installing private packages.

## Configure Multiple Buildpacks

1. Open https://github.com/settings/tokens/new
2. Create a Github Personal Access token with the following scopes: `repo`, `write:packages` and `read:packages`
3. Run `heroku config:set API_CLIENT_GITHUB_AUTH_TOKEN=token`, replacing `token` with the token you created on step 2
4. Add the buildpack to your Heroku app either using the CLI or the Heroku dashboard. The `heroku-buildpack-npmrc` needs to run before any buildpack using npm. In the following example, it runs before the `heroku/nodejs` buildpack.

```bash
$ heroku buildpacks:set --index 1 https://github.com/mindfulchefuk/heroku-buildpack-npmrc.git
$ heroku buildpacks:add heroku/nodejs
```