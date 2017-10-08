参考 [树莓派折腾录一](http://blog.csdn.net/wangmi0354/article/details/50836398) 替换软件源为中科大。

```Shell
pi@raspberrypi:~ $ date
Wed Sep 27 00:44:42 CST 2017
```

# 安装 vim
执行 `sudo apt-get install vim` 命令安装 vim：

```Shell
pi@raspberrypi:~ $ sudo apt-get install vim
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  fonts-arphic-bsmi00lp fonts-arphic-gbsn00lp scim-modules-table
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  vim-common vim-runtime
Suggested packages:
  ctags vim-doc vim-scripts
The following packages will be REMOVED:
  xxd
The following NEW packages will be installed:
  vim vim-common vim-runtime
0 upgraded, 3 newly installed, 1 to remove and 0 not upgraded.
Need to get 5,422 kB of archives.
After this operation, 24.7 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://mirrors.ustc.edu.cn/raspbian/raspbian wheezy/main armhf vim-common armhf 2:7.3.547-7+deb7u4 [163 kB]
Get:2 http://mirrors.ustc.edu.cn/raspbian/raspbian wheezy/main armhf vim-runtime all 2:7.3.547-7+deb7u4 [4,586 kB]
Get:3 http://mirrors.ustc.edu.cn/raspbian/raspbian wheezy/main armhf vim armhf 2:7.3.547-7+deb7u4 [674 kB]
Fetched 5,422 kB in 5s (1,016 kB/s)
(Reading database ... 123100 files and directories currently installed.)
Removing xxd (2:8.0.0197-4) ...
Selecting previously unselected package vim-common.
(Reading database ... 123089 files and directories currently installed.)
Preparing to unpack .../vim-common_2%3a7.3.547-7+deb7u4_armhf.deb ...
Unpacking vim-common (2:7.3.547-7+deb7u4) ...
Selecting previously unselected package vim-runtime.
Preparing to unpack .../vim-runtime_2%3a7.3.547-7+deb7u4_all.deb ...
Adding 'diversion of /usr/share/vim/vim73/doc/help.txt to /usr/share/vim/vim73/doc/help.txt.vim-tiny by vim-runtime'
Adding 'diversion of /usr/share/vim/vim73/doc/tags to /usr/share/vim/vim73/doc/tags.vim-tiny by vim-runtime'
Unpacking vim-runtime (2:7.3.547-7+deb7u4) ...
Selecting previously unselected package vim.
Preparing to unpack .../vim_2%3a7.3.547-7+deb7u4_armhf.deb ...
Unpacking vim (2:7.3.547-7+deb7u4) ...
Processing triggers for mime-support (3.60) ...
Setting up vim-common (2:7.3.547-7+deb7u4) ...
Installing new version of config file /etc/vim/vimrc ...
Processing triggers for man-db (2.7.6.1-2) ...
Setting up vim-runtime (2:7.3.547-7+deb7u4) ...
Processing /usr/share/vim/addons/doc
Setting up vim (2:7.3.547-7+deb7u4) ...
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vim (vim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vimdiff (vimdiff) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rvim (rvim) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rview (rview) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vi (vi) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/view (view) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/ex (ex) in auto mode
pi@raspberrypi:~ $ vim -v
```

# 查看 vim 版本信息
执行 `vim --version` 命令查看安装的 vim 版本信息：

```Shell
pi@raspberrypi:~ $ vim --version
VIM - Vi IMproved 7.3 (2010 Aug 15, compiled Jul 18 2017 04:31:53)
Included patches: 1-547
Extra patches: 8.0.0707, 8.0.0706, 8.0.0703, 8.0.0378, 8.0.0377, 8.0.0322, 8.0.0056
Modified by pkg-vim-maintainers@lists.alioth.debian.org
Compiled by buildd@
Huge version without GUI.  Features included (+) or not (-):
+arabic +autocmd -balloon_eval -browse ++builtin_terms +byte_offset +cindent 
-clientserver -clipboard +cmdline_compl +cmdline_hist +cmdline_info +comments 
+conceal +cryptv +cscope +cursorbind +cursorshape +dialog_con +diff +digraphs 
-dnd -ebcdic +emacs_tags +eval +ex_extra +extra_search +farsi +file_in_path 
+find_in_path +float +folding -footer +fork() +gettext -hangul_input +iconv 
+insert_expand +jumplist +keymap +langmap +libcall +linebreak +lispindent 
+listcmds +localmap -lua +menu +mksession +modify_fname +mouse -mouseshape 
+mouse_dec +mouse_gpm -mouse_jsbterm +mouse_netterm -mouse_sysmouse 
+mouse_xterm +mouse_urxvt +multi_byte +multi_lang -mzscheme +netbeans_intg 
+path_extra -perl +persistent_undo +postscript +printer +profile -python 
-python3 +quickfix +reltime +rightleft -ruby +scrollbind +signs +smartindent 
-sniff +startuptime +statusline -sun_workshop +syntax +tag_binary 
+tag_old_static -tag_any_white -tcl +terminfo +termresponse +textobjects +title
 -toolbar +user_commands +vertsplit +virtualedit +visual +visualextra +viminfo 
+vreplace +wildignore +wildmenu +windows +writebackup -X11 -xfontset -xim -xsmp
 -xterm_clipboard -xterm_save 
   system vimrc file: "$VIM/vimrc"
     user vimrc file: "$HOME/.vimrc"
      user exrc file: "$HOME/.exrc"
  fall-back for $VIM: "/usr/share/vim"
Compilation: gcc -c -I. -Iproto -DHAVE_CONFIG_H     -g -O2 -fstack-protector --param=ssp-buffer-size=4 -Wformat -Werror=format-security -U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=1      
Linking: gcc   -Wl,-z,relro -Wl,--as-needed -o vim       -lm -ltinfo -lnsl  -lselinux -lacl -lattr -lgpm     
```

# 安装 vim-voom

```Shell
pi@raspberrypi:~$ sudo apt-get install vim-voom
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  fcitx-libs fonts-arphic-bsmi00lp fonts-arphic-gbsn00lp fonts-wqy-microhei
  fonts-wqy-zenhei libicu48 liblcms1 liblua5.1-0 libopencc1 libscim8v5
  libtiff4 scim-im-agent scim-modules-socket
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  vim-addon-manager vim-nox
Suggested packages:
  cscope vim-doc
The following NEW packages will be installed:
  vim-addon-manager vim-nox vim-voom
0 upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to get 1,012 kB of archives.
After this operation, 2,815 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mirrors.ustc.edu.cn/raspbian/raspbian stretch/main armhf vim-addon-manager all 0.5.6
 [19.5 kB]
Get:2 http://mirrors.ustc.edu.cn/raspbian/raspbian stretch/main armhf vim-nox armhf 2:8.0.0197-4 
[894 kB]
Get:3 http://mirrors.ustc.edu.cn/raspbian/raspbian stretch/main armhf vim-voom all 5.2-1 [98.5 kB
]
Fetched 1,012 kB in 5s (176 kB/s)  
Selecting previously unselected package vim-addon-manager.
(Reading database ... 125599 files and directories currently installed.)
Preparing to unpack .../vim-addon-manager_0.5.6_all.deb ...
Unpacking vim-addon-manager (0.5.6) ...
Selecting previously unselected package vim-nox.
Preparing to unpack .../vim-nox_2%3a8.0.0197-4_armhf.deb ...
Unpacking vim-nox (2:8.0.0197-4) ...
Selecting previously unselected package vim-voom.
Preparing to unpack .../vim-voom_5.2-1_all.deb ...
Unpacking vim-voom (5.2-1) ...
Setting up vim-nox (2:8.0.0197-4) ...
update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/vim (vim) in auto mode
update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/vimdiff (vimdiff) in auto mode
update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/rvim (rvim) in auto mode
update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/rview (rview) in auto mode
update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/vi (vi) in auto mode
update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/view (view) in auto mode
update-alternatives: using /usr/bin/vim.nox to provide /usr/bin/ex (ex) in auto mode
Setting up vim-voom (5.2-1) ...
Processing triggers for man-db (2.7.6.1-2) ...
Setting up vim-addon-manager (0.5.6) ...
```