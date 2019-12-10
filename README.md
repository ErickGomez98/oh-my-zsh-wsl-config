# Oh my ZSH on WSL configuration steps

![6ed0e46205e82b90129b8f9fbe7f3aa7](https://user-images.githubusercontent.com/20981122/70483882-93d48980-1aaf-11ea-8475-a19414c33f6e.jpg)

This is a step by step guide to set zsh to be your default shell in windows using WSL.

## WSL
First of all, you would need to install WSL in your system if you don't have it already, in order to do so, you could follow one of these two tutorials:
 - [Install WSL through Microsoft Store](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
 - [Install WSL without Microsoft Store](https://docs.microsoft.com/en-us/windows/wsl/install-manual)
 (_If you are going to install it manually, just make sure you **install ubuntu 18.04**_)

Once your WSL is installed, you have to update all of your ubuntu packages running the following command in your ubuntu bash:
`sudo apt update && sudo apt upgrade`

Once you have followed the previous instructions, you are all ready to go to the next step
## Zsh
- Now you need to install zsh with the following command: `sudo apt-get install zsh`
- It will ask you if you want to set zsh as default, select yes
- Once it is installed, you have to open your bash_profile: `vim ~/.bashrc`
  - You have to set your zsh as default, so at the top of the file, write `bash -c zsh`, leaving the top of the `~/.bashrc` file like this:
  ``` bash
  bash -c zsh
  # ~/.bashrc: executed by bash(1) for non-login shells.
  # see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
  # for examples

  # If not running interactively, don't do anything
  case $- in
   \*i\*) ;;
   \*) return;;
  esac
  
  ...
  ```
  
### Zsh plugins
You can check all the available plugins for zsh [here](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins) but I'm going to provide you a few plugins that I use that are really useful, the names of the plugins are self descriptive so there's no need to tell you what each plugin does. Installing plugins it's pretty easy, all you have to do is edit the `plugins=()` line inside the  `~/.zshrc` file. The plugins that I use are the following ones.
```bash
plugins=(git colored-man-pages colorize cp node npm compleat copyfile django docker pip python vscode zsh-autosuggestions zsh-syntax-highlighting)
```
The last two plugins `zsh-autosuggestions zsh-syntax-highlighting` need an extra step to install, but belive me, they are extra worth it. In order to install those plugins, run the next commands:

Download zsh-autosuggestions by
```bash
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

Download zsh-highlighting by
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

Reopen your terminal, and now you can use all of the plugins you installed.


## Oh my Zsh
In order to install Oh My ZSH you have to run this command.
```bash 
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
Now that oh my zsh is installed, we now have to configure it in order to make it look nice, so we are going to install a theme called PowerLevel9k, so run this command:
```bash
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```
Then, you have to set this as your theme in your  `~/.zshrc` file by adding this line
```bash
ZSH_THEME="powerlevel9k/powerlevel9k"
```

Now in order to see your changes that you have made, you have to run this command.
```bash
source ~/.zshrc
```

## Fluent Terminal
Before you install fluent terminal, I recommend you that you first install the powerlie fonts in windows, those are fonts that will allow you to make your terminal look even better using some really nice icons, so follow the next instructions in order to install the powerline fonts.
1. Go to the [Powerline Fonts Github page](https://github.com/powerline/fonts).
2. Click on the green “Clone or download” button.
3. Click “Download ZIP”
4. Save the file `fonts-master.zip` to your Downloads folder or wherever you want to put it.
5. Extract fonts-master.zip.
6. Go into the `fonts-master` folder and the other `fonts-master` folder inside that. Rather than opening each folder and trying to install each font file ending with `.ttf` or `.otf` with the Windows Font Viewer, we will use a PowerShell batch script (`.ps1`) called `install.ps1.` But a few things need to be done to make it work.
7. You need to open PowerShell as an Administrator ( `Window Key + X` then select “Windows PowerShell (Admin)”. Click “Yes” when the User Access Control (UAC) prompt shows up. Because PowerShell started with the Administrator user rather than the regular user (you), PowerShell starts up in `C:\WINDOWS\system32` instead of `C:\Users\${env:UserName}`, you will need to navigate to the `fonts-master` folder in the Downloads folder. You can do this by typing `cd ${HOME}\Downloads\fonts-master\fonts-master`.
8. Next we need to tell the Execution Policy to stand down. If you don’t do this, the script won’t be allowed to run. This isn’t the same as what Linux does where the script is given execution privileges. Rather it is the inverse. The Execution Policy is a blanket approach to preventing scripts from executing. We will need to set to Execution Policy to `Bypass`, so that we may run this script. If you entered something else, you can reset the execution policy to `Restricted` later. So type `Set-ExecutionPolicy Bypass`. You will likely be warned you are changing the Execution Policy, type `y` for Yes then enter.
9. Now we can run the install.ps1 file! Type `.\install.ps1` If you are Installing a newer version, you will likely be prompted for every font that is replaced. (I should look into that.) Otherwise new fonts will be installed.
10. Just to be sure, reset the Execution Policy back to the Default setting. `Set-ExecutionPolicy Default` then type `y` for Yes like before.

### Instal Fluent Terminal
Now that you have installed the fonts, you can install Fluent Terminal, you can follow two simple steps that are described [here](https://github.com/felixse/FluentTerminal#chocolatey-package-manager-installation) in the Fluent Terminal repository.

1. Install Chocolatey
2. From an elevated/admin shell, execute `choco install fluent-terminal`

Now, you have to set WSL zsh as the default terminal in fluent terminal, you can do that in the fluent terminal's settings 
![1_jnK7gA02cVdPkpM4VsPIwQ](https://user-images.githubusercontent.com/20981122/70488203-9047ff00-1abd-11ea-9963-ef1f4f86f286.png)



## Extras
If you have followed all the steps in this guide, you will now have a very nice looking terminal that's actually fully functional, you can follow the next steps if you are interested in things like how to install python, nodejs and docker.

## Nodejs
If you want to install nodejs in your WSL, I highly recommend you to use nvm which is used to install and manage different nodejs versions in your environment, so you can follow the next steps to install nodejs.
First of all, we need to install some basic build tool for [node-gyp](https://github.com/nodejs/node-gyp) - node binaries build tool.
```bash
sudo apt-get install build-essential
```

Most of the times that I tried to install nvm I had a lot of problems until I found out that I had to export an environment variable before installing nvm, so run the following command.
```bash
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Install nvm running this command.
```bash
# This command install version 0.35.1, check the NVM reference it there are newer versions. 
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
```

Restart your terminal after the installation to make sure `nvm` command works correctly.

Now you can install the latest nodejs version using the following command:
```bash
nvm install --lts
```

## Python
Python is actually really easy to install, you just have to run this command and you are all set.
```bash
sudo apt install python3 python3-pip ipython3
```

## Docker
Docker is actually just a bit complicated, but you can get over it quickly if you copy and paste the following commands
1. Install packages to allow apt to use a repository over HTTPS
```bash
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```

2. Add Docker’s official GPG key:
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

3. Use the following command to set up the stable repository
```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

4. Update the apt package index again
```bash
sudo apt-get update
```

5. And install Docker Community Edition
```bash
sudo apt-get install docker-ce
```

6. Now you need to tell Docker client where the Docker host is (the docker installed in your windows), and you can do that by setting an environment variable called `DOCKER_HOST`.
```bash
echo "export DOCKER_HOST=localhost:2375" >> ~/.zshrc
```

7. Now we need to make sure that you expose the daemon on Windows, otherwise it won't work.
![1_6XwT-oT7cbw63UFHLjQPzA](https://user-images.githubusercontent.com/20981122/70489471-7f998800-1ac1-11ea-8b29-3c88a5419b3b.png)


You can now reopen your terminal and docker will be available in your WSL.

### Docker Compose
I'm sure you will need to use `docker-compose` so I'm gonna tell you how to install it.
1. Download the latest version of Docker Compose, use the command.
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

2. Next, change the file permissions to allow the new software to be executed on Ubuntu.
```bash
sudo chmod +x /usr/local/bin/docker-compose
```

And that's all, reopen your terminal and now you will also have `docker-compose` command available in your WSL.

## Extra lib: lf File Manager
Finally, I'd like to share [lf library](https://github.com/gokcehan/lf/tree/master) that's used to navigate through files and folders in an easy way.
![fd34c8b1f1ac26a8033f2ae1ff5f1439](https://user-images.githubusercontent.com/20981122/70489858-71983700-1ac2-11ea-9047-7fc2dce1cf46.jpg)

Download the version relevant to your operating system, I'll put Linux x64-bit version.
```bash
wget https://github.com/gokcehan/lf/releases/download/r6/lf-linux-amd64.tar.gz \
-O lf-linux-amd64.tar.gz
```

After downloading the package, extract it using tar
```bash
tar xvf lf-linux-amd64.tar.gz
```

Make the file executable
```bash
chmod +x lf
```

Copy the file to `/usr/local/bin` directory.
```bash
sudo mv lf /usr/local/bin
```

Reopen your terminal, and now you can use the lf command running `lf` in your terminal.


### References
I've used the following resources in order to write this guide, you should definetly go and check'em out.
- [Fluent terminal config](https://dev.to/dylantientcheu/transforming-your-ugly-windows-terminal-to-a-unicorn-577k)
- [Setting up nodejs](https://gist.github.com/noygal/6b7b1796a92d70e24e35f94b53722219)
- [Installing Docker](https://medium.com/@sebagomez/installing-the-docker-client-on-ubuntus-windows-subsystem-for-linux-612b392a44c4)
- [Installing Docker Compose](https://phoenixnap.com/kb/install-docker-compose-ubuntu)
- [Useful zsh plugins](https://gist.github.com/dogrocker/1efb8fd9427779c827058f873b94df95)
- [Install powerline fonts](https://medium.com/@slmeng/how-to-install-powerline-fonts-in-windows-b2eedecace58)
