# newrelic-cli

[![CircleCI](https://circleci.com/gh/newrelic/newrelic-cli.svg?style=svg)](https://circleci.com/gh/newrelic/newrelic-cli)
[![Go Report Card](https://goreportcard.com/badge/github.com/newrelic/newrelic-cli?style=flat-square)](https://goreportcard.com/report/github.com/newrelic/newrelic-cli)
[![GoDoc](https://godoc.org/github.com/newrelic/newrelic-cli?status.svg)](https://godoc.org/github.com/newrelic/newrelic-cli)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/newrelic/newrelic-cli/blob/master/LICENSE)
[![Release](https://img.shields.io/github/release/newrelic/newrelic-cli/all.svg)](https://github.com/newrelic/newrelic-cli/releases/latest)

The New Relic CLI is an officially supported command line interface for New Relic, released as part of the [Developer Toolkit](https://newrelic.github.io/developer-toolkit/)

## Overview

**THIS IS AN ALPHA / PRE-RELEASE: Subject to drastic changes**

The New Relic CLI is a project to consolidate some of the tools that New Relic
offers for managing resources.  Current scope is limited while the framework is
being developed, but the tool as-is does perform a subset of tasks.

* Entity Search: Search for entities across all your New Relic accounts
* Entity Tagging: Manage tags across all of your entities
* Deployment Markers: Easily record an APM Application deployment within
  New Relic.

### Getting Started

For a quick guide on getting started with the New Relic CLI, see our [Getting
Started](https://github.com/newrelic/newrelic-cli/blob/master/docs/GETTING_STARTED.md)
page.

The latest New Relic CLI documentation is available [here](https://github.com/newrelic/newrelic-cli/blob/master/docs/cli/newrelic.md)

### Other Resources

There are a handful of other useful tools that this does not replace.  Here are
some useful links to other tools that you might be interested in using at this
time.

* [NR1 CLI](https://developer.newrelic.com/build-tools/new-relic-one-applications/cli):
  Command line interface for managing development workflows for custom Nerdpacks on New Relic One.
* [New Relic Lambda CLI](https://github.com/newrelic/newrelic-lambda-cli): A
  CLI to install the New Relic AWS Lambda integration and layers.
* [New Relic Diagnostics](https://docs.newrelic.com/docs/agents/manage-apm-agents/troubleshooting/new-relic-diagnostics):
  A utility that automatically detects common problems with New Relic agents.


## Usage

### Installation

Today pre-release binaries have been created on the GitHub releases page.  You
can dowload the latest release [here](https://github.com/newrelic/newrelic-cli/releases)


### Docker

There is a docker image that can be utilized for running commands as well.

*Note:* You must pass in `NEW_RELIC_API_KEY`, which is your [Personal API
Key](https://docs.newrelic.com/docs/apis/get-started/intro-apis/types-new-relic-api-keys#personal-api-key)

#### APM Application Example

```bash
# Pull the latest container
$ docker pull newrelic/cli

# Run the container interactively, remove it once the command exists
# Also must pass $NEW_RELIC_API_KEY to the container
$ docker run -it --rm \
    -e NEW_RELIC_API_KEY \
    newrelic/cli \
    apm application get --name WebPortal --accountId 2508259

[
  {
    "AccountID": 2508259,
    "ApplicationID": 204261368,
    "Domain": "APM",
    "EntityType": "APM_APPLICATION_ENTITY",
    "GUID": "MjUwODI1OXxBUE18QVBQTElDQVRJT058MjA0MjYxMzY4",
    "Name": "WebPortal",
    "Permalink": "https://one.newrelic.com/redirect/entity/MjUwODI1OXxBUE18QVBQTElDQVRJT058MjA0MjYxMzY4",
    "Reporting": true,
    "Type": "APPLICATION"
  }
]
```


### Getting Help

In order to get help about what commands are available, the trusty `--help`
flag is here to assist.  Alternatively, using just the `help` subcommand also works.

```
newrelic --help
newrelic help
```

Help is also available for the nested sub-commands.  For example, the with the
following command, you can retrieve help for the `apm` sub-command.

```
newrelic apm --help
newrelic help apm
```

Using the CLI in this way, users are able to inspect what commands are
available, with some instruction on their usage.

### Patterns

Throughout the help, you may notice common patterns.  The term `describe` is
used to perform list or get operations, while the `create` and `delete` terms
are used to construct or destroy an item, respectively.

## Development

### Requirements

* Go 1.13.0+
* GNU Make
* git


### Building

This package does not generate any direct usable assets (it's a library).  You can still run the build scripts to validate you code, and generate coverage information.

```
# Default target is 'build'
$ make

# Explicitly run build
$ make build

# Locally test the CI build scripts
# make build-ci
```


### Testing

Before contributing, all linting and tests must pass.  Tests can be run directly via:

```
# Tests and Linting
$ make test

# Only unit tests
$ make test-unit

# Only integration tests
$ make test-integration
```

### Commit Messages

Using the following format for commit messages allows for auto-generation of
the [CHANGELOG](CHANGELOG.md):

#### Format:

`<type>(<scope>): <subject>`

| Type | Description | Change log? |
|------| ----------- | :---------: |
| `chore` | Maintenance type work | No |
| `docs` | Documentation Updates | Yes |
| `feat` | New Features | Yes |
| `fix`  | Bug Fixes | Yes |
| `refactor` | Code Refactoring | No |

#### Scope

This refers to what part of the code is the focus of the work.  For example:

**General:**

* `build` - Work related to the build system (linting, makefiles, CI/CD, etc)
* `release` - Work related to cutting a new release

**Package Specific:**

* `newrelic` - Work related to the New Relic package
* `http` - Work related to the `internal/http` package
* `alerts` - Work related to the `pkg/alerts` package



### Documentation

**Note:** This requires the repo to be in your GOPATH [(godoc issue)](https://github.com/golang/go/issues/26827)

```
$ make docs
```

## Community

New Relic hosts and moderates an online forum where customers can interact with New Relic employees as well as other customers to get help and share best practices. 

* [Roadmap](https://newrelic.github.io/developer-toolkit/roadmap/) - As part of the Developer Toolkit, the roadmap for this project follows the same RFC process
* [Issues or Enhancement Requests](https://github.com/newrelic/newrelic-cli/issues) - Issues and enhancement requests can be submitted in the Issues tab of this repository. Please search for and review the existing open issues before submitting a new issue.
* [Contributors Guide](CONTRIBUTING.md) - Contributions are welcome (and if you submit a Enhancement Request, expect to be invited to contribute it yourself :grin:).
* [Community discussion board](https://discuss.newrelic.com/c/build-on-new-relic/developer-toolkit) - Like all official New Relic open source projects, there's a related Community topic in the New Relic Explorers Hub.

Keep in mind that when you submit your pull request, you'll need to sign the CLA via the click-through using CLA-Assistant. If you'd like to execute our corporate CLA, or if you have any questions, please drop us an email at opensource@newrelic.com.

## Support

New Relic has open-sourced this project. This project is provided AS-IS WITHOUT WARRANTY OR SUPPORT, although you can report issues and contribute to the project here on GitHub.

_Please do not report issues with this software to New Relic Global Technical Support._


## Open Source License

This project is distributed under the [Apache 2 license](LICENSE).
