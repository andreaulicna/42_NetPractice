# 42_NetPractise

## To start
```
tar -xf [file_name]
chmod +rwx [file_name]
[browser] [file_name]
```

## Levels
#### Overall levels notes
- to convert to binary quickly: 128, 64, 32, 16, 8, 4, 2, 1

<details>
<summary>Level 1</summary>

##### Goal 1
Starting state:
- host A and host B are on the same network
- subnet mask is ```255.255.255.0``` which translates to ```11111111.11111111.11111111.00000000``` in binary and therefore means that:
	- the first 3 bytes represent the network address
	- the 4th byte represents the host address

Solution:
- the address to change is just that of the host as we are on the same network
- given that it is the 4th byte that represents the host address, the solution is any address between ```104.94.23.0``` and ```104.94.23.255``` except:
	- ```104.94.23.0```: the first number, "0" represents the network
	- ```104.94.23.255```: the last number, "255", is reserved for the broadcast address (used to send information to all the systems on a network)
	- ```104.94.23.12```: already used by host B

##### Goal 2
Starting state:
- host D and host C are on the same network
- subnet mask is ```255.255.0.0``` which translates to ```11111111.11111111.00000000.00000000``` in binary and therefore means that:
	- the first 2 bytes represent the network address
	- the last 2 bytes represent the host address

Solution:
- the address to change is just that of the host as we are on the same network
- given that it is the last 2 byte that represents the host address, the solution is any address between ```211.191.0.0``` and ```211.191.255.255``` except:
	- ```211.191.0.0```: the first number, "0" represents the network
	-```211.191.255.255```: the last number, "255", is reserved for the broadcast address (used to send information to all the systems on a network)
	- ```211.191.81.75```: already used by host C

</details>

<details>
<summary>Level 2</summary>

##### Goal 1
Starting state:
- host A and host B are on the same network
- subnet mask is ```255.255.255.224``` (given for host A and will be copied to host B as a part of the solution) which translates to ```11111111.11111111.11111111.11100000``` in binary and therefore means that:
	- the first 27 bits represent the network address
	- only the last 5 bits represent the host address

Solution:
- the subnet mask should be the same for both hosts and since we can change only that of host B, we copy the value of host A there
- given that it s the last 5 bits that represent the host address, the solution is any address between ```11000000.10101000.00100011.11000000``` and ```11000000.10101000.00100011.11011111```in binary and therefore between ```192.168.35.192``` and ```192.168.35.223``` in decimal, except:
	- ```192.168.35.192```: the first number, "0" represents the network
	- ```192.168.35.223```: the last number, "255", is reserved for the broadcast address (used to send information to all the systems on a network)
	- ```192.168.35.222```: already used by host B

##### Goal 2
Starting state:
- host D and host C are on the same network
- host C's subnet mask is ```255.255.255.252``` which translates to ```11111111.11111111.11111111.11111100``` in binary and therefore means that:
	- the first 30 bits (as specific in host's D subnet mask) represent the network address
	- the last 2 bits represent the host address

Solution:
- given that it is the last 2 bits that represent the host address and we are not given at least one to derive the solution from, the addresses just need to obey this criteria:
	- the first 30 bits (the network address) must be the same for client D and client c
	- they cannot be the same for client D and client C
	- the last 2 bits (that represent the host address) cannot be both 1 nor 0 as the former is the broadcast address and the later is the network address
	- they cannot be among the reserved IP addresses
	- neither address can be 127.0.0.1 as this is a 'special', loopback, address
		- packets sent to this address never reach the network but are looped through the network interface card only
		- it can be used for diagnostic purposes to verify that the internal path through the TCP/IP protocols is working

</details>

<details>
<summary>Level 3</summary>

Starting state
- hosts A, B and C are all on the same network, connected via a switch
- host C's subnet mask is ```255.255.255.128``` which translates to ```11111111.11111111.11111111.10000000``` in binary and therefore means that:
	- the first 25 bits represent the network address
	- the last 7 bits represent the host address

Solution:
- since host C has a subnet mask set and all the hosts are on the same network, their subnet masks should be the same - either ```255.255.255.128``` or ```/27```
- given that it is the last 7 bits that represent the host address, the solution for host A and host B addresses can be any address between ```.01100000``` and ```.01111111``` in binary which translates to address between ```104.198.152.96``` and ```104.198.152.127```, except:
	-```104.198.152.96```: represents the network address
	-```104.198.152.127```: represents the broadcast address
	-```104.198.152.125```: already taken by host A

</details>
