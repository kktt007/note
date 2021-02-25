## 20201210
阿里图片 数据处理-访问设置关闭原图保护

##20210225
删除系统的microsoft账号
1.
**右键开始菜单--选择“计算机管理“或者win+R输入compmgmt.msc进入计算机管理窗口。**
**系统工具--本地用户和组--用户**
勾选”**账户已禁用**“，确定重启即可。

2.
1.  假设你的微软账号是：xxx@xx.com，win+R打开运行，在运行输入框输入regedit，点击确定打开注册表编辑器，搜索微软账号名：xxx@xx.com。
2.  一般是HKEY_CURRENT_USER\Software\Microsoft\IdentityCRL\UserExtendedProperties\xxx@xx.com和HKEY_USERS\.DEFAULT\Software\Microsoft\IdentityCRL\StoredIdentities\xxx@xx.com，然后删除注册表xxx@xx.com项，开始菜单里注销微软账户；
3.  再次登录后，显示是本地账号，但是微软账号依然存在，删除HKEY_CURRENT_USER\Software\Microsoft\IdentityCRL和HKEY_USERS\.DEFAULT\Software\Microsoft\IdentityCRL中的IdentityCRL项，再次在开始菜单里注销账户；
4.  重新登陆后，在设置-账户-电子邮件和应用账户下，单击微软账户xxx@xx.com，点击“删除”即可。


> Written with [StackEdit](https://stackedit.io/).
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NjMzMzA4NDYsODYxNjMxMTIwXX0=
-->