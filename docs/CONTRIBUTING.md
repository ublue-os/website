---
hide:
  - navigation
---

# Contributing

Thanks for taking the time to look into helping out!
All contributions are appreciated! 
Please refer to our [Code of Conduct](CODE_OF_CONDUCT.md) while you're at it!

Feel free to report issues as you find them, and [helping others in the discussions]() is always appreciated.

# Getting Started

All types of contributions are encouraged and valued.
See the [Table of Contents](#table-of-contents) for different ways to help and details about how this project handles them.
Please make sure to read the relevant section before making your contribution.
It will make it a lot easier for us maintainers and smooth out the experience for all involved.
The community looks forward to your contributions!

If you like the project, but just don't have time to contribute, that's fine. There are other easy ways to support the project and show your appreciation, which we would also be very happy about:

 - Star the project
 - Toot about it
 - Refer this project in your project's readme
 - Mention the project at local meetups and tell your friends/colleagues

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [I Have a Question](#i-have-a-question)
- [I Want To Contribute](#i-want-to-contribute)
- [Reporting Bugs](#reporting-bugs)
- [How to test incoming changes](#how-to-test-incoming-changes)
- [Building Locally](#building-locally)
- [Styleguides](#styleguides)
- [Commit Messages](#commit-messages)
- [Why we insist on using GitHub](#why-we-insist-on-using-github)
- [Join The Project Team](#join-the-project-team)

## Code of Conduct

This project and everyone participating in it is governed by the
[CONTRIBUTING.md Code of Conduct](blob/master/CODE_OF_CONDUCT.md).
By participating, you are expected to uphold this code.
Please report unacceptable behavior to jorge.castro@gmail.com

## I Have a Question

> If you want to ask a question, ask in the [discussion forum](https://github.com/orgs/ublue-os/discussions) or come hang out on [the Discord server](https://discord.gg/WEu6BdFEtp)

## I Want To Contribute

> ### Legal Notice 
> When contributing to this project, you must agree that you have authored 100% of the content, that you have the necessary rights to the content and that the content you contribute may be provided under the project license.

Generally speaking we try to follow the [Lazy Concensus](http://lazyconcens.us/) model of development to keep the builds healthy and ourselves happy. 
    - If you're looking for concensus to make a decision post an issue for feedback and remember to account for timezones and weekends/holidays/work time 
    - We want people to be opinionated in their builds so we're more of a loose confederation of repos than a top-down org
    - Try not to merge your own stuff, ask for a review. At some point when we have enough reviewers we'll be turning on branch protection

### Reporting Bugs

#### Before Submitting a Bug Report

A good bug report should describe the issue in detail. Generally speaking:

- Make sure that you are using the latest version
- Remember that these are unofficial builds, it's usually prudent to investigate an issue before reporting it here or in Fedora!
- Collect information about the bug:
  - `rpm-ostree status -v` usually helps
- Image and Version 
- Possibly your input and the output
- Can you reliably reproduce the issue? And can you also reproduce it with older versions?

### How to test incoming changes

One of the nice things about the image model is that we can generate an entire OS image for every change we want to commit, so this makes testing way easier than in the past.
You can rebase to it, see if it works, and then move back.
This also means we can increase the amount of testers! 

We strive towards a model where proposed changes are more thoroughly reviewed and tested by the community.
If you see a pull request that is opened up on an image you're following you can leave a review on how it's working for you.
At the bottom of every PR you'll see something like this: 

![image](https://user-images.githubusercontent.com/1264109/221305388-3860fc07-212c-4eb9-80d9-5d7a35a77f46.png)

Click on "Add your review", and then you'll see this: 

![image](https://user-images.githubusercontent.com/1264109/221307636-5e312e48-821f-4206-848f-7fbc2c91cd78.png)

Don't worry, you can't mess anything up, all the merging and stuff will be done by the maintainer, what this does is lets us gather information in a more formal manner than just shoving everything in a forum thread.
The more people are reviewing and testing images, the better off we'll be, especially for images that are new.

At some point we'll have a bot that will leave you instructions on how to rebase to the image and all that stuff, but in the meantime we'll leave instructions manually. 

Here's an example: https://github.com/ublue-os/nvidia/pull/49

## Building Locally

The minimum tools required are git and a working machine with podman enabled and configured. 
Building locally is much faster than building in GitHub and is a good way to move fast before pushing to a remote.

### Clone the repo you want

    git clone https://github.com/ublue-os/base.git

### Build the image
    
First make sure you can build an existing image: 
    
    podman build . -t something
    
Then confirm your image built:
    
    podman image ls 

TODO: Set up and push to your own local registry
    
### Make your changes

This usually involved editing the `Containerfile`.
Most techniques for building containers apply here, if you're new to containers using the term "Dockerfile" in your searches usually shows more results when you're searching for information. 

Check out CoreOS's [layering examples](https://github.com/coreos/layering-examples) for more information on customizing. 

### Reporting problems to Fedora

We endevaour to be a good partner for Fedora.

This project is consuming new features in Fedora and ostree, it is not uncommon to find an issue.
It is strongly recommended that you attempt to reproduce the issue with a vanilla Fedora installation to see if it's a uBlue issue or a Fedora issue. 
If you are confused and can't confirm, ask in chat or post in the forums and see if someone more experienced can help out.
Issues that you can confirm should be reported upstream, and in some cases we can help test and find fixes.
Some of the issues you find may involve other dependencies in other projects, in those cases the Fedora team will tell you where to report the issue. 

Upstream bug tracker: [https://github.com/fedora-silverblue/issue-tracker/issues](https://github.com/fedora-silverblue/issue-tracker/issues)

## Styleguides
### Commit Messages

We use [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) and enforce them with a bot to keep the changelogs tidy:

```
chore: add Oyster build script
docs: explain hat wobble
feat: add beta sequence
fix: remove broken confirmation message
refactor: share logic between 4d3d3d3 and flarhgunnstow
style: convert tabs to spaces
test: ensure Tayne retains clothing
```

## Why we insist on using GitHub

If you come to the Discord you might be asked to report an issue to GitHub. DON'T PANIC! 

We do this for a few reasons:

- Scalability - we're purposely designing this project to scale, and that means a focus on:
- Asynchronous Communication - OSS is a worldwide phenonmenon for a reason, forcing us to write everything down and capturing as much data is crucial to our ability to move quickly, at some point we'll have people in every time zone, and keeping that efficient is the key. 
  - Discord search is not an engineering tool, it's for chat, it's extremely difficuly for even the most experienced person to "spin up" by tracking a chat than an issue on GitHub.
  - It feels slow! It does, but over the long term, it is much more efficient, because you are also solving the problem for as many people as you can, so we gotta make it count!
- Leverage chat as much as you can to debug and move fast
  - But when things get over a few messages, start to copying stuff into a text editor so you have it
  - and then file an issue, you can always edit and fix it up later, concentrate on the capture.
  - It's hard to have that discipline, that's why we have teammates.
  - "Oh I'll just file it later" is a good way to learn something, twice. It's going to happen but knowing the trap is a good way to avoid it (or end up gravitating towards it!)
- **DON'T BE AFRAID OF FILING AN ISSUE**
  - Part of our culture is to _teach_ and help each other grow
  - Better to file an issue and have it closed than let a subtle problem spiral out of control
    - Having an issue closed means you've ruled something out, that can be just as important as a solution!
  - That also doesn't mean to file 47 issues around your favorite feature in a 10 minute period
    - If something needs more discussion, [file a proposal](https://github.com/orgs/ublue-os/discussions?discussions_q=is%3Aopen+label%3Aproposal)
- You've earned it
  - The commons depends on everyone chipping in, be proud of your contribution!
    
## Join The Project Team

If you're interested in _maintaining_ something then let us know!

## Attribution
This guide is based on the **contributing.md**. [Make your own](https://contributing.md/)!
