# gh-list

Collection of scripts to export GitHub data into CSV

* org repos
* PRs and PR Comments 
* Issues and Issues Comments


## Prerequisites 

* [Personal GitHub access token](https://github.com/settings/tokens) 
* [jq command-line](https://stedolan.github.io/jq/)

## Setup

Exporting your GitHub token as environment variables

```shell
export GITHUB_ACCESS_TOKEN="your-token-here"
```

## Export

### Org Repos 

```shell
bin/repos [org_name]
```

The output will be a CSV file (org_name.csv) in the directory where you executed the above command containing: 

* name - name of the repo 
* org - organization name
* url - fully qualified URL of the repo in GitHub
* home - homepage from repo settings
* lang - language from repo settings 
* license - the type of of license used in the repo (e.g. apache-2.0)
* update - last update date (yyy-MM-dd)
* desc - repo description from settings 

### PRs

### PR Comments 

### Issues 

### Issue Comments 


## Disclaimer

This is my personal project and it does not represent my employer. I take no responsibility for issues caused by this code. I do my best to ensure that everything wor
