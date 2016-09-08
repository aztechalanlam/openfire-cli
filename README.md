# OpenFire cli

Some simple command line utilities for [OpenFire](https://www.igniterealtime.org/projects/openfire/) unix server

## About

This scripts provide:
* simple start/stop/restart/status interface
* check if user exist/add/delete user interface
    * only if [REST API plugin](https://www.igniterealtime.org/projects/openfire/plugins/restapi/readme.html) installed
    
## Installation

* you will need [jq](https://stedolan.github.io/jq/)
    * `sudo apt-get install jq`
* if you want check/add/delete users you will need
    * [REST API plugin](https://www.igniterealtime.org/projects/openfire/plugins.jsp)
    * also enable it in `admin panel->server->server settings->REST API` and set AUTH type to `Secret key auth`
* cd to e.g. `/usr/src/`
* clone this repo
    * `git clone https://github.com/lgg/openfire-cli && cd openfire-cli`
* edit `of-cli-uapi`
    * change apiKey for your REST API AUTH key
    * change apiPort if needed
    * change apiHost if needed
* copy scripts to `/usr/sbin/`
    * `sudo cp ./of-cli /usr/sbin/ && sudo cp ./of-cli-uapi /usr/sbin/`
* add execution rights
    * `sudo chmod +x /usr/sbin/of-cli && sudo chmod +x /usr/sbin/of-cli-uapi`
* enjoy
    
## Usage

* `of-cli status`
    * commands: start/status/stop/restart/force-reload
* `of-cli-uapi get admin`
    * usage: `of-cli-uapi ACTION USERNAME PASSWORD`
    * actions: get/add/delete

## of-cli-uapi

### get user

* `of-cli-uapi get USERNAME`
    * e.g. `of-cli-uapi get admin`
* if user exists return `true`, if not exist, return `false`

### add user

* `of-cli-uapi add USERNAME PASS`
    * e.g. `of-cli-uapi add bobby sup3rs3cur3pass`
* create user with provided credentials

### delete user

* `of-cli-uapi delete USERNAME`
    * e.g. `of-cli-uapi delete bobby`
* delete user with provided username

## ToDo

* add #"email":"$" to reg data
* add header response code checks
* add check for right api key

## License

* 2016, lgg
* MIT