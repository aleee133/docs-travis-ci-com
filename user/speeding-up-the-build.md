---
title: Speed up the build
layout: en

---

Travis CI implements a few optimizations which help to speed up your build,
like in-memory filesystem for DB's files, but there is a range of things
that can be done to improve build times even more.


## Parallelize Builds across Virtual Machines

To speed up a test suite, you can break it up into several parts using
Travis CI's [build
matrix](/user/customizing-the-build/#build-matrix)
feature.

Say you want to split up your unit tests and your integration tests into two
different build jobs. They’ll run in parallel and fully utilize the available
build capacity for your account.

Here's an example of how to utilize this feature in your `.travis.yml`:

```yaml
env:
  - TEST_SUITE=units
  - TEST_SUITE=integration
```
{: data-file=".travis.yml"}

Then you change your script command to use the new environment variable to
determine the script to run.

```yaml
script: "bundle exec rake test:$TEST_SUITE"
```
{: data-file=".travis.yml"}

Travis CI will determine the build matrix based on the environment variables and
schedule two builds to run.

The neat part about this setup is that the unit test suite is usually going to
be done before the integration test suite, giving you a faster visual feedback
on the basic test coverage.

Depending on the size and complexity of your test suite, you can split it up even
further. You could separate different concerns for integration tests into
different subfolders and run them in separate stages of a build matrix.

```yaml
env:
  - TESTFOLDER=integration/user
  - TESTFOLDER=integration/shopping_cart
  - TESTFOLDER=integration/payments
  - TESTFOLDER=units
```
{: data-file=".travis.yml"}

Then you can adjust your script command to run rspec for every subfolder:

```yaml
script: "bundle exec rspec $TESTFOLDER"
```
{: data-file=".travis.yml"}

For instance, the Rails project uses the build matrix feature to create separate
jobs for every database to test against and also to split up the tests by
concern. One set runs tests only for the railties, another one for actionpack,
actionmailer, activesupport and a whole bunch of sets run the activerecord
tests against multiple databases. See their [.travis.yml
file](https://github.com/rails/rails/blob/master/.travis.yml) for more examples.

## Parallelize a Build on a single Virtual Machine

Parallelizing the test suite on one virtual machine depends on the language and test runner:

- For Ruby and RSpec use the [parallel_tests](https://github.com/grosser/parallel_tests) gem.
- For Java, use the built-in feature [to run tests in parallel
  using JUnit](http://incodewetrustinc.blogspot.com/2009/07/run-your-junit-tests-in-parallel-with.html).

To give you an idea of the speedup we are talking about, I've tried to run tests in parallel on `travis-core` and I was able to see a drop from about 26 minutes to about 19 minutes across 4 jobs.

## Parallelize RSpec, Cucumber, and Minitest on Multiple VMs

If you want to perform parallel tests for RSpec, Cucumber, or Minitest on multiple VMs to get faster feedback from CI, you can try [knapsack](https://github.com/ArturT/knapsack) gem. It will split tests across virtual machines and make sure that tests will run a comparable time on each VM (each job will take similar time). You can use our matrix feature to set up knapsack.

### RSpec Parallelization Example

```yaml
script: "bundle exec rake knapsack:rspec"
env:
  global:
    - MY_GLOBAL_VAR=123
    - CI_NODE_TOTAL=2
  jobs:
    - CI_NODE_INDEX=0
    - CI_NODE_INDEX=1
```
{: data-file=".travis.yml"}

Such configuration will generate a matrix with the 2 following ENV rows:

```
MY_GLOBAL_VAR=123 CI_NODE_TOTAL=2 CI_NODE_INDEX=0
MY_GLOBAL_VAR=123 CI_NODE_TOTAL=2 CI_NODE_INDEX=1
```

### Cucumber Parallelization Example

```yaml
script: "bundle exec rake knapsack:cucumber"
env:
  global:
    - CI_NODE_TOTAL=2
  jobs:
    - CI_NODE_INDEX=0
    - CI_NODE_INDEX=1
```
{: data-file=".travis.yml"}

### Minitest Parallelization Example

```yaml
script: "bundle exec rake knapsack:minitest"
env:
  global:
    - CI_NODE_TOTAL=2
  jobs:
    - CI_NODE_INDEX=0
    - CI_NODE_INDEX=1
```
{: data-file=".travis.yml"}

### RSpec, Cucumber, and Minitest Parallelization Example

If you want to parallelize a test suite for RSpec, Cucumber, and Minitest at the same time, define script in `.travis.yml` as follows:

```yaml
script:
  - "bundle exec rake knapsack:rspec"
  - "bundle exec rake knapsack:cucumber"
  - "bundle exec rake knapsack:minitest"
```
{: data-file=".travis.yml"}

You can find more examples in [knapsack docs](https://github.com/ArturT/knapsack#info-for-travis-users).

## Caching the Dependencies

Installing the dependencies for a project can take quite some time for bigger projects. In
order to make it faster, you may try caching the dependencies.

You can either use our [built-in caching](/user/caching/) or roll your own on S3. If you
want to roll your own and you use Ruby with Bundler, check out [the great WAD project](https://github.com/Fingertips/WAD).
For other languages, you can use s3 tools directly to upload and download the dependencies.

## Environment-Specific Ways to Speed up a Build

In addition to the optimizations implemented by Travis, there are also
several environment-specific ways you may consider to increase the speed of
your tests.

### PHP Optimizations

PHP VM images on Travis CI provide several PHP versions which include
XDebug. The XDebug extension is useful, if you wish to generate code coverage
reports in your Travis builds, but it has been shown to have a negative effect
upon performance.

You may wish to consider
[disabling the PHP XDebug extension](/user/languages/php/#disabling-preinstalled-php-extensions) for your
builds if:

- you are not generating code coverage reports in your Travis tests; or
- you are testing on PHP 7.0 or above and are able to use the [PHP Debugger (phpdbg)](https://github.com/krakjoe/phpdbg)
  which may be faster.

#### phpdbg Example

```yaml
before_script:
  - phpenv config-rm xdebug.ini
  - composer install

script:
  - phpdbg -qrr phpunit
```
{: data-file=".travis.yml"}

### Makefile Optimization

If your makefile build consists of independent parts that can be safely
parallelized, you can [run multiple recipes
simultaneously](https://www.gnu.org/software/make/manual/html_node/Parallel.html).
See [Virtualization
environments](/user/reference/overview/#virtualization-environments) to determine
how many CPUs an environment normally has and set the `make` job parameter to a
similar number (or slightly higher if your build frequently waits on disk I/O).

> Note that doing this will cause concurrent recipe output to become interleaved.

#### Makefile Parallelization Example

```yaml
env:
  global:
    - MAKEFLAGS="-j 2"
```
{: data-file=".travis.yml"}
