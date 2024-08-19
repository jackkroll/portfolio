---
title: "It's my first time doing X"
showDate: false
summary: "Some issues I ran into and what you can do to avoid that"
showSummary: True
showReadingTime: False
---
## Is this really something I can do?
This project had a lot of firsts for me and I think it's completely something you can do as long as you're willing to learn a lot :)

## What is Git/Github??
Git is a versioning system, and Github is an online platform that can host it. Similarly to if you made a video and uploaded it to YouTube, except way nerdier and complicated
### Repository
This is the place where your project lives. It is versioned and can have various branches
### Branches
These are short term diversions from the main branch, this is typically done for a beta or small feature additions that will later be merged to the main branch after revision
## Linux??
This is just another operating system like Windows or macOS. This will typically result in more terminal/command line usage which is okay, it's just something you'll need to figure out
## How should I implement X?
It depends on where it needs to be run and there are a few pre-configured options such as
- On boot
- On LMNL startup
- As a threaded background process
## How should I store X data?
For small things that won't have a lot of writing to it, I personally recommend putting it into the `/ref/config.json` file. If you have any other generic assets please place them in the `/ref` folder too
### This require lots of read/write data
I would suggest an SQL database or something similarly locally hosted. Currently, there is an online [Firebase Firestore](https://firebase.google.com/docs/firestore) database hosting all information. If you are looking to change this please [email me](mailto:me@jackk.dev)