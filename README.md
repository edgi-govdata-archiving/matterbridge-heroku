# **IMPORTANT! We've moved development of this repo to the `main` branch. You will not be able to merge changes into `master`.**

## **UPDATING LOCAL CLONES**

(via [this link](https://www.hanselman.com/blog/EasilyRenameYourGitDefaultBranchFromMasterToMain.aspx), thanks!)

If you have a local clone, you can update and change your default branch with the steps below.

```sh
git checkout master
git branch -m master main
git fetch
git branch --unset-upstream
git branch -u origin/main
git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main
```

The above steps accomplish:

1. Go to the master branch
2. Rename master to main locally
3. Get the latest commits from the server
4. Remove the link to origin/master
5. Add a link to origin/main
6. Update the default branch to be origin/main

[![Code of Conduct](https://img.shields.io/badge/%E2%9D%A4-code%20of%20conduct-blue.svg?style=flat)](https://github.com/edgi-govdata-archiving/overview/blob/master/CONDUCT.md)

# Matterbridge-heroku

This is a fork of [the original
`matterbridge-heroku`](https://github.com/cadecairos/matterbridge-heroku).

It includes [a custom config file][config] specific to one implementation, but this can easily be modified in a new fork.

## About this Fork

[**Heroku**](https://www.heroku.com/what) is a platform for easily deploying
applications.

A [**buildpack**](https://docs.cloudfoundry.org/buildpacks/) provides
framework and runtime support for apps running on platforms like Heroku.

An [**_inline_ buildpack**](https://github.com/kr/heroku-buildpack-inline#readme) is a special buildpack that includes code for both the app and the
buildpack that _runs_ the app.

[**Matterbridge**](https://github.com/42wim/matterbridge#readme) is a
simple _bridge_ that can relay messages between a number of different
chat services, essentially connecting separate chat tools.

This fork is intended to help bridge channels between both the EDGI and
Archivers Slack teams.

* Required envvars:
  * `MATTERBRIDGE_VERSION`. Use a [matterbridge git tag][git-tags].
  * `SLACK_<team name>_TOKEN`. See [_Slack bot setup_ documentation][bot-setup].
* Optional envvars:
  * `MATTERBRIDGE_URL`. Use this to download the binary from a custom
    url instead of the tagged release from the official GitHub repo.
    (Setting this makes `MATTERBRIDGE_VERSION` ignored.)
    * With caution, you may want to use the [latest nightly matterbridge
      build](https://bintray.com/42wim/nightly/Matterbridge/_latestVersion)
      while waiting on the next official release.
  * `DEBUG`. Set to "1" to log all message events across bridges.
* Auto-deploys `master` branch to our heroku app: `edgi-matterbridge`
* `master` branch is protected branch, and changes must go through pull
  request process.
* Edit channel bridge config via [`config/config-heroku-template.toml`][config].

   [bot-setup]: https://github.com/42wim/matterbridge/wiki/Slack-bot-setup
   [git-tags]: https://github.com/42wim/matterbridge/tags
   [config]: config/config-heroku-template.toml
