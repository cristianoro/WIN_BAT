# WIN_BAT
Windows BAT批处理指令学习笔记

- **打开电脑时同时运行某个程序**
```
@echo off
echo Starting chrome...
::路径改成自己相应的
start "" "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" www.google.com
```
将上面.bat文件放到Windows**启动目录**下：
```
C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
```
打开Chrome浏览器并浏览谷歌，网站可以换成自己想要查看的任何网站。
