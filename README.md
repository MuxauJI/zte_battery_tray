# zte_battery_tray
Show ZTE MF920 battery fxce4 tray

![ZTE](https://www.ixbt.com/img/r30/00/02/24/04/title1.jpg)

## With [Genmon-plugin](https://docs.xfce.org/panel-plugins/xfce4-genmon-plugin/start)

```
#!/bin/bash
net_name=$(iwgetid -r)
if [ "$net_name" = "ZTE MF920" ]; then
	battery_value=$(curl -s --location --request GET 'http://192.168.0.1/goform/goform_get_cmd_process?multi_data=1&isTest=false&cmd=modem_main_state%2Cpin_status%2Copms_wan_mode%2Cloginfo%2Cnew_version_state%2Ccurrent_upgrade_state%2Cis_mandatory%2Cwifi_dfs_status%2Cbattery_value%2Cppp_dial_conn_fail_counter&_=1668023062256' \
--header 'Referer: http://192.168.0.1/index.html'| jq -r '.battery_value')
	if [ $battery_value -eq 100 ];then
		echo "<icon>gpm-battery-100</icon>"
	elif [ $battery_value -gt 80 ];then
		echo "<icon>gpm-battery-080</icon>"
	elif [ $battery_value -gt 60 ];then
		echo "<icon>gpm-battery-060</icon>"
	elif [ $battery_value -gt 40 ];then
		echo "<icon>gpm-battery-040</icon>"
	elif [ $battery_value -gt 20 ];then
		echo "<icon>gpm-battery-020</icon>"
	else
		echo "<icon>gpm-battery-000</icon>"
	fi
	echo "<txt>$battery_value% </txt>"
else
	echo "<txt>$net_name</txt>"
fi

```
