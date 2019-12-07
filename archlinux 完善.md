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

#### 2. archiso: netctl (wpa_supplicant dhcpcd dialog) 
	> `cli: netctl / wifi-menu`

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNjM2NDM1NzgsLTIwODYxOTU5MjEsMT
YzMzU3NjM1LC0xMzIyOTM0Mzg0LDQ0MjEwOTk5LC01MDI5ODYz
ODksMTUwOTU5NDk5MywtNzc3MzcwOTE0LC0xMDYwMzAzMzg2XX
0=
-->