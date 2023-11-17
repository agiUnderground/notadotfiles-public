mikrotik get info about connected devices:

`interface/ wireless/ registration-table/ print`

we can use network card drivers to get the `physical length of the cable`(smart link etc.)

test TLS connection:

```openssl s_client --host google.com --port 443```

rshell with nc:

```
    $ rm -f /tmp/f; mkfifo /tmp/f

    $ cat /tmp/f | /bin/sh -i 2>&1 | nc -l 127.0.0.1 1234 > /tmp/f
```

get number of open ports in a wait state:

```ss -a | grep TIME-WAIT | wc -l```

Check what dhcp server gonna respond for a pxe request:

```
user@laptop nmap % sudo nmap -e eth0 -sV --script pxe-check.nse 192.168.34.1 
Starting Nmap 7.94 ( https://nmap.org ) at 2099-00-00 00:00
Pre-scan script results:
| pxe-check: 
|   Response 1 of 1: 
|     Interface: eth0
|     IP Offered: 192.168.34.203
|     IP TFTP Server: 192.168.34.1
|     DHCP Message Type: DHCPOFFER
|     Subnet Mask: 255.255.255.0
|     Router: 192.168.34.1
|     Domain Name Server: 192.168.34.1, 192.168.10.1
|     IP Address Lease Time: 12h00m00s
|_    Server Identifier: 192.168.34.1
```

Show pretty printed dhcp packets:

```sudo dhcpdump -i eth0```

Send a file using netcat(nc):

server - ```nc -l 4444 > testfile.txt```

client - ```cat testfile.txt | pv -bpt -s $(stat -f %z testfile.txt) | nc -N 192.168.122.155 4444```

`-N` option is used to close the socket after EOF appeared in stdin.

Curl using socks:

```curl -x socks5h://localhost:1080 http://ifconfig.me```

Nic statistics:

```
sudo ethtool -S enp69s42
```

Nic statistics example output:
```
NIC statistics:
     tx_packets: 54830
     rx_packets: 26875
     tx_errors: 0
     rx_errors: 0
     rx_missed: 0
     align_errors: 0
     tx_single_collisions: 0
     tx_multi_collisions: 0
     unicast: 21989
     broadcast: 1070
     multicast: 3816
     tx_aborted: 0
     tx_underrun: 0
```

Watch packets flow in realtime:

watch -d -n 0.1 "ethtool -S enp69s42"
```
Every 0.1s: ethtool -S enp69s42

NIC statistics:
     tx_packets: 111106
     rx_packets: 144724
     tx_errors: 0
     rx_errors: 0
     rx_missed: 0
     align_errors: 0
     tx_single_collisions: 0
     tx_multi_collisions: 0
     unicast: 139734
     broadcast: 1080
     multicast: 3910
     tx_aborted: 0
     tx_underrun: 0
```

Just a cool unix tool "column":

```
sudo ethtool -S enp69s42 | column -t -o " <===> "
watch -d -n 0.1 'ethtool -S enp69s42 | column -t -o " <===> "'
watch -d -n 0.1 'tc -g -s qdisc show dev enp69s42'
```

Validate DNS responses with DNSSEC:

```
delv @1.1.1.1 cloudflare.com
```
