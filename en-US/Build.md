Command build
====

Help information: `gopm build -h` or `gopm help build`:

	NAME:
	   build - link dependencies and go build
	
	USAGE:
	   command build [command options] [arguments...]
	
	DESCRIPTION:
	   Command build links dependencies according to gopmfile,
	and execute 'go build'
	
	gopm build <go build commands>
	
	OPTIONS:
	   --verbose, -v	show process details
   
### `gopm build <go build commands>`

- Feature: Link dependencies according to gopmfile and go build.
- Detail: Downloads missing dependencies and link them then build binary for current project.
- Example: `gopm build`.

## Options

- `--verbose, -v`: show process details.