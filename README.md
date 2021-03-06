# gh2csv

Collection of scripts to export GitHub data into CSV

* Repos in an Organization
* PRs and PR Comments for a given Repo
* Issues and Issues Comments for a given Repo
* Contributors for a given Repo 
* Events for a given Repo 

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
bin/repo org_name
```

https://docs.github.com/en/rest/repos/repos

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

https://docs.github.com/en/rest/pulls/pulls

Outputs CSV file (pr-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that PR
* `number` - sequential number of that PR
* `state` - current state fo that PR (open, closed)
* `repo` - name of the repo 
* `org` - organization name
* `user` - username who submitted the PR
* `assignee` - username to whom this PR was assigned 
* `time` - ISO timestamp of that PR event
* `title` - PR tile at that time 
* `labels` - N-number of columns with one label per column 

The `pr` command also exports PR Reviews for each one of the PRs into CSV file (prr-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that PR review 
* `number` - number of the PR
* `state` - current state fo that PR review
* `repo` - name of the repo 
* `org` - organization name
* `user` - username who submitted the PR
* `time` - ISO timestamp of that PR review
* `association` - author association (CONTRIBUTOR, MEMBER etc) 


### PR Comments 

```shell
bin/prc [org_name] [repo_name]
```

https://docs.github.com/en/rest/pulls/comments#list-review-comments-in-a-repository

Outputs CSV file (prc-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that PR comment
* `in_reply_to_id` - numeric identifier for the PR
* `position` - order of the comment in the context of the PR
* `repo` - name of the repo 
* `org` - organization name
* `user` - username who made the PR comment
* `event` - name of the event (e.g. `pr-comment`)
* `created_at` - comment creation timestamp 
* `updated_at` - comment update timestamp

### Issues 

```shell
bin/issue [org_name] [repo_name]
```

https://docs.github.com/en/rest/issues/issues#list-repository-issues

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

https://docs.github.com/en/rest/issues/comments#list-issue-comments-for-a-repository

Outputs CSV file (issuec-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that issue comment
* `number` - number of the issues 
* `repo` - name of the repo 
* `org` - organization name
* `user` - username who made the issue comment 
* `event` - name of the event (e.g. `issue-comment`)
* `time` - ISO timestamp of the event
* `association` - comment author association (role)

### Contributors 

```shell
bin/contrib [org_name] [repo_name]
```

https://docs.github.com/en/rest/repos/repos#list-repository-contributors

Outputs CSV file (contrib-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that issue comment
* `repo` - name of the repo 
* `org` - organization name
* `user` - username who made the issue comment 
* `admin` - whether the user is a repo admin
* `num` - number of contributions to this repo made by that user

### Events 

> Note: Only events created within the past 90 days will be included in timelines.

```shell
bin/event 
[org_name] [repo_name]
```

https://docs.github.com/en/rest/activity/events

Outputs CSV file (event-`org_name`-`repo-name`.csv) containing: 

* `id` - numeric identifier for that event
* `repo` - name of the repo 
* `org` - organization name
* `user` - the actor (user) that caused that event
* `type` - the type of the event (e.g. `PushEvent`)
* `time` - ANSI timestamp of this event


## Disclaimer

This is my personal project and it does not represent my employer. I take no responsibility for issues caused by this code. I do my best to ensure that everything wor
