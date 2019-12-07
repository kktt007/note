
network manager (NetworkManager.service)
cli: nmcli / nmtui

<font face="黑体" color=green size=5>我是黑体，绿色，尺寸为5</font>

<table><tr><td bgcolor=orange>背景色red</td></tr></table>




 **1. List nearby wifi networks:**
 
    nmcli device wifi list

**2. Connect to a wifi network:**

    nmcli device wifi connect "kktt" password "12345678"

3. See a list of network devices and their state:

- $ nmcli device

4. Turn off wifi:

- $ nmcli radio wifi off

archiso: netctl wpa_supplicant dhcpcd dialog 
cli: netctl / wifi-menu

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc3NzM3MDkxNCwtMTA2MDMwMzM4Nl19
-->