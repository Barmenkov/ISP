# ISP
```
configure
int gi1/0/1
ip address dhcp
ip firewall disable

int gi1/0/3
ip address 172.16.4.1/28
ip firewall disable
no shutdown

int gi1/0/2
ip address 172.16.5.1/28
ip firewall disable
no shutdown

commit
confirm
```
```
object-group network LOCAL_NET
  ip address-range 172.16.5.1-172.16.5.2
  ip address-range 172.16.4.1-172.16.4.2
exit

nat source
  ruleset SNAT
    to interface gigabitethernet 1/0/1
    rule 1
      match source-address LOCAL_NET
      action source-nat interface
      enable
    exit
  exit
exit
```
