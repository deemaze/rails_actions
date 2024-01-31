# rails-actions
This repo contains a few composite GitHub Actions workflows extracted from deemaze's ruby on rails projects. By using them you'll be
able to DRY your GitHub Actions workflows.

These are the available actions:
- `setup-rails-dependencies`: installs a ruby version, and optionally a node version too. Also runs `bundle install` (and `yarn install` if node is required);
- `run-overcommit`: runs overcommit, optionally handles setting up a db if any db checks are required;
- `setup-db-and-run-rspec`: sets up a db and runs RSpec; can also handle precompilling rails assets and caching them beforehand if the project is using webpacker/shakapacker;
- `capistrano-staging-deploy`: deploys the project to a staging environment using capistrano.


## setup-rails-dependencies

**Available inputs:**
- `ruby_version`: Which ruby version to install;
- `install_node`: (Optional) Pass true if node/yarn are required;
- `node_version`: Which node version to install. Required if `install_node` is set to `true`.


## run-overcommit

**Available inputs:**
- `db_checks_enabled`: (Optional) Set to `true` if a db should be setup to run database checks (e.g., `database_consistency`);
- `DEVELOPMENT_CREDENTIALS_KEY`: The contents of the `config/credentials/development.key` file. Required if `db_checks_enabled` is set to true.


## setup-db-and-run-rspec

**Available inputs:**
- `TEST_CREDENTIALS_KEY`: The contents of the `config/credentials/test.key` file;
- `precompile_webpacker_assets`: (Optional) Pass true if rails assets should be compiled before running RSpec. Usually this is required when using webpacker/shakapacker.


## capistrano-staging-deploy

**Available inputs:**
- `ruby_version`: Which ruby version to install;
- `ssh_private_key`: An SSH private key with access to the webserver to be used by capistrano;
- `RAILS_MASTER_KEY`: The contents of the `config/master.key` file;
- `STAGING_CREDENTIALS_KEY`: The contents of the `config/credentials/staging.key` file;
- `SLACK_WEBHOOK_URL`: The Slack webhook URL to post to after the deploy succeeds;
- `SLACK_CHANNEL`: (Optional) The Slack channel to post to; defaults to the channel set when the webhook was created;
- `SLACK_USERNAME`: (Optional) The username to use when posting to Slack;
- `SLACK_ICON_EMOJI`: (Optional) An emoji to use as the picture when posting to Slack.
