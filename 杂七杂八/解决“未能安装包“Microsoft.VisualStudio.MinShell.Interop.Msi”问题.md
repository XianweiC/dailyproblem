# 解决“未能安装包“Microsoft.VisualStudio.MinShell.Interop.Msi”问题

-------------------------------



未能安装包“Microsoft.VisualStudio.MinShell.Interop.Msi,version=16.0.28329.73”。
  Could not open key:

UNKNOWN\Components\F0821A7258CB16D4F8C88902F97FA48C\D3AD87A34D8CD9245B63E6950A804815.  

Verify that you have sufficient access to that key, or contact your support personnel.
  --------------------------------------------------------------------------------

 

解决方案如下：

1.运行：regedit

2.找到下面的目录

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Installer\UserData\S-X-X-XX\Components\

3.找到对应的项，删除即可，我的就是F0821A7258CB16D4F8C88902F97FA48C\D3AD87A34D8CD9245B63E6950A804815

4.如果不能删除，下个PC hunter来删