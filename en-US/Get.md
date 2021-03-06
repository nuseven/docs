Command get
===========

Help information: `gopm get -h` or `gopm help get`:

```
NAME:
   get - fetch remote package(s) and dependencies

USAGE:
   command get [command options] [arguments...]

DESCRIPTION:
   Command get fetches a package or packages,
and any package that it or they depend(s) on.
If the package has a gopmfile, the fetch process will be driven by that.

gopm get
gopm get <import path>@[<tag|commit|branch>:<value>]
gopm get <package name>@[<tag|commit|branch>:<value>]

Can specify one or more: gopm get cli@tag:v1.2.0 github.com/Unknwon/macaron

If no version specified and package exists in GOPATH,
it will be skipped, unless user enabled '--remote, -r' option
then all the packages go into gopm local repository.

OPTIONS:
   --tags 			apply build tags
   --download, -d	download given package only
   --update, -u		update package(s) and dependencies if any
   --local, -l		download all packages to local GOPATH
   --gopath, -g		download all packages to GOPATH
   --remote, -r		download all packages to gopm local repository
   --verbose, -v	show process details
```
   
### `gopm get`

- Feature: Fetch remote package(s) and dependencies to local repository according to gopmfile.
- Detail: No argument means get dependencies for project that is in work directory, if a gopmfile is supplied, then will get based on the information from gopmfile.
- Example: `gopm get`.

#### Usage example

##### `gopm get`

Suppose your work directory is in the project of gopm(`github.com/gpmgo/gopm`):

	$ pwd
	
Output: 

	$GOPATH/src/github.com/gpmgo/gopm

And there is a gopmfile:

	$ cat .gopmfile
	
Output:

```
[target]
path = github.com/gpmgo/gopm

[deps]
github.com/Unknwon/com =
github.com/Unknwon/goconfig =
github.com/aybabtme/color =
github.com/codegangsta/cli =
github.com/Unknwon/cae =
```
	
So the command will downloads 4 packages(into gopm local repository `~/.gopm/repos`) in `deps` section if there do not exist in your `$GOPATH`.

Suppose you need to download them all into your `$GOPATH` so you may able to make some changes and then compile gopm. Use option `--gopath, -g` to achieve that.

However, in case you want to keep your `$GOPATH` clean and download all of them into gopm local repository. Use option `--remote, -r` to achieve that.

### `gopm get <import path>@[<tag|commit|branch>:<value>]`

- Feature: Fetch remote package(s) and dependencies to local repository according to specified version.
- Detail: This command can accept one or more import paths with/without specified version.
- Example:
	- Latest version: `gopm get github.com/go-xorm/xorm`.
	- Certain branch: `gopm get github.com/go-xorm/xorm@branch:master`.
	- Specified tag: `gopm get github.com/go-xorm/xorm@tag:v0.2.3`.
	- Fixed commit: `gopm get github.com/go-xorm/xorm@commit:6ffffe9`.

#### Usage example

##### Latest version: `gopm get github.com/go-xorm/xorm`

This downloads the latest version of xorm, and its dependencies according to its gopmfile.

##### Certain branch: `gopm get github.com/go-xorm/xorm@branch:master`

This downloads the latest version of xorm in master branch, and its dependencies according to its gopmfile.

##### Specified tag: `gopm get github.com/go-xorm/xorm@tag:v0.2.3`

This downloads the version of xorm in `tag:v0.2.3`, and its dependencies according to its gopmfile.

##### Fixed commit: `gopm get github.com/go-xorm/xorm@commit:6ffffe9`

This downloads the version of xorm in `commit:6ffffe9`, and its dependencies according to its gopmfile.
	
### `gopm get <package name>@[<tag|commit|branch>:<value>]`

- Feature: Fetch remote package(s) and dependencies to local repository according to specified version; but instead of using full import path, use project name.
- Detail: It's basically a short-cut for package import path.
- Example:
	- Latest version: `gopm get xorm`.
	- Certain branch: `gopm get xorm@branch:master`.
	- Specified tag: `gopm get xorm@tag:v0.2.3`.
	- Fixed commit: `gopm get xorm@commit:6ffffe9`.
	
See [well-known Go projects list](../pkgname.list) for details.

## Options

- `--tags`: apply build tags.
- `--download, -d`: download given package only.
- `--update, -u`: update package(s) and dependencies if any.
- `--gopath, -g	`: download all packages to GOPATH.
- `--remote, -r`: download all packages to gopm local repository.
- `--verbose, -v`: show process details.
