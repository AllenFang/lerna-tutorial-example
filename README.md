# Lerna Tutrial Example

This repo give you an independent enviornment to play with [lerna](https://github.com/lerna/lerna). We leverage on Docker to provide you a gitserver and a lightweight npm server so that you can easy to understadn and learn how lerna publish, release and so on. 

You will have following components after setup:

* NPM server(We use [verdaccio](https://github.com/verdaccio/verdaccio))
  * `npmserver` is docker dontainer name
* GIT server(Simple git server on SSH and already contain a bare repository)
  * `gitserver` is docker dontainer name
* Workspace(Git, Node.js and NPM installed), develop/testing/deploy/publish here!!
  * `workspace` is docker dontainer name

## Setup

### Install and run
```sh
####### GENERATE SSH KEY IF YOU DON'T HAVE YET #######
$ cd ~
$ mkdir .ssh
$ ssh-keygen -t rsa
######################################################

$ git clone https://github.com/AllenFang/lerna-tutorial-example.git
$ cd lerna-tutorial-example
$ cp ~/.ssh/id_rsa.pub ./docker/git-server/keys
$ docker-compose up -d
```
After docker compose start, `gitserver` and `npmserver` will run in the background then you need to type following commands to launch to `workspace` container to do further setup: 

`docker-compose run workspace sh`

### Setup NPM

```sh
$ npm set registry http://npmserver:4873
$ npm adduser --registry http://npmserver:4873  # Keyin your username, password and email
```
Then open your browser and do login via http://localhost:4873. After login, you will see no any package published yet. So two steps you need to do as below:

### Setup GIT

```sh
$ git config --global user.email "you@example.com"  # Keyin your email
$ git config --global user.name "Your Name"  # Keyin your username
```

### Setup Dummy Project

```sh
$ git clone ssh://git@gitserver/git-server/repos/examples.git
$ cd examples
$ npm install
```

## Lerna Test

After above commands, you already setup the git and npm config in the `workspace` container then it's time that we can publish modules via `lerna`:

```sh
$ ./node_modules/.bin/lerna publish
```

After above comment, lerna will ask you auto detect what packages had changes since last publish and ask you what version you want to upgrade by a prmopt.
Following is the result screenshot:

![lerna publish result](https://i.imgur.com/NDA5INz.png)
