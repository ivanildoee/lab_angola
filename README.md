# Configuração LAB-SW-CORE-01

Os passos abaixo descrevem como configurar o switch
Configurar hostname
```
conf t
hostname LAB-SW-CORE-01
```
Configurar todas vlans
```
vlan 2
 name Mgmt
#
vlan 3
 name internet
#
vlan 10
 name Domain_Controller
#
vlan 12
 name DNS_Externo
#
vlan 13
 name Email_server
#
vlan 20
 name Webserver
#
vlan 30
 name Financeiro
#
vlan 31
 name Informatica
#
vlan 50
 name Proxy_Server
#
vlan 100
 name SecOps
#
```

configuração das portas

```
vrf context management
  ip route 0.0.0.0/0 172.16.2.1
#
interface mgmt0
  vrf member management
  ip address 172.16.2.2/24
#
int Ethernet2/1
 description Connected FW-01 Port e1
 switchport
 switchport mode access
 switchport access vlan 2
 no shut
#
int Ethernet2/2
 description Connected FW-01 Port e2
 switchport
 switchport mode trunk
 switchport trunk allowed vlan 2,3,10,12,13,20,30,31,50,100
 no shut
#
int Ethernet2/3
 description Connected FW-02 Port e1
 switchport
 switchport mode access
 switchport access vlan 2
 no shut
#
int Ethernet2/4
 description Connected FW-02 Port e2
 switchport
 switchport mode trunk
 switchport trunk allowed vlan 2,3,10,12,13,20,30,31,50,100
 no shut
#
int Ethernet2/5
 description Connected LAB-SW-SERVICES-01 Port Mgmt0
 switchport
 switchport mode access
 switchport access vlan 2
 no shut
#
int Ethernet2/6
 description Connected LAB-SW-SERVICES-01 Port E2/1
 switchport
 switchport mode trunk
 switchport trunk allowed vlan 2,10,12,13,20
 no shut
#
int Ethernet2/7
 description Connected LAB-SW-SERVICES-02 Port Mgmt0
 switchport
 switchport mode access
 switchport access vlan 2
 no shut
#
int Ethernet2/8
 description Connected LAB-SW-SERVICES-02 Port E2/1
 switchport
 switchport mode trunk
 switchport trunk allowed vlan 2,50,100
 no shut
#
int Ethernet2/9
 description Connected LAB-SW-ACCESS-01 Port Mgmt0
 switchport
 switchport mode access
 switchport access vlan 2
 no shut
#
int Ethernet2/10
 description Connected LAB-SW-ACCESS-01 Port E2/1
 switchport
 switchport mode trunk
 switchport trunk allowed vlan 2,30,31
 no shut
#
int Ethernet2/11
 description Connected Internet
 switchport
 switchport mode access
 switchport access vlan 3
 no shut
#
```
Configurar snmp
```
snmp-server contact info@lab.local
snmp-server location Datacenter
snmp-server community lab1234 RO
```
Salvar configuração
````
end
copy running-config startup-config
````
# Configuração LAB-SW-ACCESO-01

Os passos abaixo descrevem como configurar o switch

```
hostname LAB-SW-ACCESS-01
```

Configurar todas vlans
```
vlan 2
 name Mgmt
#
vlan 30
 name Financeiro
#
vlan 31
 name Informatica
#
```

configuração das portas

```
vrf context management
  ip route 0.0.0.0/0 172.16.2.1
#
interface mgmt0
  vrf member management
  ip address 172.16.2.5 255.255.255.0
#
int Ethernet2/1
 description Connected LAB-SW-CORE-01 Port G0/2
 switchport
 switchport mode trunk
 switchport trunk allowed vlan 2,30,31
 no shut
#
int Ethernet2/2
 description Connected LAB-SW-CORE-01 Port Mgmt
 switchport
 switchport mode access
 switchport access vlan 2
 no shut
#
int Ethernet 2/5 - 9
 description LAN Informatica
 switchport
 switchport mode access
 switchport access vlan 31
 no shut
#
int Ethernet 2/10 - 19
 description LAN Financeiro
 switchport
 switchport mode access
 switchport access vlan 30 
 no shut
#
```
Configurar snmp
```
snmp-server contact info@lab.local
snmp-server location Datacenter
snmp-server community lab1234 RO
```
Salvar configuração
````
end
copy running-config startup-config
````
# Configuração LAB-SW-SERVICES-01

Os passos abaixo descrevem como configurar o switch

```
hostname LAB-SW-SERVICES-01
```
Configurar todas vlans
```
vlan 2
 name Mgmt
#
vlan 10
 name Domain_Controller
#
vlan 12
 name DNS_Externo
#
vlan 13
 name Email_server
#
vlan 20
 name Webserver
#
```

configuração das portas

```
vrf context management
  ip route 0.0.0.0/0 172.16.2.1
#
interface mgmt0
  vrf member management
   ip address 172.16.2.3 255.255.255.0
#
int Ethernet2/1
 description Connected SW-CORE-01 Port G2/6
 switchport
 switchport mode trunk
 switchport trunk allowed vlan 10,12,13,20
 no shut
#
int Ethernet2/5 - 7
 description LAN Domain_Controller
 switchport
 switchport mode access
 switchport access vlan 10
 no shut
#
int Ethernet2/8 - 10
 description LAN DNS_Externo
 switchport
 switchport mode access
 switchport access vlan 12
 no shut
#
int Ethernet2/11 - 13
 description LAN Email_server
 switchport
 switchport mode access
 switchport access vlan 13
 no shut
#
int Ethernet2/15 - 16
 description LAN Webserver
 switchport
 switchport mode access
 switchport access vlan 20
 no shut
#
```

Configurar snmp
```
snmp-server contact info@lab.local
snmp-server location Datacenter
snmp-server community lab1234 RO
```
Salvar configuração
````
end
copy running-config startup-config
````
# Configuração LAB-SW-SERVICES-02

Os passos abaixo descrevem como configurar o switch

```
hostname LAB-SW-SERVICES-02
```
Configurar todas vlans
```
vlan 2
 name Mgmt
#
vlan 50
 name Proxy_Server
#
vlan 100
 name SecOps
#
```

configuração das portas

```
vrf context management
  ip route 0.0.0.0/0 172.16.2.1
#
interface mgmt0
  vrf member management
   ip address 172.16.2.4 255.255.255.0
#
int Ethernet2/1
 description Connected SW-CORE-01 Port G0/2
 switchport
 switchport mode trunk
 switchport trunk allowed vlan 2,50,100
 no shut
#
int Ethernet2/5 - 9
 description LAN Proxy_Server
 switchport
 switchport mode access
 switchport access vlan 50
 no shut
#
int Ethernet2/10 - 19
 description LAN SecOps
 switchport
 switchport mode access
 switchport access vlan 100
 no shut
#
```

Configurar snmp
```
snmp-server community lab1234 RO
```
Salvar configuração
````
end
copy running-config startup-config
````
# Configuração LAB-FW-01
configuração de portas
```
config system ha
    set group-name "lab"
    set mode a-a
    set password lab
    set hbdev "port3" 0
    set ha-mgmt-status enable
    config ha-mgmt-interfaces
        edit 1
            set interface "port1"
            set gateway 172.16.2.1
        next
    end
    set override disable
    set monitor "port2"
end
config system interface
    edit port1
        set alias "MgmtInt"
        set mode static
        set ip 172.16.2.10/24
        set allowaccess https http ping ssh snmp
    next
    edit port2
        set alias CoreTrunk
    next
    edit Informatica
        set vdom "root"
        set alias Informatica
        set allowaccess https http ping ssh
        set ip 172.16.31.1/24
        set role lan
        set interface "port2"
        set vlanid 31
    next    
    edit Mgmt
        set vdom "root"
        set alias Mgmt
        set allowaccess https http ping ssh
        set ip 172.16.2.1/24
        set role lan
        set interface "port2"
        set vlanid 2
    next
end

```
configurar DHCP
```
config system dhcp server
    edit 10
        set dns-service default
        set ntp-service local
        set default-gateway 172.16.31.1
        set netmask 255.255.255.0
        set interface Informatica
        config ip-range
            edit 1
                set start-ip 172.16.31.20
                set end-ip 172.16.31.254
            next
        end
    next
end
```
Criar politica para permitir comunicação com mgmt
```
config firewall policy
    edit 1
        set name "Allow to Mgmt"
        set srcintf "Informatica"
        set dstintf "Mgmt"
        set srcaddr "all"
        set dstaddr "all"
        set action accept
        set schedule "always"
        set service "ALL"
        set logtraffic all
    next
end
```
# Configuração FW-02
```
config system ha
    set group-name "lab"
    set mode a-a
    set password lab
    set hbdev "port3" 0
    set ha-mgmt-status enable
    config ha-mgmt-interfaces
        edit 1
            set interface "port1"
            set gateway 172.16.2.1
        next
    end
    set override disable
    set monitor "port2"
    set priority 100
end
config system interface
    edit port1
        set alias "MgmtInt"
        set mode static
        set allowaccess https http ping ssh snmp
        set ip 172.16.2.11/24
    next
end
```

# Configuração do LAB-FW em cluster

```
config system interface
    edit DomainControler
        set vdom "root"
        set alias DomainControler
        set allowaccess ping
        set ip 172.16.10.1/24
        set role lan
        set interface "port2"
        set vlanid 10
    next
    edit DNS_Externo
        set vdom "root"
        set alias DNS_Externo
        set allowaccess ping
        set ip 172.16.12.1/24
        set role lan
        set interface "port2"
        set vlanid 12
    next
    edit Email_server
        set vdom "root"
        set alias Email_server
        set allowaccess ping
        set ip 172.16.13.1/24
        set role lan
        set interface "port2"
        set vlanid 13
    next
    edit Webserver
        set vdom "root"
        set alias Webserver
        set allowaccess ping
        set ip 172.16.20.1/24
        set role lan
        set interface "port2"
        set vlanid 20
    next
    edit Proxy_Server
        set vdom "root"
        set alias Proxy_Server
        set allowaccess ping
        set ip 172.16.50.1/24
        set role lan
        set interface "port2"
        set vlanid 50
    next
    edit SecOps
        set vdom "root"
        set alias SecOps
        set allowaccess ping
        set ip 172.16.100.1/24
        set role lan
        set interface "port2"
        set vlanid 100
    next
    edit Financeiro
        set vdom "root"
        set alias Financeiro
        set allowaccess ping
        set ip 172.16.30.1/24
        set role lan
        set interface "port2"
        set vlanid 30
    next
    edit Internet
        set vdom "root"
        set alias Internet
        set allowaccess ping
        set ip 192.168.122.2/24
        set role lan
        set interface "port2"
        set vlanid 3
    next
end
```
configurar DHCP
```
config system dhcp server
    edit 10
        set dns-service default
        set ntp-service local
        set default-gateway 172.16.30.1
        set netmask 255.255.255.0
        set interface Financeiro
        config ip-range
            edit 1
                set start-ip 172.16.30.20
                set end-ip 172.16.30.254
            next
        end
    next
end
```
Criar politica para permitir comunicação para internet
```
config firewall policy
    edit 2
        set name "Allow access to Internet"
        set srcintf "DNS_Externo" "Email_server" "Informatica" "Proxy_Server" "SecOps" "Webserver"
        set dstintf "Internet"
        set srcaddr "all"
        set dstaddr "all"
        set action accept
        set schedule "always"
        set service "ALL"
        set logtraffic all
        set nat enable
    next
end
```

configurar rota default
```
config router static
    edit 1
        set dst 0.0.0.0/0
        set gateway 192.168.122.1
        set device "Internet"
    next
end
```


# Configuração VPN Kali

Editar o ficheiro
```
sudo nano /etc/ipsec.conf
```

Copiar a configuração
```
conn VPN
  keyexchange = ikev1

  ike = des-sha1-modp1536
  esp = des-sha1-modp1536

  aggressive = yes

  right = 192.168.122.2
  rightsubnet = 172.16.0.0/12
  rightauth = psk

  left = %defaultroute 
  leftsourceip=%config
  leftauth = psk
  leftauth2 = xauth
  xauth_identity = "labadmin"

  auto = add
```

Editar ficheiro ipsec.secrets
```
sudo nano /etc/ipsec.secrets
```

```
192.168.122.2 %any : PSK "lab1234" 
192.168.122.2 %any : XAUTH "labadmin"
```

Restart ipsec
```
sudo ipsec restart
```
```
sudo ipsec up VPN
```
