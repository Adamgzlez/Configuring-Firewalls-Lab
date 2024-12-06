# CONFIGURING FIREWALLS LAB

## Objective

The Configuring Firewalls Lab aimed to establish a controlled environment for using firewalld, making zones, adding interfaces, managing zones with ports and protocols, and blocking ips and pings requests to harden the system. This hands on experience was used to help understand firewalls and how to configure them to best them use them to mitigate potential threats as well as filter different bussiness needs considering each group. 

### Skills Learned

- Creating zones for different sectors of bussiness.
- Managing traffic using ports and protocols.
- Blocking ips and ping requests to harden the system.
- Using eth0 to givng each zone interfaces. 

### Tools Used

- Firewalld to make rules.
- Blacklisting to block potential threats.
- Assigning services, ports and protocols to each zone.
- Creating zones within firewalld.
- Assigning designated interfaces to each zone using eth0.
- Virtual Machine (VM).

## Steps

1. Starting and enabling firewalld

Command to start and enable firewalld. This will determine whether or not we have these programs running.

```
$ sudo systemctl enable firewalld 
$ sudo systemctl start firewalld 
```

2. listing all firewalld configured rules

Command to list all current firewalld commands to make appropriate changes. 

```
$ sudo firewall-cmd --list-all
```

3. Creating zones for web, sales, and mail

Command for creating zones. This will allow us to segmennt them into more easily managable areas and control the traffic between each zone.

```
$ sudo firewall-cmd --permanent --new-zone=web
$ sudo firewall-cmd --permanent --new-zone=sales
$ sudo firewall-cmd --permanent --new-zone=mail
```

4. settings zones for their inferfaces and adding services to active zones

Command for setting interfaces to zones. Adding ethernet to the newly created zones.

```
$ sudo firewall-cmd --zone=public --add-interface eth0 --permanent
$ sudo firewall-cmd --zone=web --add-interface eth1 --permanent
$ sudo firewall-cmd --zone=sales --add-interface eth2 --permanent
$ sudo firewall-cmd --zone=mail --add-interface eth3 --permanent
```

Command for adding services to active zones. Adding different ports and protocols. 

Public :

```
$ sudo firewall-cmd zone=public --add-service=http --permanent
$ sudo firewall-cmd zone=public --add-service=pop3 --permanent
$ sudo firewall-cmd zone=public --add-service=smtp --permanent
$ sudo firewall-cmd zone=public --add-service=https --permanent
```

Web :

```
$ sudo firewall-cmd zone=web --add-service=http --permanent
```

Sales :

```
$ sudo firewall-cmd zone=sales --add-service=https --permanent

```

Mail :

```
$ sudo firewall-cmd zone=mail --add-service=smtp --permanent
$ sudo firewall-cmd zone=mail --add-service=pop3 --permanent
```

5. Adding a blacklist of ips to the drop zone

Command for blacklisting ips. Blacklisting ips with malicious intent will protect our network.

```
$ sudo firewall-cmd --permanent --zone=drop --add-source=10.208.56.23
$ sudo firewall-cmd --permanent --zone=drop --add-source=135.95.103.76
$ sudo firewall-cmd --permanent --zone=drop --add-source=76.34.169.118
```

6. Blocking an ip and ping/ICMP requests

Commands for blocking ips using a rich rule and blocking ping/IMCP requests. Blocking ips and ping/ICMP requests will harden our network.

```
$ sudo firewall-cmd --zone=public --add-rich-rule=’rule family=”ipv4” source address=”138.138.0.3” reject’
```

```
$ sudo firewall-cmd --add-icmp-block=echo-reply
$ sudo firewall-cmd --add-icmp-block=echo-request
```

7. Rule checking

Command for rule checking. This makes sure we have made the right changes to the rules.

```
$ sudo firewall-cmd --zone=public --list-all
$ sudo firewall-cmd --zone=sales --list-all
$ sudo firewall-cmd --zone=mail --list-all
$ sudo firewall-cmd --zone=web --list-all
$ sudo firewall-cmd --zone=drop --list-all
```
