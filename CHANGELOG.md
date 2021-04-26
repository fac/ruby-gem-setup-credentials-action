# CHANGELOG

## [Unreleased]

## [2.0.0] - 2021-04-26

- Change: Name change to `ruby-gem-setup-credentials` from `ruby-gem-setup-github-packages-action`
- Change: Don't export the token in the environment by default, users should use the key name.
- Add: Input `key` to set the key name, defaults to `github`.
- Add: Input `export-token` to control exporting the environment, default false.

## [1.1.0] - 2021-04-15

- Change: name to ruby-gem-setup-github-packages-action. Old name still works due too GH redirects.

## [1.0.0] - 2021-04-14

- Add: Action that can log into github package registry using a passed (github or other) token.

----

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).
