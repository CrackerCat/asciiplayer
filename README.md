
# :tv: ASCIIPlayer

[![Build Status](https://travis-ci.org/qeesung/asciiplayer.svg?branch=master)](https://travis-ci.org/qeesung/asciiplayer)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/2dba80ebf4c04687a320858c385fe7f8)](https://app.codacy.com/app/qeesung/asciiplayer?utm_source=github.com&utm_medium=referral&utm_content=qeesung/asciiplayer&utm_campaign=Badge_Grade_Dashboard)
[![Coverage Status](https://coveralls.io/repos/github/qeesung/asciiplayer/badge.svg)](https://coveralls.io/github/qeesung/asciiplayer)
[![Go Report Card](https://goreportcard.com/badge/github.com/qeesung/asciiplayer)](https://goreportcard.com/report/github.com/qeesung/asciiplayer)
[![GoDoc](https://godoc.org/github.com/qeesung/asciiplayer?status.svg)](https://godoc.org/github.com/qeesung/asciiplayer)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

```                  
                       _    ____   ____ ___ ___ ____  _        _ __   _______ ____
                      / \  / ___| / ___|_ _|_ _|  _ \| |      / \\ \ / / ____|  _ \
                     / _ \ \___ \| |    | | | || |_) | |     / _ \\ V /|  _| | |_) |
                    / ___ \ ___) | |___ | | | ||  __/| |___ / ___ \| | | |___|  _ <
                   /_/   \_\____/ \____|___|___|_|   |_____/_/   \_\_| |_____|_| \_\
```

ASCIIPlayer is a library that convert gif/video into ASCII gif/video and provide command-line tools for easy use.

## Table of contents

- [Features](#features)
- [How it workds](#how-it-works)
- [CLI usage](#cli-usage)
    - [Command Play](#command-play)
    - [Command Encode](#command-encode)
    - [Command Server](#command-server)
- [Library usage](#library-usage)
- [Examples](#examples)

## Features

## How it works?

```
                 +---------------+                                                  +---------+
                 |               |                                                  |         |
          +------> Gif Decoder   |                                              +---> Encoder +---> file
          |      |               |                                              |   |         |
          |      +---------------+                                              |   +---------+
          |      +---------------+                 +-------------+              |   +---------+
          |      |               |                 |             |              |   |         |
Input File+------> Image Decoder +---> Frames +--->+ Image2ASCII +->ASCII Image+----> Player  +---> stdout
          |      |               |                 |             |              |   |         |
          |      +---------------+                 +-------------+              |   +---------+
          |      +---------------+                                              |   +---------+
          |      |               |                                              |   |         |
          +------> Video Decoder |                                              +---> Server  +---> socket
                 |               |                                                  |         |
                 +---------------+                                                  +---------+
```

## Installation

```bash
go get -u github.com/qeesung/asciiplayer
```

## CLI usage

```
    _    ____   ____ ___ ___ ____  _        _ __   _______ ____
   / \  / ___| / ___|_ _|_ _|  _ \| |      / \\ \ / / ____|  _ \
  / _ \ \___ \| |    | | | || |_) | |     / _ \\ V /|  _| | |_) |
 / ___ \ ___) | |___ | | | ||  __/| |___ / ___ \| | | |___|  _ <
/_/   \_\____/ \____|___|___|_|   |_____/_/   \_\_| |_____|_| \_\
>>>Version  : 1.0.0
>>>Author   : qeesung
>>>HomePage : https://github.com/qeesung/asciiplayer

asciiplayer is a library that can convert gif and video to ASCII image
and provide the cli for easy use.

Usage:
  asciiplayer [command]

Available Commands:
  encode      Encode gif or video to ascii gif or video
  help        Help about any command
  play        Play the gif and video in ASCII mode
  server      Server command setup a server
  version     Show the version

Flags:
  -D, --debug   Switch log level to DEBUG mode
  -h, --help    help for asciiplayer

Use "asciiplayer [command] --help" for more information about a command.
```

### Command play

Play command only work in terminal, decoding the gif or video info multi frames and convert the frames to ASCII character matrix, finally, output the matrix to stdout at a certain frequency.

More detail please run `asciiplayer play --help`

#### Play examples

Play the gif， and be able to match the screen size.
```bash
asciiplayer play demo.gif
```

Zoom to the original 1/10 and play it.
```bash
asciiplayer play demo.gif -r 0.1
```

Zoom to the fixed width and fixed height and play it
```bash
asciiplayer play demo.gif -w 100 -h 40
```

Play the png image
```
asciiplayer play demo.png
```

### Command encode

Encode command can convert gif or video to a ascii gif or video.

More detail please run `asciiplayer encode --help`

#### Encode examples

Encode gif image to ascii gif image 
```bash
asciiplayer encode demo.gif -o output.gif
```

Encode gif image to ascii gif image with custom font size
```bash
asciiplayer encode demo.gif -o output.gif --font_size=5
```

Zoom to the original 1/10, then encode gif image to ascii gif image
```bash
asciiplayer encode demo.gif -o output.gif -r 0.1
```

Encode jpeg image to ascii png image
```bash
asciiplayer encode demo.jpeg -o output.png
```

### Command server

Setup a http server, and share your ascii image with others. Setup a http server, then access through curl command.

Setup server
```bash
$ asciiplayer server demo.gif
# Server available on : http://0.0.0.0:8080
```

Access from remote
```bash
$ curl http://hostname:8080
# play ascii image here
```

#### Server examples

Setup a http server with default port and host
```bash
asciiplayer server demo.gif
```

Setup a http server with the custom port
```bash
asciiplayer server demo.gif --port 8888
```

Setup a http server and share the ascii png image
```bash
asciiplayer server demo.png
```

## Library usage

Please access the godoc https://godoc.org/github.com/qeesung/asciiplayer

## Examples
