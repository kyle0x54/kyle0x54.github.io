---
title: "Ubuntu系统配置"
tags:
  - ubuntu
  - config
---


## 1. 设置阿里云apt源
1. 设置apt安装源为阿里云
`system settings` -> `Software & Updates`
2. 更新apt软件包
```sh
sudo apt update
sudo apt upgrade
```


## 2. 安装常用软件
```sh
sudo apt install openssh-server zsh tree ncdu htop dfc
sudo apt install byobu tilda krusader
sudo apt install vim git cmake meld
sudo apt install axel rdesktop filezilla smplayer digikam okular typora tig keepass2
sudo apt install tldr unity-tweak-tool compizconfig-settings-manager
sudo pip install percol pygments

# git plugins
sudo apt-get install git-extras
sudo apt install npm
sudo npm install -g diff-so-fancy
sudo npm install -g commitizen

# oh-my-zsh
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

# google-chrome web browser
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb

# sublime-text
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text

# anaconda
```


## 3. 配置git
```sh
git config --global user.email "kyle0x54@163.com"
git config --global user.name kyle0x54
git config --global core.editor "vim"

git config --global alias.st status
git config --global alias.ci commit
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.unstage 'reset HEAD'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"


# 开启diff-so-fancy并配色
git config --global core.pager "diff-so-fancy | less --tabs=4 -RFX"

git config --global color.ui true

git config --global color.diff-highlight.oldNormal "red bold"
git config --global color.diff-highlight.oldHighlight "red bold 52"
git config --global color.diff-highlight.newNormal "green bold"
git config --global color.diff-highlight.newHighlight "green bold 22"

git config --global color.diff.meta "227"
git config --global color.diff.frag "magenta bold"
git config --global color.diff.commit "227 bold"
git config --global color.diff.old "red bold"
git config --global color.diff.new "green bold"
git config --global color.diff.whitespace "red reverse"

# 为某个项目配置commitizen，该项目主文件夹下执行如下命令
npm init --yes
commitizen init cz-conventional-changelog --save --save-exact
```

生成ssh-key
```sh
ssh-keygen -t rsa -C "kyle0x54@163.com"
cat ~/.ssh/id_rsa.pub
```


## 4. 配置vim
```sh
echo "\
:set number\n\
:syntax on\n\
:set nocompatible\n\
:set nobackup\n\
:set ts=4\n\
:set expandtab\n\
:set shiftwidth=4\n\
:set autoindent\n\
:set smartindent\n\
:set hlsearch\n\n\
autocmd Filetype gitcommit setlocal spell textwidth=72\
" > ~/.vimrc
```


## 5. 安装常用terminal插件
### 5.1 安装oh-my-zsh插件[zsh-syntax-highlighting]和[zsh-autosuggestion]
1. 把插件源代码克隆到oh-my-zsh目录
```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

2. 在oh-my-zsh插件列表加入插件，修改`~/.zshrc`文件中的`plugins`
```
plugins=([...], zsh-autosuggestions zsh-syntax-highlighting)
```
并使之立即生效
```sh
source activate ~/.zshrc
```

### 5.2 安装配置autojump
```sh
sudo apt install autojump
echo ". /usr/share/autojump/autojump.sh" >> ~/.zshrc
source activate ~/.zshrc
```


## 6. 设置阿里云pip源
```sh
mkdir ~/.pip
echo "\
[global]\n\
index-url = http://mirrors.aliyun.com/pypi/simple/\n\
\n\
[install]\n\
trusted-host=mirrors.aliyun.com\
" > ~/.pip/pip.conf
```


## 7. 设置全局alias
```sh
echo "\
alias untar='tar -zxvf '\n\
alias wget='wget -c '\n\
alias ping='ping -c 5'\n\
alias ccat='pygmentize -g -O style=colorful,linenos=1'\n\
alias apt-get='sudo apt-get'\n\
alias ..='cd ..'\n\
" >> ~/.zshrc
```

## 8. 其他
- Krusader Terminal 设置
in Krusader menu -> Settings -> Configure Krusader... -> Tab "General" -> Terminal: gnome-terminal --working-directory %d
- teamviewer
- cuda和cudnn
    - [install cuda](http://www.jianshu.com/p/eb42f81f4e47)
- 搜狗拼音输入法
    - [install sogou](http://jingyan.baidu.com/article/380abd0a0e135f1d91192c4f.html)
- 编译boost & opencv
    - [compile boost](http://www.jianshu.com/p/d343d4cbea13)
    - [compile opencv](http://www.jianshu.com/p/4b52d4288d06)
- 安装 pycharm & clion
    ```sh
    wget https://download.jetbrains.8686c.com/cpp/CLion-2017.1.3.tar.gz
    tar -xvzf CLion-2017.1.3.tar.gz
    cd clion-2017.1.3/bin
    ./clion.sh
    ```
- 安装manoco字体
    - 参考[manoco font installation](https://github.com/cstrap/monaco-font.git)
- ubuntu 18.04, 配置单击图标最小化
    ```sh
    gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'
    ```
