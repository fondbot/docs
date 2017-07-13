# Introduction

## Overview

FondBot is a framework for building chat bots.

The main goal of this project is to provide elegant and flexible architecture to develop and maintain chatbot projects from small to the big ones.

## Features

* Intents
* Built-in finite state machine (conversation system)
* Asynchronous message sending
* Drivers: Facebook, Telegram, VK Communities and more...

## Release Management & Version Lifecycle

FondBot strictly follows [semantic versioning](http://semver.org). 

Branches are created using the following pattern: [MAJOR].[MINOR]

Release tags are never deleted. 

When there is a new major release, only the latest minor release of the previous major release will receive bug & security fixes. Hence, if there are 1.0, 1.1, 1.2, 2.0 releases, 1.2 will receive bug & security patches, but 1.0 and 1.1 will not. 

No new functionality will be added to the old major releases. 

Deprecated functionality is removed in the next major release.

The major release which is under development lives in master. 

## Community

Join our open Slack channel:
[https://fondbot.signup.team](https://fondbot.signup.team)
