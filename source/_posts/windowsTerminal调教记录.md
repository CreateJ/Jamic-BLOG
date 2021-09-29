---
title: Windows Terminal调教记录
date: 2020-09-13 10:16:41
categories: 工具调教记录
tags:
 - 工具
 - window Terminal 
---

这个是windowTermial的setting.json文件，复制替换即可


```json
{
  "$schema": "https://aka.ms/terminal-profiles-schema",

  "defaultProfile": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",

  "copyOnSelect": false,

  "copyFormatting": false,

  "profiles": {
    "defaults": {
      "acrylicOpacity": 0.6,
      "useAcrylic": false,
      "startingDirectory": "G:\\Code"
    },
    "list": [
      {
        "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "name": "命令提示符",
        "colorScheme": "Solarized Dark",
        "commandline": "cmd.exe",
        "hidden": false,
        "backgroundImage": "C:\\Users\\王二蛋\\OneDrive\\图片\\壁纸\\windowTerminal\\Snipaste_2020-09-13_13-03-02.png",
        "backgroundImageOpacity": 0.25,
        "backgroundImageStretchMode": "fill"
      },
      {
        "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "name": "Windows PowerShell",
        "commandline": "powershell.exe",
        "hidden": false
      },
      {
        "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
        "hidden": true,
        "name": "Azure Cloud Shell",
        "source": "Windows.Terminal.Azure"
      }
    ]
  },

  "schemes": [
    {
      "name": "Campbell",
      "foreground": "#F2F2F2",
      "background": "#0C0C0C",
      "colors": [
        "#0C0C0C",
        "#C50F1F",
        "#13A10E",
        "#C19C00",
        "#0037DA",
        "#881798",
        "#3A96DD",
        "#CCCCCC",
        "#767676",
        "#E74856",
        "#16C60C",
        "#F9F1A5",
        "#3B78FF",
        "#B4009E",
        "#61D6D6",
        "#F2F2F2"
      ]
    },
    {
      "name": "Solarized Dark",
      "foreground": "#FDF6E3",
      "background": "#073642",
      "colors": [
        "#073642",
        "#D30102",
        "#859900",
        "#B58900",
        "#268BD2",
        "#D33682",
        "#2AA198",
        "#EEE8D5",
        "#002B36",
        "#CB4B16",
        "#586E75",
        "#657B83",
        "#839496",
        "#6C71C4",
        "#93A1A1",
        "#FDF6E3"
      ]
    },
    {
      "name": "Solarized Light",
      "foreground": "#073642",
      "background": "#FDF6E3",
      "colors": [
        "#073642",
        "#D30102",
        "#859900",
        "#B58900",
        "#268BD2",
        "#D33682",
        "#2AA198",
        "#EEE8D5",
        "#002B36",
        "#CB4B16",
        "#586E75",
        "#657B83",
        "#839496",
        "#6C71C4",
        "#93A1A1",
        "#FDF6E3"
      ]
    },
    {
      "name": "Ubuntu",
      "foreground": "#EEEEEC",
      "background": "#2C001E",
      "colors": [
        "#EEEEEC",
        "#16C60C",
        "#729FCF",
        "#B58900",
        "#268BD2",
        "#D33682",
        "#2AA198",
        "#EEE8D5",
        "#002B36",
        "#CB4B16",
        "#586E75",
        "#657B83",
        "#839496",
        "#6C71C4",
        "#93A1A1",
        "#FDF6E3"
      ]
    },
    {
      "name": "UbuntuLegit",
      "foreground": "#EEEEEE",
      "background": "#2C001E",
      "colors": [
        "#4E9A06",
        "#CC0000",
        "#300A24",
        "#C4A000",
        "#3465A4",
        "#75507B",
        "#06989A",
        "#D3D7CF",
        "#555753",
        "#EF2929",
        "#8AE234",
        "#FCE94F",
        "#729FCF",
        "#AD7FA8",
        "#34E2E2",
        "#EEEEEE"
      ]
    }
  ],
  "keybindings": [
    { "command": { "action": "copy", "singleLine": false }, "keys": "ctrl+c" },
    { "command": "paste", "keys": "ctrl+v" },
    { "command": "find", "keys": "ctrl+shift+f" },
    {
      "command": {
        "action": "splitPane",
        "split": "auto",
        "splitMode": "duplicate"
      },
      "keys": "alt+shift+d"
    }
  ]
}

```

