# gasmask

gasmask is a shell script written for Bash 3.2+ that can help you configure network settings.  

gasmask is a Bash-written copy of [Whatmask](http://www.laffeycomputer.com/whatmask.html). You can find more information about the `whatmask` utility at this website: http://www.laffeycomputer.com/whatmask.html

## Installation
To install `gasmask`, simply clone this repository and symlink, copy, or move the script into a directory that is in your `$PATH`.  

`git clone https://github.com/kbelleau/gasmask.git`  

## Usage
gasmask has two modes. In both modes, `gasmask` will only acknowledge the first argument entered with the command. Additionally, one argument is always required with the gasmkask script.  

The first mode is used by invoking `gasmask` with only a subnet mask as an argument. In this mode, gasmask will echo back the subnet mask in four formats, plus the number of usable addresses in the subnet's range.  

gasmask notations supported:  
| Name          | Example       |
|---------------|---------------|
| CIDR          | /24           |
| Netmask       | 255.255.255.0 |
| Netmask (hex) | 0xffffff00    |
| Wildcard Bits | 0.0.0.255     |

The above notations are all identical. CIDR notation commonly has a slash ("/") in front of it, but gasmask can accept CIDR values with or without a slash.  

To use gasmask in its second mode, invoke `gasmask` with any IP address within the subnet, followed by a slash ("/"), followed by the subnet mask in any format. Be sure to not include any spaces in this string.  

gasmask will echo back all information from the first mode, and additionally the network address, broadcast address, and first+last usable IP addresses.  

(gasmask assumes that the broadcast address is the highest address in the subnet, which is the most common configuration.)

## Examples

```
➞ $ gasmask /26

---------------------------------------------
       TCP/IP SUBNET MASK EQUIVALENTS
---------------------------------------------
CIDR = .....................: /26
Netmask = ..................: 255.255.255.192
Netmask (hex) = ............: 0xffffffc0
Wildcard Bits = ............: 0.0.0.63
Usable IP Addresses = ......: 62

```

```
➞ $ gasmask 255.255.192.0

---------------------------------------------
       TCP/IP SUBNET MASK EQUIVALENTS
---------------------------------------------
CIDR = .....................: /18
Netmask = ..................: 255.255.192.0
Netmask (hex) = ............: 0xffffc000
Wildcard Bits = ............: 0.0.63.255
Usable IP Addresses = ......: 16,382
```

```
➞ $ gasmask 192.168.0.113/0xffffffe0

------------------------------------------------
           TCP/IP NETWORK INFORMATION
------------------------------------------------
IP Entered = ..................: 192.168.0.113
CIDR = ........................: /27
Netmask = .....................: 255.255.255.224
Netmask (hex) = ...............: 0xffffffe0
Wildcard Bits = ...............: 0.0.0.31
------------------------------------------------
Network Address = .............: 192.168.0.96
Broadcast Address = ...........: 192.168.0.127
Usable IP Addresses = .........: 30
First Usable IP Address = .....: 192.168.0.97
Last Usable IP Address = ......: 192.168.0.126
```

```
➞ $ gasmask 192.168.0.169/0.0.0.127

------------------------------------------------
           TCP/IP NETWORK INFORMATION
------------------------------------------------
IP Entered = ..................: 192.168.0.169
CIDR = ........................: /25
Netmask = .....................: 255.255.255.128
Netmask (hex) = ...............: 0xffffff80
Wildcard Bits = ...............: 0.0.0.127
------------------------------------------------
Network Address = .............: 192.168.0.128
Broadcast Address = ...........: 192.168.0.255
Usable IP Addresses = .........: 126
First Usable IP Address = .....: 192.168.0.129
Last Usable IP Address = ......: 192.168.0.254
```