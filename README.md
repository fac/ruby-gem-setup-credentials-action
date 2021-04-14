# RubyGems Setup GitHub Package Registry Action

## Description

This action will setup ruby gem access (the `~/.gem/credentials` file) for the GitHub Package Registry. If you pushing a gem to the same repo, all it needs is the default github actions token.

The key is added under the name `github` and we also set environment variables (`GEM_HOST_API_KEY` and `GEM_HOST`) that can be used to push gems. You can do this your self, but the action is designed to also be used with the [fac/rubygems-push-action](https://github.com/fac/rubygems-push-action).

## Usage

```yaml
    steps:
    - uses: actions/checkout@v2
    - uses: ruby/setup-ruby@v1 # .ruby-version

    - name: Build Gem
      shell: bash
      run: bundle exec rake build

    - name: Setup GPR
      uses: fac/rubygems-setup-gpr-action@v1
      with:
        token: ${{ secrets.github_token }}

    - name: Push Gem
      uses: fac/rubygems-push-action@v1
```

If you want to use your own push or other customizations:

```yaml
    - name: Setup GPR
      uses: fac/rubygems-setup-gpr-action@v1
      with:
        token: ${{ secrets.package_token }}

    - name: Push Gem
      run: gem push --host "$GEM_HOST" foo.gem
```

## Inputs

### token

The token to be used for authenticating with GitHub packages. If you are pushing a gem to the same repo with a matching name, the default token is enough:

```yaml
with:
   token: ${{ secrets.package_token }}
```

## Outputs

None.
## Environment Variables

### GEM_HOST_API_KEY

Set for the workflow by calling the action. Contains the API key string (prefixed token with Bearer), to access the package repo. Used by `gem push`.

### GEM_HOST

Set for the workflow by calling the action. The host URL for pushing gems to the package repo for the currently building repo.
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
