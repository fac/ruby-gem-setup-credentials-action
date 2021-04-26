# Ruby Gem - Setup Credentials Action

## Description

This action will setup ruby gem access (the `~/.gem/credentials` file) with the given token. If your pushing a gem to GH packages using the same repo as it builds in, all it needs is the default GitHub actions token. For other repos you will need to add a secret you can then pass to the input.

The key is added under the name `github` by default, change with the `key` input. Optionally you can export environment variable `GEM_HOST_API_KEY` which is read by (more recent versions of) the `gem` command. However we advise you to be explicit and pass the key name `github` as an input or argument instead.

You can do the gem push your self, but the action is also designed to be used with the [fac/ruby-gem-push-action](https://github.com/fac/ruby-gem-push-action).

## Usage

```yaml
    steps:
    - uses: actions/checkout@v2
    - uses: ruby/setup-ruby@v1 # .ruby-version

    - name: Build Gem
      shell: bash
      run: bundle exec rake build

    - name: Setup GPR
      uses: fac/ruby-gem-setup-credentials-action@v2
      with:
        token: ${{ secrets.github_token }}

    - name: Push Gem
      uses: fac/ruby-gem-push-action@v2
```

If you want to use your own push or other customizations:

```yaml
    - name: Setup GPR
      uses: fac/ruby-gem-setup-credentials-action@v2
      with:
        token: ${{ secrets.package_token }}

    - name: Push Gem
      run: gem push --key=github --host='https://rubygems.pkg.github.com/${{ github.repository_owner }}' foo.gem
```

## Inputs

### token

The token to be used for authenticating with GitHub packages. If you are pushing a gem to the same repo with a matching name, the default token is enough:

```yaml
with:
   token: ${{ secrets.github_token }}
```

### key

The key name to use in the credentials file. Default is `github`.

### export-token

Set true to export the GEM_HOST_API_KEY environment variable.

## Outputs

None.
## Environment Variables

### GEM_HOST_API_KEY

Optionally exported by calling the action. Contains the API key string (prefixed token with Bearer), to access the package repo. Used by `gem push`.

## Authors

* FreeAgent <opensource@freeagent.com>

## Licence

```
Copyright 2021 FreeAgent Central Ltd.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
