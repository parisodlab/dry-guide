
[TOC]

## Overview

This guide will walk you through how to connect to a remote server using Visual Studio Code (VScode). This is useful if you want to edit files on a remote server without having to use a terminal or a text editor like `vim` or `nano`. You can also setup keybindings to run code on the remote server, which is useful to document your code while you are creating and testing it.

## Steps

### 1. Install the Remote - SSH extension

1. Open VScode
2. Click on the Extensions icon on the left-hand side of the window
3. Search for `Remote - SSH` in the search bar
4. Click on the green `Install` button

### 2. Connect to the remote server

1. Click on the `Remote Explorer` icon on the left-hand side of the window (it looks like a little monitor)
2. Click on the `+` icon at the top of the window
3. Enter the username and IP address/server id of the server you want to connect to (e.g. `username@ip_address`, e.g. `<user_id>@login8.hpc.binf.unibe.ch` -IBU or `<user_id>@biolpc045604` - p910)
4. Select the SSH configuration file you want to use and update (e.g. `~/.ssh/config`)
5. Once you receive Host added message, click `Connect`, you will be prompted to enter your password
6. Once connected you need to open a folder on the remote server. Click on the `Open Folder` button and select the folder you want to open. You will be prompted to enter your password again.
7. You can now Open a terminal on the remote server by clicking on the `Terminal` menu and selecting `New Terminal`. Now you can run commands on the remote server, while saving and editing files (e.g. README.md) in VScode.

### 3. Set keybindings to run code on the remote server





