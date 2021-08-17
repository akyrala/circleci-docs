---
layout: classic-docs
title: "Migrating to next-gen Convenience Images"
short-title: "Migrating to next-gen Convenience Images"
description: "Migrating to next-gen Convenience Images"
order: 30
version:
- Cloud
- Server v2.x
---

* TOC
{:toc}


## Overview

Last year (2020) CircleCI introduced the next generation (next-gen) of Convenience Images. These new images are designed to replace the legacy Convenience Images that came out during the announcement of CircleCI 2.0, about 4 years ago. The next-gen CircleCI Convenience Images are designed from the ground up for a Continuous Integration environment. They’re designed to be faster, more efficient, and more importantly, more reliable. You can learn more about all of the features on our blog post. As we begin to deprecate the legacy images, here is information on the migration process.

Moving from a legacy to next-gen image is easy and straightforward. All legacy images have a Docker namespace of “circleci” while next-gen images have a Docker namespace of “cimg”. For example, migrating from the legacy Ruby or Python image to the respective next-gen:

circleci/ruby:2.3.0 -> cimg/ruby:2.3.0
circleci/python:3.8.4 -> cimg/python:3.8.4


## Changes

### Deprecated images

There are a few images that will be completely deprecated, without a replacement, as well as one that has a name change. The buildpack-deps, JRuby, and DynamoDB images will be fully deprecated with no next-gen equivalents. If you are using the buildpack-deps image, the suggestion is to use the new CircleCI Base image, cimg/base. For the other two images, you can install the software yourself in the base image or use a 3rd-party image instead. The Go image name has been changed from golang to go. All of the Legacy to Next-Gen image changes are captured below in this table:


| Legacy Image | Next-Gen Image |
| --- | --- |
| circleci/buildpack-deps | cimg/base |
| circleci/jruby | No suggested path |
| circleci/dynamodb | No suggested path |
| circleci/golang | cimg/go |


### Browser Testing

With legacy images, there were 4 different variant tags you could use to get browser testing for a particular image. For example, if you were doing browser testing with the Python v3.7.0 image, you might have used Docker image: circleci/python:3.7.0-browsers. These 4 tags have now been consolidated into a single tag designed to be used together with the CircleCI Browser Tools orb.


Legacy Variant Tags


Next-gen Variant Tag
-browsers
-browsers + Browser Tools Orb
-browsers-legacy
-node-browsers
-node-browsers-legacy


The new, single browsers variant tag includes Node.js, common utilities to use in browser testing such as Selenium, but not the actual browsers. Please note the browsers are no longer pre-installed. Instead, browsers such as Google Chrome and Firefox as well as their drivers Chromedriver and Gecko are installed via the browsers-tools orb. This provides the flexibility to mix and match the browser versions you need in a build rather than using strictly what CircleCI provides. You can find examples of how to use this orb here.

Using Ubuntu as the Single Base OS

Legacy images had variant tags for several different base operating systems (OS). Some images were versions of Debian and Ubuntu while other images provided several different bases. This is no longer the case. All CircleCI next-gen images are based on the latest LTS release of Ubuntu.

With the base image, at least two LTS releases and non-EOL’d standard releases will be supported.


## Troubleshooting

When migrating to a next-gen image, there might be some software issues. Common issues include a library you were using now has a different version or an apt package is no longer pre-installed. In this scenario simply install that package using:

sudo apt-get update && sudo apt-get install -y <the-package>

Every image has its own GitHub repository. You can find them here. These repositories are where you can learn more about an image, what makes up the image, open GitHub Issues, and contribute PRs. If you’re having an issue with an image, especially if it’s a migration issue, you can open up a GitHub Issue and ask questions. You can always open up a Support ticket or reach out on CircleCI Discuss. 

