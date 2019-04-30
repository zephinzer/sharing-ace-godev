---
title: GoDev
separator: <!-- // -->
verticalSeparator: <!-- / -->
theme: night
revealOptions:
  center: false
  transition: slide
---
<!-- .slide: class="center" -->

# GoDev

#### Lessons from writing a live-reload development tool in Go for fun and profit

<!-- / -->
<!-- .slide: class="center profile" -->

<table>
  <tr>
    <td>
      ![./assets/img/profile.jpg](./assets/img/profile.jpg)
    </td>
    <td data-markdown>
      <h3>
        Who's this fella and what's he trying to sell me?
      </h3>
      <ul>
        <li>
          Joseph Matthias Goh
        </li>
        <li>
          DevOps Engineer, MyCareersFuture
        </li>
        <li>
          Agile Consulting & Engineering
        </li>
        <li>
          Gopher for 6 months
        </li>
        <li>
          Writes at: https://medium.com/@joeir
        </li>
        <li>
          Codes at: https://github.com/zephinzer
        </li>
        <li>
          THAT outdated website: https://joeir.net
        </li>
      </ul>
    </td>
  </tr>
</table>


<!-- // -->
<!-- .slide: class="center" -->

# Why Need This?

<!-- / -->
<!-- .slide: class="left center" -->

- ~5 minutes to bootstrap a new Go project

- Leychey dependency retrieval (`go get`)

- Lack of live-reload tool that worked with Go Modules

- Lack of test-watching tool

- An excuse to write something in Go

<!-- // -->
<!-- .slide: class="center" -->

# Got What Else?

<!-- / -->
<!-- .slide: class="left" -->

## Air
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

<!-- / -->
<!-- .slide: class="left" -->

## Gin
> [github.com/codegangsta/gin](https://github.com/codegangsta/gin)

- - -

Too slow


<!-- / -->
<!-- .slide: class="left" -->

## Realize
> [github.com/oxequa/realize](https://github.com/oxequa/realize)

- - -

Broke when using `go.mod`

<!-- / -->
<!-- .slide: class="left" -->

## GoConvey
> Link FYI: [github.com/smartystreets/goconvey](https://github.com/smartystreets/goconvey)

- - -

Requires a web interface for logs


<!-- / -->
<!-- .slide: class="left" -->

## GoDev Makefile
> [github.com/zephinzer/godev](https://github.com/zephinzer/godev/tree/master/scripts)

- - -

1. Go to website
2. Copy Makefile
3. Open directory
4. Paste Makefile
5. Save
6. `make init`


<!-- // -->
<!-- .slide: class="center" -->

# Design & Architecture

(and other big words)


<!-- / -->
<!-- .slide: class="center" -->

#### Watcher

#### Runner

#### CLI

#### Controller

#### Logger


<!-- / -->
<!-- .slide: class="left" -->

## Watcher

Watches for file system changes
- Create
- Remove
- Write
- Rename
- Permissions

Library: [github.com/fsnotify/fsnotify](https://github.com/fsnotify/fsnotify)

<!-- / -->
<!-- .slide: class="left" -->

## Runner Module

Executes command groups
- Execution groups
- Commands

<!-- / -->
<!-- .slide: class="left" -->

## CLI

Manage sub-commands
- eg. `godev test`

Manage flags
- eg. `godev --exec 'go run .'`

<!-- / -->
<!-- .slide: class="left" -->

## Controller

Retrieves configuration from CLI

Initialises the Watcher and Runner

AKA `func main() {...}`

<!-- / -->
<!-- .slide: class="left" -->

## Logger

Enable various log levels
- Trace - *very verbose*
- Debug - *verbose*
- Info - *standard*
- Warn - *not used*
- Error - *silent*

Reduces noise

One per module for clarity


<!-- // -->
<!-- .slide: class="center" -->

# Learnings & Gotchas

<!-- / -->
<!-- .slide: class="center" -->

#### Language Semantics
#### Process Forking
#### Goroutines & Channels
#### Golang Versioning
#### IDEs Save Twice (why?)

<!-- / -->
<!-- .slide: class="left" -->

## Language Semantics

Type Inference: `:=`

Classes (somewhat): `type x struct{}`

<!-- / -->
<!-- .slide: class="left" -->

## Process Forking

<!-- / -->
<!-- .slide: class="left" -->

## Goroutines & Channels

Goroutines
- `async function b() => 'hi'`
- `await b()`

<!-- / -->

## IDEs Saves Twice

VSCode

IntelliJ Editors

`vim` doesn't do this 

<!-- // -->
<!-- .slide: class="center" -->

# Thank you

### (and any questions?)

- - -

Convinced? Get it at:

[github.com/zephinzer/godev](https://github.com/zephinzer/godev)
