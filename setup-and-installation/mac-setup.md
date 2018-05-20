# Mac Setup

Setting up for Mac OS X is pretty simple. In this guide, we will install Python3.6 and Node.js on your computer via the command line.

#### Installing HomeBrew

First off, install HomeBrew, a savvy package manager for Mac. It saves lives.

```text
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Next, we need to insert the Homebrew Directory at the top of your `PATH`. Thus, go to `~/.profile` and open it with your favorite text editor. Create the file if you don't have one and at the end of the file put in:

```text
export PATH=/usr/local/bin:/usr/local/sbin:$PATH
```

#### Installing Python3

Install and link python3 and pip3 \(pip3 comes with python3\)

```text
$ brew install python3
$ brew link python3
```

Then, install Pipenv:

```text
$ brew install pipenv
```

#### Installing Node.js

```text
$ brew install node
$ brew update
$ brew upgrade node
```

The full article is [here](http://blog.teamtreehouse.com/install-node-js-npm-mac)

Next, check the version of node

```text
$ node -v
```

It should output a version 8 and higher.

