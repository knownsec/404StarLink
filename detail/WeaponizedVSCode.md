## WeaponizedVSCode <https://github.com/Esonhugh/WeaponizedVSCode>
<!--auto_detail_badge_begin_0b490ffb61b26b45de3ea5d7dd8a582e-->
![Language](https://img.shields.io/badge/Language-Python-blue)
![Author](https://img.shields.io/badge/Author-Esonhugh-orange)
![GitHub stars](https://img.shields.io/github/stars/Esonhugh/WeaponizedVSCode.svg?style=flat&logo=github)
![Version](https://img.shields.io/badge/Version-V0.5.0-red)
![Time](https://img.shields.io/badge/Join-20250722-green)
<!--auto_detail_badge_end_fef74f2d7ea73fcc43ff78e05b1e7451-->



## Create Hacking Environment

### USAGE

[Usage Readme](./documents/USE.md)

[Custom Readme](./documents/CUSTOM.md)

[Demo](./documents/DEMO.md)

### AIM of project (which problem this project try to solve)

Cobalt Strike has a lot of features, but it's too heavy for only host machine or boxes. But it's inspired me a lot.

So I wanna create a lightweight hacking environment for myself and providing features like following:

1. different enviroment in different hacking project - content switching

    > such as, you play #hackthebox machine and #tryhackme machine at the same time, and you have to switch the different environment for them.
    > 
    > you will cost a lot time on switching the environment, and you will forget to switch the environment sometimes although you have a note for it.

2. enviroments collections. put things about projects together. - save and clean

    > such as, you have a #hackthebox machine and you put all the tools together in a arsenal
    > 
    > Now you need craft some payload and delivery it to the target machine
    > 
    > before: you need to switch the environment to the arsenal folder , compile payloads and start a server(maybe http server or jndi server) to delivery the payload
    > 
    > that compile will make the arsenal folder dirty, and you need to clean it up before you commit it to git
    > 
    > and what you compile is useless for other projects which also need this payload
    >
    > if you want copy the payload back to the project folder, you need to find the project folder again and copy the path.
    >
    > now: you can create $PROJECT_WEB_DELIVERY for the payload and delivery it to the target machine, and you can easliy move the payload to $PROJECT_WEB_DELIVERY and delivery it to the target machine. also you save the payload for this project and you can use it again and keep the arsenal folder clean.

3. customized metaspoit rcfile for different projects

    > such as, you have a #hackthebox machine and you want create a handler fastly. when your machine is resetting and recover the reverse shell again.
    > 
    > now: you can edit the rcfile for project and use it in vscode terminal with `metasploit` mode. send trigger again and get the shell.

4. taking notes, log/save credentials, download files from remote machine and keep them tidy

    it works well with vscode. so you can use some vscode extensions and vscode features to do sth.

    like ssh with vscode or port fortwarding with vscode

    > such as, you have a #hackthebox machine and you want to save the credentials you found in the machine.
    > 
    > now: you can create a file named `cred` and save the credentials in it. `user` folder to save context with getting foothold and to user. `root` folder to save context with getting root.
    > 
    > also I recommand using Foam in extensions.json to take notes and save the notes in the project folder. you can use the notes to write the report after you get the goal. you can use double linked like [[USE]] to go to the doucment use.md.
    > 

5. fast payload generation with metasploit

    > such as, you have a #hackthebox machine and you want to craft a payload for it.
    > 
    > now: you can use vscode tasks in vscode to generate the payload fastly.
    >
    > 

6. more feature ...


### Happy hacking. ;)


<!--auto_detail_active_begin_e1c6fb434b6f0baf6912c7a1934f772b-->
## 项目相关


## 最近更新

<!--auto_detail_active_end_f9cf7911015e9913b7e691a7a5878527-->
