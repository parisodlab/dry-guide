
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
**Unix/Linux**:  
This step is useful if you want to document your code while you are creating and testing it.  
1. Click on the `File` menu and select `Preferences` -> `Keyboard Shortcuts`  
2. Search for `Terminal: Run Selected Text in Active Terminal` and click on the pen icon to add a keybinding  
3. Enter the keybinding you want to use (e.g. `Ctrl+Enter`)

**R**:

1. Create a dedicated R environment on the remote server using `conda` to install packages and run R code.
2. install.packages("languageserver") in the above R to enable code completion and syntax highlighting in VScode.
3. Install the `R` extension `REditorSupport.r` in VScode to run R code on the remote server.
4. Click on the `File` menu and select `Preferences` -> `Settings` and search for `@ext:REditorSupport.r R: Always use Active Terminal` and check the box.
5. Follow the [steps here:](https://github.com/REditorSupport/vscode-R/wiki/Installation:-Linux) to make vscode mimic RStudio.


### 4. Passwordless SSH Access in VS Code

If you want to avoid entering your password every time you connect to the remote server, you can set up passwordless SSH access. This involves generating SSH keys and configuring your local and remote machines to use them for authentication.

**1. Configure Your Local SSH Client**  

1. Open your SSH configuration file, from vscode. Go to Yiew -> Command Palette -> type `Remote-SSH: Open SSH Configuration File` and select the file you want to edit.  
   If the file doesn't exist, create it.

2. Add the following configuration for your remote server:
   ```plaintext
   Host <myhost>
     HostName <host>
     User <username>
     IdentityFile "path/to/.ssh/keys/<myhost>_rsa"
   ```
   Replace the placeholders:
   - `<host>`: The remote server's hostname or IP address.
   - `<username>`: Your username on the remote server.

**2. Generate SSH Keys**  

1. Generate a public/private key pair:
   ```bash
   ssh-keygen -q -b 2048 -P "" -f path/to/.ssh/keys/<host>_rsa -t rsa
   ```
   This creates:
   - `path/to/.ssh/keys/<host>_rsa` (private key)
   - `path/to/.ssh/keys/<host>_rsa.pub` (public key)

2. Ensure the keys are stored securely:
   ```bash
   chmod 700 path/to/.ssh
   chmod 600 path/to/.ssh/keys/<host>_rsa
   ```

**3. Copy the Public Key to the Remote Server**  

You can use any method to transfer the public key to the remote server:  

**Using `scp`**  
   ```bash
   scp path/to/.ssh/keys/<host>_rsa.pub <username>@<host>:~/
   ```


**4. Configure the Remote Server**  

1. Log in to the remote server:
   ```bash
   ssh <username>@<host>
   ```

2. Set up the public key for SSH authentication:
   ```bash
   mkdir -p ~/.ssh
   cat ~/myhost_rsa.pub >> ~/.ssh/authorized_keys
   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys
   ```

   If `authorized_keys` doesn’t exist:
   ```bash
   mv ~/myhost_rsa.pub ~/.ssh/authorized_keys
   chmod 600 ~/.ssh/authorized_keys
   ```

**5. Test SSH Connection**  

1. On your local machine, test the connection:
   ```bash
   ssh <username>@<host>
   ```
   If configured correctly, you should log in without entering a password.

**6. Set Up VS Code**  

1. Open VS Code and install the **Remote - SSH** extension from the Extensions Marketplace.

2. Open the Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`) and select:
   ```
   Remote-SSH: Connect to Host...
   ```

3. Choose the host configured in `path/to/.ssh/config`. You should connect to your server without entering a password.

**Troubleshooting**  

- **Permission Issues:** Ensure that `.ssh` and key files have the correct permissions:
   - `.ssh`: `700`
   - Private key: `600`
   - `authorized_keys`: `600`

