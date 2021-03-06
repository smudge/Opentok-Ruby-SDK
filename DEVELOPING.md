# Development Guidelines

This document describes tools, tasks and workflow that one needs to be familiar with in order to effectively maintain
this project. If you use this package within your own software as is but don't plan on modifying it, this guide is
**not** for you.

## Tools

*  [Bundler](http://bundler.io): used to ensure gems that are used as dependencies are uniform with other contributors
   and maintainers. The first thing you should do once you've cloned this repository is to run `bundle install`. This
   will also generate the `Gemfile.lock` file, which caches the configuration of gems you are using. Bundler is
   included with all recent versions of Ruby.

*  [Rake](http://rake.rubyforge.org/): used to run predefined tasks. Rake is usually run by prefixing `bundle exec` to
   ensure that dependencies used for the task are provided through bundler. Example: `$ bundle exec rake spec`. Rake
   is installed by Bundler when `bundler install` is run.

## Tasks

### Building

Building is required to generate the gem. A gem is a distributable artifact suitable for installing on other systems.

*  `rake build` - builds the gem into the `pkg` directory.

### Testing

This project's tests are written using [RSpec](http://rspec.info/). It also uses the VCR and WebMock helpers.

*  `rake spec` - run the test suite.

### Generating Documentation

This project's reference documentation is generated by Yard and resides in the `docs` directory of the project.
Common tasks:

*  `rake yard` - generate the reference documentation.

### Releasing

In order to create a release, the following should be completed in order.

1. Ensure all tests are passing (`rake spec`) and that there is enough test coverage.
1. Make sure you are on the `master` branch of the repository, with all changes merged/committed already.
1. Update the version number in the source code (`lib/opentok/version.rb`) and the README. See [Versioning](#versioning) for
   information about selecting an appropriate version number.
1. Commit the version number change with the message ("Update to version v.x.x.x"), substituting the new version number.
1. Ensure you have permission to update the `opentok` gem on Rubygems: <https://rubygems.org/gems/opentok>.
1. Run `rake release`, which will create a git tag for the version number, build, and push the gem to Rubygems.
1. Change the version number for future development by adding ".alpha.1", then make another commit with the message
   "Beginning development on next version".
1. Push the changes to the main repository (`git push origin master`).

## Workflow

### Versioning

The project uses [semantic versioning](http://semver.org/) as a policy for incrementing version numbers. For planned
work that will go into a future version, there should be a Milestone created in the Github Issues named with the version
number (e.g. "v2.2.1").

During development the version number should end in ".alpha.1" or ".beta.x", where x is an increasing number starting
from 1.

### Branches

*  `master` - the main development branch.
*  `feat.foo` - feature branches. these are used for longer running tasks that cannot be accomplished in one commit.
   once merged into master, these branches should be deleted.
*  `vx.x.x` - if development for a future version/milestone has begun while master is working towards a sooner
   release, this is the naming scheme for that branch. once merged into master, these branches should be deleted.

### Tags

*  `vx.x.x` - commits are tagged with a final version number during release.

### Issues

Issues are labelled to help track their progress within the pipeline.

*  no label - these issues have not been triaged.
*  `bug` - confirmed bug. aim to have a test case that reproduces the defect.
*  `enhancement` - contains details/discussion of a new feature. it may not yet be approved or placed into a
   release/milestone.
*  `wontfix` - closed issues that were never addressed.
*  `duplicate` - closed issue that is the same to another referenced issue.
*  `question` - purely for discussion

### Management

When in doubt, find the maintainers and ask.
