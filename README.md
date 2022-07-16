# gh2csv

Collection of scripts to export GitHub data into CSV

* Repos in an Organization
* PRs and PR Comments for a given Repo
* Issues and Issues Comments for a given Repo

> Note, the provided PR, PR Comments, Issues, and Issue Comments export only the basic events, you can alter the fields names to include additional data needed for your use-case. 

## Prerequisites 

* [Personal GitHub access token](https://github.com/settings/tokens) 
* [jq command-line](https://stedolan.github.io/jq/)

## Setup

Exporting your GitHub token as environment variables

```shell
export GITHUB_ACCESS_TOKEN="your-token-here"
```

## Export

> Each one of the below scripts uses paging to export all of the data from the inception of that repo. Depending on the size of your repo, that may take a while. You can experiment with the starting page number in each script to start with a more recent records. 

### Org Repos 

```shell
bin/repos org_name
```

Outputs CSV file (repo-`org_name`.csv) containing: 

* `repo` - name of the repo 
* `org` - organization name
* `url` - fully qualified URL of the repo in GitHub
* `home` - homepage from repo settings
* `lang` - language from repo settings 
* `license` - the type of of license used in the repo (e.g. apache-2.0)
* `update` - last update date (yyy-MM-dd)
* `desc` - repo description from settings 

### PRs

```shell
bin/pr [org_name] [repo_name]
```

Outputs CSV file (pr-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that PR
* `repo` - name of the repo 
* `org` - organization name
* `user` - username who submitted the PR
* `event` - name of the event (e.g. `pr`)
* `time` - ISO timestamp of the event

### PR Comments 

```shell
bin/prc [org_name] [repo_name]
```

Outputs CSV file (prc-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that PR comment
* `repo` - name of the repo 
* `org` - organization name
* `user` - username who made the PR comment
* `event` - name of the event (e.g. `pr-comment`)
* `time` - ISO timestamp of the event

### Issues 

```shell
bin/issue [org_name] [repo_name]
```

Outputs CSV file (issue-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that issue
* `repo` - name of the repo 
* `org` - organization name
* `user` - username who made the issue
* `event` - name of the event (e.g. `issue`)
* `time` - ISO timestamp of the event

### Issue Comments 

```shell
bin/issuec [org_name] [repo_name]
```

Outputs CSV file (issuec-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that issue comment
* `repo` - name of the repo 
* `org` - organization name
* `user` - username who made the issue comment 
* `event` - name of the event (e.g. `issue-comment`)
* `time` - ISO timestamp of the event

## Disclaimer

This is my personal project and it does not represent my employer. I take no responsibility for issues caused by this code. I do my best to ensure that everything wor
