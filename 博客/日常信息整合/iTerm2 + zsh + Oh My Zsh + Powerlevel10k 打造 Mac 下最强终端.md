写在前面
对于开发人员来说，每天打交道最多的两类应用即代码编辑器与终端，一个好用的代码编辑器和终端可以使效率飞速提升。代码编辑器有 VSCode，那也应有如此酷炫的终端。

除了 iTerm2，本文同样适用于大多数 Linux 终端和 WSL (Windows Subsystem for Linux)，通过以下步骤可以实现同样的效果。

先上两种配置结果:
Classic Prompt Style：

Rainbow Prompt Style：


安装 iTerm2
对于 Linux 和 WSL 用户，可以略过本步骤。Linux 使用默认的终端，WSL 使用 Windows Terminal 实现相同的效果。

对于 macOS 用户来说，iTerm2 是一个代替系统自带终端的好方案，它有很多快捷的小功能可以大幅提高效率，也拥有漂亮且个性化自由度较大的界面。

安装 zsh
查看是否已安装
```
zsh --version
```
安装
# macOS
brew install zsh zsh-completions

# Ubuntu
sudo apt-get install zsh

# CentOS
sudo yum -y install zsh
切换为默认 shell
chsh -s /bin/zsh
安装 Oh My Zsh
Oh My Zsh 可以做很多的定制化内容，包括丰富的主题与插件，让你直呼 AMAZING!!
两种方式选择一种即可：

# 使用 curl 命令
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# 或者使用 wget 命令
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
安装 Powerlevel10k
Oh My Zsh 有许许多多的主题/外部主题，个人觉得比较好用的是 Powerlevel9k，使用了大约一年的时间，但响应时间却越变越慢，遂转到了它的更新版 Powerlevel10k，它可以直接兼容 Powerlevel9k 的配置，也可以直接使用它提供的菜单化配置脚本，简单回答一些问题就可以生成美观的配置。

git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
克隆下来之后，在 zsh 的配置文件 ~/.zshrc 中设置 ZSH_THEME=powerlevel10k/powerlevel10k 即可。

安装 Nerd Font 字体
完成上述操作之后，你可能会发现终端出现了乱码，这是因为你的电脑不支持那么多字体，需要安装扩展字体。

Nerd 字体是支持 icon 最多的，可以直接在 nerd-fonts GitHub 或者官网下载 Hack Nerd Font。Powerlevel10k 作者推荐使用 Meslo Nerd Font 字体，但发现在 iTerm2 下 Hack Nerd Font 更好看一点，其他系统还是下载 Meslo Nerd Font 比较保险。

对于 macOS 和 WSL 来说，直接双击下载的 ttf 文件即可安装。对于 Linux 来说，需要将文件放入指定目录并刷新缓存，请看这里。

安装之后，对于 iTerm2 来说，在 Preferences-Profiles-Text-Font 设置为对应字体。Windows Terminal 在 settings.json 配置中加入 "fontFace": "MesloLGS NF" 即可。

配置 Powerlevel10k
配置分为两步，首先使用自动化配置脚本，其次根据个人喜好进行个性化设置。

自动配置脚本
Powerlevel10k 提供了一个配置脚本，运行脚本后只需回答几个简单的问题即可完成配置。

直接输入 p10k configure 即可进入配置问答界面，完成后会生成一个配置文件 ~/.p10k.zsh，并且在 ~/.zshrc 中自动加入了

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ -f ~/.p10k.zsh ]] && source ~/.p10k.zsh
在配置过程中需要注意的是，Instant Promt Mode 尽量选择打开，可以加快终端启动速度，详情请见这里。

个性化设置
在 Powerlevel10k 新生成的配置文件 ~/.p10k.zsh 中根据个人喜好进行个性化设置。

每次修改配置文件后重启终端或者新开一个 tab 即可显示。
在 vim 中可以通过 :/str 来执行搜索，通过 N 或 n 键来跳转到上一个结果或下一个结果。

左右栏图标显示
左栏图标修改 POWERLEVEL9K_LEFT_PROMPT_ELEMENTS 中内容，右栏图标修改 POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS 中内容。作者写了比较详细的注释，按需修改即可，也可以调整显示顺序。全部可配置内容请见这里，也可以自己实现一个。

左右分隔符号
也就是文首第二张图像火一样的分隔符号，实际上用到了两个 Unicode 字符 \uE0C0 和 \uE0C2。还有其他形状的字符，请在 Nerd Font Cheat Sheet 搜索 E0。

 Separator between different-color segments on the left.
typeset -g POWERLEVEL9K_LEFT_SEGMENT_SEPARATOR='\uE0C0'
 Separator between different-color segments on the right.
typeset -g POWERLEVEL9K_RIGHT_SEGMENT_SEPARATOR='\uE0C2'
 The right end of left prompt.
typeset -g POWERLEVEL9K_LEFT_PROMPT_LAST_SEGMENT_END_SYMBOL='\uE0C0'
 The left end of right prompt.
typeset -g POWERLEVEL9K_RIGHT_PROMPT_FIRST_SEGMENT_START_SYMBOL='\uE0C2'
长路径折叠
Powerlevel10k 默认将长路径折叠到只显示最上层和最底层，多少有些不方便，可以通过如下进行更改，推荐 2 或者 3。

 Don't shorten this many last directory segments. They are anchors.
typeset -g POWERLEVEL9K_SHORTEN_DIR_LENGTH=2
命令成功提示符
命令成功提示符（即右边栏最左边的对号）有时候会被遮挡住，可能是一个小 bug 吧，希望作者后续能修复它，现在可以通过在前面加一个空格来避免：

typeset -g POWERLEVEL9K_STATUS_OK_VISUAL_IDENTIFIER_EXPANSION=' ✔'

typeset -g POWERLEVEL9K_STATUS_OK_PIPE_VISUAL_IDENTIFIER_EXPANSION=' ✔'
颜色配置
查看所有可用颜色：

for i in {0..255}; do print -Pn "%K{$i}  %k%F{$i}${(l:3::0:)i}%f " ${${(M)$((i%6)):#3}:+$'\n'}; done
修改目录颜色为黑色字：

#################################[ dir: current directory ]##################################
 Current directory background color.
 typeset -g POWERLEVEL9K_DIR_BACKGROUND=4
 Default current directory foreground color.
typeset -g POWERLEVEL9K_DIR_FOREGROUND=0

 Color of the shortened directory segments.
typeset -g POWERLEVEL9K_DIR_SHORTENED_FOREGROUND=238
 Color of the anchor directory segments. Anchor segments are never shortened. The first
 segment is always an anchor.
typeset -g POWERLEVEL9K_DIR_ANCHOR_FOREGROUND=0
 Display anchor directory segments in bold.
typeset -g POWERLEVEL9K_DIR_ANCHOR_BOLD=true
修改时间显示块颜色使得不那么刺眼：

typeset -g POWERLEVEL9K_TIME_BACKGROUND=255
其实在 ~/.p10k.zsh 中，所有的颜色几乎都可以修改，作者注释也写的很清楚，可以自己根据喜好配置。

Oh My Zsh 插件
Oh My Zsh 有非常丰富的插件，使用插件可以使得在终端的效率翻倍，下面介绍 5 个我常用的插件。
插件均需在配置文件 ~/.zshrc 中写出，如下：

plugins=(
  git
  github
  autojump
  zsh-syntax-highlighting
  zsh-autosuggestions
)
git
git plugin
提供丰富的 git 别名与几个有用的函数。

github
github plugin
提供几个快捷的函数。

autojump
autojump
可以记录下来你之前 cd 到访过的所有目录，下次要去那个目录时不需要输入完整的路径，直接 j somedir 即可到达，甚至那个目标目录的名称只输入开头也可以。

安装方式

zsh-syntax-highlighting
zsh-syntax-highlighting
终端命令语法高亮。

 克隆
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
 ~/.zshrc 中配置
plugins=(zsh-syntax-highlighting)
zsh-autosuggestions
zsh-autosuggestions
终端命令自动推荐，会记录下来之前使用过的命令，当你输入开头时，会暗色提示之前的历史命令供你选择，可直接按右方向键选中该命令。

 克隆
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
 ~/.zshrc 中配置
plugins=(zsh-autosuggestions)
修改 VSCode 的终端
VSCode 带的终端界面也可保持一致，只需简单设置字体即可。
打开 VSCode 的设置，搜索 terminal font，做如下修改：


Post author: Sui Xin
Post link: https://suixinblog.cn/2019/09/beautify-terminal.html
Copyright Notice: All articles in this blog are licensed under BY-NC-SA unless stating additionally.
