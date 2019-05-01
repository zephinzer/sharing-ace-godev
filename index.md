---
title: GoDev
separator: <!-- / -->
verticalSeparator: <!-- - -->
theme: night
revealOptions:
  center: false
  transition: slide
---
<!-- .slide: class="center" -->

# GoDev

#### What I learnt from writing a live-reload development tool in Go for fun and profit

<!-- - -->
<!-- .slide: class="profile" -->

<table>
  <tr>
    <td>
      ![./assets/img/profile.jpg](./assets/img/profile.jpg)
    </td>
    <td data-markdown>
      <h3>
        Joseph is a...
      </h3>
      <ul>
        <li>
          DevOps Evangelist
        </li>
        <li>
          MyCareersFuture Team Member
        </li>
        <li>
          Gopher for 6 months
        </li>
        <li>
          Writer ([medium.com/@joeir](https://medium.com/@joeir))
        </li>
        <li>
          Developer ([github.com/zephinzer](https://github.com/zephinzer))
        </li>
      </ul>
    </td>
  </tr>
</table>

<!-- - -->

## TL;DR

- Yet Another Tool?
- What's Already Out There
- Short Demo
- Code Design & Architecture
- What I Learnt


<!-- / -->
<!-- .slide: class="center" -->

## Yet Another Tool?

<!-- - -->
<!-- .slide: class="left center" -->

### Why another tool

- ~5 minutes to bootstrap a new Go project

- Cumbersome dependency retrieval (`go get`)

- No live-reload tool that worked with Go Modules

- No test-watching tool with sufficient logging

- **An excuse to write something in Go**

<!-- - -->
<!-- .slide: class="left center" -->

### What I Created

- Project bootstrapper

- Automatic dependency retrieval

- Live-reload functionality

- Test-watching functionality

- **A Go CLI tool**

<!-- / -->
<!-- .slide: class="center" -->

## Short Demo

<!-- - -->

### [getgo.dev](https://getgo.dev)
- Install: `go get -v github.com/zephinzer/godev`
- `godev init`
  - Initialises a new Go project
- `godev`
  - Starts the application in live-reload mode
- `godev test`
  - Starts the tests in live-reload mode
- `godev --exec 'go run .'`
  - Ad-hoc runs a Go program


<!-- / -->
<!-- .slide: class="center" -->

## What's Already Out There?

<!-- - -->
<!-- .slide: class="left" -->

### Air
> [github.com/cosmtrek/air](https://github.com/cosmtrek/air)

- - -

Relies on Fresh

Not `go get`table

```sh
$ go get github.com/cosmtrek/air
```

```wrap
> package github.com/cosmtrek/air: no Go files in /home/zephinzer/.gvm/pkgsets/go1.11/global/src/github.com/cosmtrek/air
```

<!-- - -->
<!-- .slide: class="left" -->

### Gin
> [github.com/codegangsta/gin](https://github.com/codegangsta/gin)

- - -

Too slow

Really bloated

Has the next tool as a dependency...


<!-- - -->
<!-- .slide: class="left" -->

### Realize
> [github.com/oxequa/realize](https://github.com/oxequa/realize)

- - -

Broke when using `go.mod`

<!-- - -->
<!-- .slide: class="left" -->

### GoConvey
> Link FYI: [github.com/smartystreets/goconvey](https://github.com/smartystreets/goconvey)

- - -

Requires a web interface for logs

CLI usage lacks live-reload of tests


<!-- - -->
<!-- .slide: class="left" -->

### GoDev Makefile
> [github.com/zephinzer/godev](https://github.com/zephinzer/godev/tree/master/scripts)

- - -

1. Go to website
2. Copy Makefile
3. Open directory
4. Paste Makefile
5. Save
6. `make init`


<!-- / -->
<!-- .slide: class="center" -->

## Code Design & Architecture


<!-- - -->
<!-- .slide: class="center" -->

### TL;DR
- Configuration Management
- Logs Management
- Filesystem Watcher
- Pipeline Executor

<!-- - -->
<!-- .slide: class="left" -->

### Configuration Management

- - -

Library: [github.com/urfave/cli](https://github.com/urfave/cli)

- - -

Manage sub-commands
- eg. `godev test`

Manage flags
- eg. `godev --exec 'go run .'`

<!-- - -->
<!-- .slide: class="left" -->

### Logs Management

- - -

Library: [github.com/sirupsen/logrus](https://github.com/sirupsen/logrus)

- - -

Enable various log levels
- Trace - *very verbose*
- Debug - *verbose*
- Info - *standard*
- Warn - *not used*
- Error - *silent*

<!-- - -->
<!-- .slide: class="left" -->

### Filesystem Watcher

- - -

Library: [github.com/fsnotify/fsnotify](https://github.com/fsnotify/fsnotify)

- - -

Watches for file system changes
- Create
- Remove
- Write
- Rename
- Permissions

<!-- - -->
<!-- .slide: class="left" -->

### Pipeline Executor

Executes groups of commands

Execution groups
- Runs sequentially
- Runs a set of commands to run in parallel

Commands
- Atomic script
- Encapsulates a shell command

<!-- / -->
<!-- .slide: class="center" -->

## What I Learnt

<!-- - -->
<!-- .slide: class="center" -->

### TL;DR
- Go has some neat language semantics
- Dependency management in Go
- Versioning in Go
- Concurrency is difficult
- Filesystem notifications are iffy

<!-- - -->
<!-- .slide: class="left" -->
### Go has some neat language semantics

- Really concise language specification
  - 25 reserved keywords only
  - 10 inbuilt functions only
- Highly standardised code styles
- Interfaces for <sup>composition</sup>/<sub>inheritance</sub>
- Testing is part of the standard library

<!-- - -->
<!-- .slide: class="left" -->
### Dependency management in Go

- **Previously**: GoDep, Dep, Glide, *etc*
- **Now**: Go Modules (since Go 1.11)
- Simply run `go mod vendor`

<!-- - -->
<!-- .slide: class="left" -->
### Versioning in Go

- Complex stuff
- via `-ldflags` build-time arguments (for binaries)
- via code as variables (for `go get` purposes)
- via repository Git tags (for packages meant for use in other packages)

<!-- - -->
<!-- .slide: class="left" -->
### Concurrency is difficult

- Goroutines
- Channels
- Memory leaks

<!-- - -->
<!-- .slide: class="left" -->
### Filesystem notifications are iffy

- IDEs save files twice for some reason
- Filesystem signals are created for bitmasking
- Requires batching for ease of use

<!-- / -->
<!-- .slide: class="center" -->

## That's all folks

- - -

Convinced? Get it at:

[github.com/zephinzer/godev](https://github.com/zephinzer/godev)
