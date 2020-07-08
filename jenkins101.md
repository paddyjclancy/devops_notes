# Jenkins - Integration Server

- Combines all code / aspects of an app, to continuously test it.

## Build steps:

1) Dev updates / changes code
	- Code --> Version Control --> repo
2) Code delivered to build server
	- Jenkins detects chenge, sends to server
3) Builds app
	- Builds new version of app using build-script (.sh file)
4) Testing
	- Using test script
	- Either unit or integrated
5) Return problems
	- Either in UI or as email



## Jenkins Pipeline Set-up

How to add a repo to a pipeline, in a Jenkins Server

1) Enter Jenkins server
2) `New Item`
	- Enter name and type (freestyle project)
3) `Discard old builds` 
	- Max 3
4) `GitHub project` - enter WEB url
5) `Restrict where this project can be run` - sparta-ubuntu-node
	***Disabled during set-up***
6) `Source Code Management` - Git
	- CLONE url
7) `Add key`
	- `Kind` - SSH username with private key
	- `id`, `desc` - an internal, unique name
	- `Private key` - enter directly
		- jenkins / idrsa
	- `ADD`
8) Add new key (public) to GitHub, if not there
9) GitHub Webhooks
	- `Payload URL` = http://[Public IP Jenkins server]/github-webhook/
	- `Content type` = application/json
	- Send me everything
9) `Branches to build` - `*/dev`
10) `Additional Behaviours`
	- Merge before build
	- To master
11) `Build Triggers` - GitHub Hook
12) `Execute shell`, eg:
		- `cd app`
		- `npm install`
		- `npm test`
13) `Post Build Actions`
	- Git Publisher
		- Push only if succeed
		- Merge results
		- Notes