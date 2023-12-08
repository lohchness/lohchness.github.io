# lohchness.github.io

[Lohchness public website](lohchness.github.io)

Powered by Ruby and Jekyll. Text-focused custom theme. Deployed on GitHub pages.

Requires Ruby, RubyGems, and [Jekyll](https://github.com/jekyll/jekyll) to run. 

`cd` into the root directory.

```
bundle exec jekyll s
```

The website will be located at `localhost:4000`. Changes in `_config.yml` will require a reload.

# GitHub Deployment

Double check `/.github/workflows/` for GitHub Actions.

If `Gemfile.lock` is commited and you are not running Linux, update the platform list of the lock-file:

`bundle lock --add-platform x86_64-linux`

Then, configure the Pages service. Under Settings>Pages, select GitHub Actions in the Source section under Build and deployment.

Push any commits to trigger the workflow.