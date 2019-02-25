# OpenFire cli

Some simple command line utilities for [OpenFire](https://www.igniterealtime.org/projects/openfire/) unix server

## About

This scripts provide:
* simple `start/stop/restart/status` command line interface
* `list registered users/check if user exist/add/delete` command line interface
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
    * usage: `of-cli-uapi ACTION USERNAME (PASSWORD|GROUP|NAME)`
    * actions: list/get/add/delete/update/addtogroup/deletefromgroup

## of-cli-uapi

### list users

* `of-cli-uapi list`
* lists all registered users

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

### add user to group

* `of-cli-uapi addtogroup USERNAME GROUP`
   * e.g. `of-cli-uapi addtogroup bobby thisgroup`
* add user to group (maybe shared group). If group is 'shared', this user appears in other users rosters.
  If GROUP is not exist, it will be created. If user was member of other group already, this GROUP is added to user groups list.

### delete user from group

* `of-cli-uapi deletefromgroup USERNAME GROUP`
   * e.g. `of-cli-uapi deletefromgroup bobby thisgroup`
* delete user from group. This action is reverse to 'addtogroup', it can be used when it was added to some group by mistake
   or when it is necessary to delete user from shared roster.

### update user name

* `of-cli-uapi update USERNAME NAME`
   * e.g. `of-cli-uapi update bobby McFarrell`
* update user 'name' property. This property used by clients to show 'real user name' in roster instead his/her login (username).
  For example, it can be surname, nick or similar.


## ToDo

* add #"email":"$" to reg data
* add header response code checks
* add check for right api key

## License

* 2016, lgg
* MIT