---
title: vscode remote
layout: post
categories: vscode
date:   2020-12-10 8:06:16 +0800
tags: vscode
excerpt: vscode remote
---
--------------------
文章出自个人博客<https://applelin8.github.io/2020/12/10/vscode-remote>，转载请申明

------------------


# content <span id="home">

* [how to use vscode](#1)
* [extension](#2)
* [gdb](#3)
* [shell](#4)

  
----------------------------
# how to use vscode <span id="1">

how to use vscode
![how to use vscode](https://AppleLin8.github.io/assets/img/blog/vscode/vscode_extension.png)

remote-ssh
![architecture](https://AppleLin8.github.io/assets/img/blog/vscode/remote_ssh.png)


C/C++ IntelliSense, debugging, and code browsing.
![architecture](https://AppleLin8.github.io/assets/img/blog/vscode/remote-ssh_c_cpp_intellisense.png)

# extension <span id="2">

![architecture](https://AppleLin8.github.io/assets/img/blog/vscode/extension.png)

# gdb <span id="3">

![architecture](https://AppleLin8.github.io/assets/img/blog/vscode/gdb.png)

${workspace}/.vscode/launch.json

```bash
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "gcc - 生成和调试活动文件",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}",
            "args": [ "ls"],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: gcc build active file",
            "miDebuggerPath": "/usr/bin/gdb"
        }
    ]
}
```

${workspace}/.vscode/tasks.json

```bash
{
    "tasks": [
        {
            "type": "shell",
            "label": "C/C++: gcc build active file",
            "command": "/usr/bin/gcc",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "options": {
                "cwd": "${workspaceFolder}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ],
    "version": "2.0.0"
}
```



# shell <span id="4">

![architecture](https://AppleLin8.github.io/assets/img/blog/vscode/log_sh.png)