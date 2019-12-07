Use `systemctl --type=service` to ensure that no other network service is running before enabling a _netctl_ profile/service.

### network manager 


#### 1.  NetworkManager.service
> **cli: nmcli / nmtui**

<font face="黑体" color=green size=5>我是黑体，绿色，尺寸为5</font>

<table><tr><td bgcolor=orange>背景色red</td></tr></table>
结尾2空格
开头 1 2 除此4个的换用tab=4 spacebace



 **1. List nearby wifi networks:**
 
	nmcli device wifi list

**2. Connect to a wifi network:**

	nmcli device wifi connect "kktt" password "12345678"

**3. See a list of network devices and their state:**

	nmcli device

**4. Turn off wifi:**

	nmcli radio wifi off

#### 2. archiso: netctl wpa_supplicant dhcpcd dialog 
> **cli: netctl / wifi-menu**

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5NDg5MjM1NSwtNTAyOTg2Mzg5LDE1MD
k1OTQ5OTMsLTc3NzM3MDkxNCwtMTA2MDMwMzM4Nl19
-->