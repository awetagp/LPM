
LPM package manager <!-- omit in toc -->
====

- [1. Introduction](#1-introduction)
- [2. Install](#2-install)
- [3. Setup repositories](#3-setup-repositories)
- [4. Usage of the lpm command](#4-usage-of-the-lpm-command)
- [5. Creating new package](#5-creating-new-package)
- [6. Upload new/update packages:](#6-upload-newupdate-packages)
- [7. Backgrounder](#7-backgrounder)


# 1. Introduction

[LPM](https://loupeteam.github.io/LoupeDocs/) is original the B&R Automation Studio package manager for Loupe ecosystem.


The AWETA version of LPM has the following changes to the orginal version:
* Distributed as executalable instead of python code.
* Allow use of own package repositories (called registries with npm)


# 2. Install

Make sure you already have `nodejs` installed with our package manager or downloaded from https://nodejs.org.

Next install the lpm by using the supplied installer downloaded from the releases area.

The `lpm` tools is added to to path, but can requires restarting tooling after installation.


# 3. Setup repositories

Below two repositories are setup:
* @loupeteam which points to the orginal loupe packages
* @aweta which points to an example repository at our own internal ProGet server

Create a file `.nmprc` in `C:\users\<username>`.
Set the content to:
```
@loupeteam:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=your_very_secret_key

@youronwscope:registry=http://yourreposhost/yourepopath
```

# 4. Usage of the lpm command 
You can find documentation here:
https://loupeteam.github.io/LoupeDocs/tools/lpm.html

The login command for loupe is not required (because the token is already set in the repo config).
The AWETA test repo does not require an login for download

When manupuliating package you need to indicate the correct repo, two ways to do that:
* Provide an additional scope argument to lpm
```
lpm install --scope=@aweta foobar
```
* Or just use the scope prefix with the package name
```
lpm install @aweta/foobar
```

# 5. Creating new package

Best illustrated by an example.
Requires an project initialized with lpm.

```
lpm install --scope=@youronwscope foobar
```

Study the youronwscope/foobar library and the package.json file in the library directory.
You can repack the library by:

```
cd Logical/Libraries/Aweta/foobar
npm pack
```

A `.tgz` is created that can be uploaded to a repository.

# 6. Upload new/update packages:

You can use the common npm commands for uploading or use the web interface of your repo to upload it by hand.


# 7. Backgrounder
The `lpm` command is a thin python wrapper arround the javascript package management system `npm`.
The package configuration is stored in the root of the AR project in the file package.json.

Most npm commands also work with lpm command.
