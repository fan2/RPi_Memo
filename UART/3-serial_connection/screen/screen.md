## recover
[Gnu screen: kill a frozen tab](https://superuser.com/questions/458122/gnu-screen-kill-a-frozen-tab)  
[Kill detached screen session](https://stackoverflow.com/questions/1509677/kill-detached-screen-session)  
[How to recover a 'lost' screen session?](https://unix.stackexchange.com/questions/28675/how-to-recover-a-lost-screen-session)  
[How do I kill a screen if I know the name of it?](https://superuser.com/questions/112117/how-do-i-kill-a-screen-if-i-know-the-name-of-it)  
[The GNU screen is unresponsive, seems blocked](https://stackoverflow.com/questions/4367669/the-gnu-screen-is-unresponsive-seems-blocked)  
[Kill a GNU Screen Session from the Command Line](http://droptips.com/kill-a-gnu-screen-session-from-the-command-line)  
[How to prevent screen from terminating when command in window terminates](https://serverfault.com/questions/237778/how-to-prevent-screen-from-terminating-when-command-in-window-terminates)  

Anyway, add this to your ~/.screenrc:

```Shell
zombie kr
verbose on
```

try <kbd>ctrl</kbd>+<kbd>a</kbd>,<kbd>q</kbd> to send the `Xon` signal, which is the sequence to unblock scrolling.

try <kbd>ctrl</kbd>+<kbd>a</kbd>,<kbd>:</kbd> to open bottom command prompt, and type `zombie kr` to kill and restart after its command has finished.

## session
> [screen-session](https://github.com/skoneka/screen-session) - a collection of tools for GNU Screen  
> [使用 GNU Screen 管理终端会话](https://meiriyitie.com/2015/07/15/using-gnu-screen-to-manage-persistent-terminal-sessions/)  
> [使用 Screen 创建并管理多个 shell](https://www.ibm.com/developerworks/cn/aix/library/au-gnu_screen/index.html)  
> [使用 Screen 指令操控 UNIX/Linux 終端機的教學與範例](https://blog.gtwang.org/linux/screen-command-examples-to-manage-linux-terminals/)  

## .screenrc
[tnarihi/.screenrc](https://gist.github.com/tnarihi/3c459b4df0ff7a64695c)  
[What are useful .screenrc settings?](https://serverfault.com/questions/3740/what-are-useful-screenrc-settings)  
[Understanding GNU Screen’s hardstatus strings](http://www.kilobitspersecond.com/2014/02/10/understanding-gnu-screens-hardstatus-strings/)  
[GNU screen status bar - how to make it display shell session names?](https://unix.stackexchange.com/questions/114505/gnu-screen-status-bar-how-to-make-it-display-shell-session-names)  

[screen command to persistently enable menu at bottom](https://stackoverflow.com/questions/19705378/screen-command-to-persistently-enable-menu-at-bottom)  
[How do I supress date/time display in GNU Screen vertical splits?](https://superuser.com/questions/600851/how-do-i-supress-date-time-display-in-gnu-screen-vertical-splits)  
