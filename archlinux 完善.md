### network manager 
> *Use `systemctl --type=service` to ensure that no other network service is running before enabling a _netctl_ profile/service.*

#### 1.  NetworkManager.service `cli: nmcli / nmtui`


 **1.1 List nearby wifi networks:**
 
	nmcli device wifi list

**1.2 Connect to a wifi network:**

	nmcli device wifi connect "kktt" password "12345678"

**1.3 See a list of network devices and their state:**

	nmcli device

**1.4 Turn off wifi:**

	nmcli radio wifi off

#### 2. archiso: netctl (wpa_supplicant dhcpcd dialog) `cli: netctl / wifi-menu`

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMjI5MzQzODQsNDQyMTA5OTksLTUwMj
k4NjM4OSwxNTA5NTk0OTkzLC03NzczNzA5MTQsLTEwNjAzMDMz
ODZdfQ==
-->