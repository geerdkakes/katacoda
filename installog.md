# install log quectel RG500Q module

## update system

This is for an x86_64 system running ubuntu18.04

Get latest software package and kernel version
```
sudo apt-get update
sudo apt upgrade
sudo apt dist-upgrade
sudo apt-get autoremove
sudo reboot
```



## extract driver package

Extract drivers and change path to remove the unwanted characters. The `&` will break the scripts.
```
unzip QT0030801073-Quectel_5G_EVB_Kit_Support_Package.zip
cd Quectel_5G_EVB_Kit_Support_Package_V1.0/
mv Driver\&User\ Guide Driver_user_guide
cd Driver_user_guide/
unzip Quectel_LTE\&5G_Linux_USB_Driver_V1.0.zip
mv 'Quectel_Linux&Android_GobiNet_Driver_V1.6' gobi
unzip 'Quectel_Linux&Android_QMI_WWAN_Driver_V1.1.zip'
mv 'Quectel_Linux&Android_QMI_WWAN_Driver_V1.1' qmi_wwan
unzip 'Quectel_Linux_USB_Serial_Option_Driver_V1.0.zip'
mv 'Quectel_Linux_USB_Serial_Option_Driver_V1.0' USB_Serial_option
```

## install modules

For the following directories run install commands:
- gobi or qmi_wwan
- USB_Serial_option/<kernal version>

You can check the kernel version using:
```
uname -a
```

## check working with AT commands

Open de AT command port with minicom. You can optianlly use the '-C' flag to log all output for later reference. 
```
minicom -D /dev/ttyUSB2 -C logoutput.txt
```

Check if the modem is responding using:
```
AT
```
and
```
ATI
```

Check sim state. This should give the state ready
```
AT+CPIN?
```

Check the PDU context list
```
AT+CGDCONT?
```

Set a PDU context, e.g.:
```
AT+CGDCONT=1,"IP","internet"
```

## connect using the modem manager

unzip the package
```
QConnectManager_Linux_V1.5.zip
```

Compile the program
```
make install
```

Connect using:
```
sudo ./quectel-CM
```


## Other AT commands that might be useful


Set preferred 5G NR band to for example 28:
```
AT+QNWPREFCFG="nsa_nr5g_band",28
```

query current modes:
```
AT+QNWPREFCFG= "mode_pref"
```

set mode to LTE or 5GNR
```
AT+QNWPREFCFG= "mode_pref",LTE:NR5G
```

query lte bands
```
AT+QNWPREFCFG="lte_band"
```

set bands to search
```
AT+QNWPREFCFG="lte_band",1:3:7:20
```

activate context:
```
AT+CGACT=1,1
```

show the ip address of pdp context 1:
```
AT+CGPADDR=1
+CGPADDR: 1,"10.117.165.73"
```

get activated pdp context:
```
AT+CGACT?
+CGACT: 1,1
+CGACT: 2,0
+CGACT: 3,0
```

Check firmware using:
```
AT+QGMR
RG500QEAAAR01A04M4G_01.001.01.001
```

Check available networks:
```
AT+COPS=?
+COPS: (1,"NL KPN","NL KPN","20408",2),(1,"NL KPN","NL KPN","20408",7),(1,"vodafone NL","voda NL","20404",7),(1,"T-Mobile NL","TMO NL","20416",7),,(0-4),(0)
```

Check connected network technology
```
AT+QNWINFO
+QNWINFO: "FDD LTE","20408","LTE BAND 3",1300
```

Query serving cell
```
AT+QENG="servingcell"
+QENG: "servingcell","NOCONN"
+QENG: "LTE","FDD",204,08,AF7921,412,1300,3,5,5,F425,-109,-15,-73,11,255,-32768,16
+QENG:"NR5G-NSA",204,08,188,-32768,-32768,-32768
```
