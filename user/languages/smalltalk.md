---
title: Build a Smalltalk Project
layout: en

---


This guide covers build environment and configuration topics specific to Smalltalk
projects. Please make sure to read our
[Onboarding](/user/onboarding/) and
[General Build configuration](/user/customizing-the-build/) guides first.

## Community-Supported Warning

Travis CI support for Smalltalk is provided by [SmalltalkCI](https://github.com/hpi-swa/smalltalkCI) and contributed by the community and may be removed or altered at any time. If you run into any problems, please report them [here](https://github.com/hpi-swa/smalltalkCI/issues).

## Basic configurations

To set up continuous integration for your Smalltalk project, you need a `.travis.yml` and a `.ston` configuration file for SmalltalkCI.

An example `.travis.yml` :

```yaml
language: smalltalk

# Select operating system(s)
os:
  - linux

# Select virtual machine(s)
smalltalk_vm:
  - Squeak-5.0
  - Pharo-5.0

# Select compatible Smalltalk image(s)
smalltalk:
  - Squeak-trunk
  - Squeak-5.0
  - Squeak-4.6
  - Squeak-4.5

  - Pharo-alpha
  - Pharo-stable
  - Pharo-5.0
  - Pharo-4.0
  - Pharo-3.0

  - GemStone-3.3.0
  - GemStone-3.2.12
  - GemStone-3.1.0.6
```
{: data-file=".travis.yml"}

This is a minimal `.smalltalk.ston` that uses  [Metacello](https://github.com/dalehenrich/metacello-work) to test on all supported platforms:

```javascript
SmalltalkCISpec {
  #loading : [
    SCIMetacelloLoadSpec {
      #baseline : 'MyProject',
      #directory : 'packages',
      #platforms : [ #squeak, #pharo, #gemstone ]
    }
  ]
}
```
{: data-file=".smalltalk.ston"}

## Configuration

This documentation is just a minimal example and not as exhaustive as [SmalltalkCI's `README.md`](https://github.com/hpi-swa/smalltalkCI#templates).

## Build Config Reference

You can find more information on the build config format for [Smalltalk](https://config.travis-ci.com/ref/language/smalltalk) in our [Travis CI Build Config Reference](https://config.travis-ci.com/).
