# Ubuntu安装FireFox开发者版



从[Mozilla Firefox Developer Edition webpage](https://www.mozilla.org/en-US/firefox/developer/)下载。用`file-roller`提取它并将该文件夹移动到其最终位置。一个好的做法是将其安装在`/opt/`或`/usr/local/`中。

将文件移动到最终位置后(例如`/opt/firefox_dev/`)，您可以创建以下文件`~/.local/share/applications/firefox_dev.desktop`以获取启动器，其图标与普通Firefox不同。

```
[Desktop Entry]
Name=Firefox Developer 
GenericName=Firefox Developer Edition
Exec=/opt/firefox_dev/firefox
Terminal=false
Icon=/opt/firefox_dev/browser/chrome/icons/default/mozicon128.png
Type=Application
Categories=Application;Network;X-Developer;
Comment=Firefox Developer Edition Web Browser.
```

要启动它，请搜索`Firefox Developer`，然后只需运行`firefox`二进制文件即可。

请注意，当您手动安装时，F.D.E.默认情况下没有统一全局菜单。