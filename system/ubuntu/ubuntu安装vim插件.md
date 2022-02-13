## vim

### info

执行 `vim --version` 查看 vim 版本信息：

```Shell
pifan@rpi4b-ubuntu:~$ vim --version
VIM - Vi IMproved 8.2 (2019 Dec 12, compiled Dec 17 2021 16:55:33)
Included patches: 1-2434, 3402-3403, 3409, 3428, 3487, 3564, 3581-3582, 3611, 3613, 3612, 3625, 3669, 3741
Modified by team+vim@tracker.debian.org
Compiled by team+vim@tracker.debian.org
Huge version with GTK3 GUI.  Features included (+) or not (-):

...
   system vimrc file: "$VIM/vimrc"
     user vimrc file: "$HOME/.vimrc"
 2nd user vimrc file: "~/.vim/vimrc"
      user exrc file: "$HOME/.exrc"
  system gvimrc file: "$VIM/gvimrc"
    user gvimrc file: "$HOME/.gvimrc"
2nd user gvimrc file: "~/.vim/gvimrc"
       defaults file: "$VIMRUNTIME/defaults.vim"
    system menu file: "$VIMRUNTIME/menu.vim"
  fall-back for $VIM: "/usr/share/vim"
...
```

查看 `/usr/share/vim` 目录结构：

```Shell
pifan@rpi4b-ubuntu:~$ tree -L 1 /usr/share/vim
/usr/share/vim
├── addons
├── gvimrc -> /etc/vim/gvimrc
├── registry
├── vim82
├── vimfiles
├── vimrc -> /etc/vim/vimrc
└── vimrc.tiny -> /etc/vim/vimrc.tiny
```

三个配置文件：

- /etc/vim/gvimrc
- /etc/vim/vimrc
- /etc/vim/vimrc.tiny

```Shell
$ vim /etc/vim/vimrc.tiny

" Debian system-wide default configuration Vim
set runtimepath=~/.vim,/var/lib/vim/addons,/usr/share/vim/vimfiles,/usr/share/vim/vim82,/usr/share/vim/vimfiles/after,/var/lib/vim/addons/after,~/.vim/after

set compatible

" vim: set ft=vim:
```

/etc/vim/vimrc.tiny 中 runtimepath 第二项是 /var/lib/vim/addons，来看看其下结构。
可以看到其下的 autoload 和 plugin 插件实际软链到 /usr/share/vim/addons/ 目录。

```Shell
pifan@rpi4b-ubuntu:~$ tree -L 2 /var/lib/vim/addons/
/var/lib/vim/addons/
├── autoload
│   ├── pathogen.vim -> /usr/share/vim/addons/autoload/pathogen.vim
│   └── syntastic
├── doc
│   ├── syntastic-checkers.txt -> /usr/share/vim/addons/doc/syntastic-checkers.txt
│   ├── syntastic.txt -> /usr/share/vim/addons/doc/syntastic.txt
│   └── tags
├── plugin
│   ├── syntastic
│   └── syntastic.vim -> /usr/share/vim/addons/plugin/syntastic.vim
└── syntax_checkers
...
```

### config

将 macOS 上的 `~/.vimrc` 复制到 rpi4b-ubuntu 上应用。

如果通过 apt install 安装过 vim-pathogen，runtimepath 中默认包含了 /usr/share/vim/addons/，启动时会自动加载 autoload/pathogen.vim，因此在自定义配置中，无需重复加载 `pathogen.vim`，直接 call pathogen 的相关函数即可。

```Shell
$ vim ~/.vimrc

124 "通过 apt install vim-pathogen，无需重复加载。
125 "set runtimepath+=~/.vim/autoload/pathogen.vim
126 call pathogen#infect()
127 call pathogen#helptags()
```

### plugin

```Shell
$ apt search vim --name-only

vim/impish-updates,impish-security,now 2:8.2.2434-3ubuntu3.2 arm64 [installed,automatic]
  Vi IMproved - enhanced vi editor

vim-addon-manager/impish,now 0.5.10 all [installed,automatic]
  manager of addons for the Vim editor

vim-airline/impish 0.11-1 all
  Lean & mean status/tabline for vim that\'s light as air

vim-autopep8/impish 1.2.0-2 all
  vim plugin to apply autopep8

vim-gitgutter/impish 0~20200414-2 all
  Vim plugin which shows a git diff in the sign column

# 插件脚本管理器
vim-pathogen/impish 2.4-5 all
  Manage your runtimepath with ease

vim-scripts/impish 20210124.1 all
  plugins for vim, adding bells and whistles

vim-solarized/impish 0~git110509-3 all
  Solarized Colorscheme for Vim

# 语法检查
vim-syntastic/impish,now 3.10.0-2 all [installed]
  Syntax checking hacks for vim

vim-tabular/impish 1.0-6 all
  Vim script for text filtering and alignment

# TOC
vim-voom/impish 5.3-8 all
  Vim two-pane outliner

vim-youcompleteme/impish 0+20200825+git2afee9d+ds-2 all
  fast, as-you-type, fuzzy-search code completion engine for Vim
```

安装 `pathogen` 和 `syntastic` 插件：

```Shell
$ sudo apt install vim-pathogen
$ sudo apt install vim-syntastic
```

安装后，会出现在 `apt list --manual-installed` 手动安装列表中：

```Shell
pifan@rpi4b-ubuntu:~$ apt list --manual-installed vim*
Listing... Done
vim-pathogen/impish,now 2.4-5 all [installed]
vim-syntastic/impish,now 3.10.0-2 all [installed]
```

查看 `/usr/share/vim/addons/` 目录结构：

```Shell
pifan@rpi4b-ubuntu:~$ tree -L 2 /usr/share/vim/addons/
/usr/share/vim/addons/
├── autoload
│   ├── pathogen.vim
│   └── syntastic
├── doc
│   ├── syntastic-checkers.txt
│   └── syntastic.txt
├── plugin
│   ├── editexisting.vim -> ../../vim82/macros/editexisting.vim
│   ├── justify.vim -> ../../vim82/macros/justify.vim
│   ├── matchit.vim -> ../../vim82/macros/matchit.vim
│   ├── syntastic
│   └── syntastic.vim
├── syntax
│   └── jinja.vim
└── syntax_checkers
...
```

### vim-addons

查看已安装的 vim 相关的包：

```Shell
pifan@rpi4b-ubuntu:~$ apt list --installed vim*
# 或 apt list --installed vim* | grep -v automatic
pifan@rpi4b-ubuntu:~$ apt list --manual-installed vim*
```

执行 apt show 命令可以查看包信息，其中 *Depends* 为其依赖包。

```Shell
pifan@rpi4b-ubuntu:~$ apt show vim-pathogen | grep Depends
pifan@rpi4b-ubuntu:~$ apt show vim-syntastic | grep Depends
```

在 ubuntu 上通过 apt 安装以上插件，会自动安装依赖的 vim-addon-manager。

运行 `vim-addon-manager` 或 **`vim-addons`** 命令可查看 vim 插件状态：

```Shell
pifan@rpi4b-ubuntu:~$ vim-addons
# Name                     User Status  System Status
editexisting                removed       removed
jinja                       removed       removed
justify                     removed       removed
matchit                     removed       removed
pathogen                    removed       installed
syntastic                   removed       installed
```

> 关于 **vim-addons** 命令的详细用法，可以通过 `man vim-addon-manager`  或 `man vim-addons` 查看帮助文档。

对于 vim 的插件管理，我们既可以用 vim-addons，也可以基于 pathogen，自行 git clone 插件到 ~/.vim/bundle 目录下。
