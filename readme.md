# Commited Git Files [![Build Status](https://travis-ci.org/clakech/commited-git-files.svg?branch=master)](https://travis-ci.org/clakech/commited-git-files)

This module returns an array of commited files diff from a source branch and current HEAD and their status acording to git.

## Usage

**Download**

`npm install commited-git-files`

**In Code**

```
var cgf = require("commited-git-files");
cgf(function(err, results){
	//WHAT EVER YOU SO PLEASE
});
```

**Example Results**

```
[
	{
		"filename": "package.json",
		"status": "Added"
	},
	{
		"filename": "readme.md",
		"status": "Modified"
	},
	{
		"filename": "index.js",
		"status": "Renamed"
	}
]
```

## API

### cgf(source, filter, callback)

Get a list of commited git files

* source: string of git source branch: origin/master
* filter: string of git status codes. No spaces
* callback:
	* err: the error
	* results: file object array.

### cgf.getSourceId(source, callback)

Get commit id that will be used in the diff to ID which files are commited diff.

* source: string of git source branch: origin/master
* callback
	* err: the error
	* head: the git commit id of the branch

### cgf.readFile(filename, [options], callback)

This is a proxy for [fs.readFile](http://nodejs.org/api/fs.html#fs_fs_readfile_filename_options_callback) with one change. The filename will be relative to the `cgf.cwd`

### cgf.debug

Boolean that flips logging on and off. By default this is false. If true, all git commands will be console logged.

### cgf.includeContent

If true, include content will add a `content` or `err` param to the file object.

* Default Value: false
* Content Param: the content of the file 
* Err Param: the error message received while trying to read the file.

### cgf.cwd

The current working directory. AKA: where the .git folder you care about is.

# Default Value: is equal to process.cwd() of your app.g

## Statuses

**cgf-Status (git status code)**

* Added (A)
* Copied (C)
* Deleted (D)
* Modified (M)
* Renamed (R)
* Type-Change (T) [i.e. regular file, symlink, submodule, etc.]
* Unmerged (U)
* Unknown (X)

## Change Log

### 0.0.1

* implements mvm (minimum viable module) to diff commited files form a source branch
* forked from https://github.com/mcwhittemore/staged-git-files