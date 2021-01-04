# My Biggest Beef With Open Source

## Preface

This post is based on my poor experience with OSS software such as GIMP, Darktable and several CAD programs.
I find most of them barely usable and in this post I try to conjecture a reason as to why it happens.

A TL;DR of this post is:

> Open-Source Software does not place enough emphasis on user experience.

With our little summary in mind, let me add some important notes:

- This post is about regular users and things developers can do to ease their pains.
- I'll be talking about software with some kind of GUI (regardless of being native or web-based).
- Not all OSS user experiences suck.
- The user experience extends far beyond the interface.

## Introduction

As the presence of open-source software grows in everyday life,
we developers ought to get to know our target audience and take their advice.
While the audience might not be skilled in development, it needs to be skilled in using the product we deliver,
as such, the product's target audience should be an important part of the development process,
even without contributing code.

> There are only 10 kinds of people in this world, those who understand binary and those who don't.

Extending on the dichotomy built by the joke, we can say there are two kinds of people in this world:
developers and non-developers.
The former are the ones that build the software used by both groups.
This creates a problem as the latter will not have a say on how the software is built in the first place.
I am not arguing that non-developers should tell us how to design software,
however, I am saying that we should take their feedback into account when building a product for them,
since they'll be the ones who use it.

So far, what I've said is obvious, when building the product for a target audience, take their needs into account.
Regardless of how obvious it is, I argue we constantly forget to do so.

## The Closed Open-Source Software

I know that OSS stands for software whose source code is *open* for everyone to see,
however, with the recent efforts put into making the OSS community actually *open* and more welcoming
to people from all walks of life,
I think it is time we also consider users are potential contributors.

We already do that: we add documentation to the code
and write contribution guides and rules of conduct to our projects,
but while these resources are applicable to most users,
they are usually developer oriented.

Considering end-users in the software development process would not only benefit the final product,
as it is in-line with the open source philosophy, a community open to all,
where everyone is allowed to have a voice.

### The Culprits

I think its time I provide some arguments in favor of my points.
I'll show some applications I use (or have tried to use) and comment on their pain points for regular users.

### GIMP

GIMP is a popular image manipulation software, we can consider it as a "direct" competitor to Adobe Photoshop.
To put things into perspective, I've learned to use Photoshop when I was a teen,
however, years later I still find GIMP's interface confusing.

*I tried to take a screenshot, but GIMP captures my keyboard strokes for shortcuts (?).*
Moving on, if you go to `Help` and in the menu click `Bug Reports and Feature Requests`,
you will be redirected to the GNOME project GitLab.
This is less than ideal, requiring a non-technical user to create an account to submit a bug report
or a feature request is creating an unnecessary entry barrier.
The user probably has never heard of GitLab, let alone git, it has no need to know what both are.

Nonetheless, creating an account would mean that
other projects under the GNOME project are also accessible for feedback,
this great when you take into account that the GNOME project hosts endless amounts of software.

