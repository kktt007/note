### network manager 
> *Use `systemctl --type=service` to ensure that no other network service is running before enabling a _netctl_ profile/service.*


1. #### NetworkManager.service 
    > `cli: nmcli / nmtui`

	1. List nearby wifi networks:

		```
        nmcli device wifi list
        ```

	2. Connect to a wifi network:**
		```
		nmcli device wifi connect "kktt" password "12345678"
		```

	3. See a list of network devices and their state:

		```
		nmcli device
		```

	4. Turn off wifi:

		```
		nmcli radio wifi off
		```

2. #### archiso: netctl (wpa_supplicant dhcpcd dialog) 
	> `cli: netctl / wifi-menu`

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMyODg0Njc5OCwtMTM2MzY0MzU3OCwtMj
A4NjE5NTkyMSwxNjMzNTc2MzUsLTEzMjI5MzQzODQsNDQyMTA5
OTksLTUwMjk4NjM4OSwxNTA5NTk0OTkzLC03NzczNzA5MTQsLT
EwNjAzMDMzODZdfQ==
-->