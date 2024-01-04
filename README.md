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

##### Starting state
- hosts A, B and C are all on the same network, connected via a switch
- host C's subnet mask is ```255.255.255.128``` which translates to ```11111111.11111111.11111111.10000000``` in binary and therefore means that:
	- the first 25 bits represent the network address
	- the last 7 bits represent the host address

##### Solution
- since host C has a subnet mask set and all the hosts are on the same network, their subnet masks should be the same - either ```255.255.255.128``` or ```/25```
- given that it is the last 7 bits that represent the host address, the solution for host A and host B addresses can be any address between ```.00000000``` and ```.01111111``` in binary which translates to an address between ```104.198.152.0``` and ```104.198.152.127```, except:
	- ```104.198.152.0```: represents the network address
	- ```104.198.152.127```: represents the broadcast address
	- ```104.198.152.125```: already taken by host A

</details>

<details>
<summary>Level 4</summary>

##### Starting state
- host A and B are on the same network, connected via a switch
- the switch also connects route R with them
	- a route connects multiple networks together, doing so via interefaces for each
- we need to take care only of the communication happening between the router Interface R1 and those of hosts (Interface A1 and Interface B1), so within one network

##### Solution
-  interface R1, A1 nor B1 has a mask setup, and so the choice is on us
	- for simplicity, a mask of increments of 8 can be used as it won't require binary calculation to find the range of suitable addresses
	- mask of ```255.255.0.0``` or ```/16``` can, therefore, do
- interface A1 has an IP address specified and so the first 2 bytes of addresses for Interface B1 and R1 should follow it
	- therefore, their addresses can be any between ```72.96.0.0``` and ```72.96.255.255``` expect:
		- ```72.96.0.0```: represents the network address
		- ```72.96.255.255```: represents the broadcast address
		- ```72.96.116.132```: already taken by interface A1

</details>

<details>
<summary>Level 5</summary>

##### Theory
- interfaces A1 and B1 have routing tables to be completed with:
	- destination:
		- speficies the network address the host is on
		- ```default``` or ```0.0.0.0/0``` address is the route taken when there is no IP destination address provided, sending the packets via the next-hop address
	- next-hop:
		- refers to the closest router (it's IP address) the packets can go via

##### Solution
###### Goal 1
- interface R1 and A1 are on the same network and therefore need to have the same subnet mask of ```255.255.255.128```
- that subnet mask defines that the host address is represented by the last 7 bits (126 in binary is 01111110) and so is between ```.00000000``` and ```01111111``` in binary, translating to between ```18.143.35.0``` and ```18.143.35.127``` in decimal, except:
	- ```18.143.35.0```: represents the network address
	- ```18.143.35.127```: represents the broadcast address
	- ```18.143.35.126```: already taken by interface R1

###### Goal 2
- interface R2 and B1 are on the same network and therefore need to have the same subnet mask of ```255.255.192.0```
- that subnet mask defines that the host address is represented by the last 14 bits (192 = 11000000, 254 = 11111110) and so is between ```.11000000.00000000``` and ```.11111111.11111111``` in binary, translating to between ```153.192.192.0``` and ```153.192.255.255``` in decimal, except:
	- ```153.192.192.0```: represents the network address
	- ```153.192.255.255```: represents the broadcast address
	- ```153.192.192.254```: already taken by the interface R2

###### Goal 3
- since there is only one route that both, A1 and B1, interfaces can send packets via saying ```default``` or ```0.0.0.0/0``` is enough
- the next-hop address needs to equal the IP address of the closest route

</details>

<details>
<summary>Level 6</summary>

##### Theory
- internet behaves like a router
- yet, if an interface is directly or indirectly connected to the internet, its address cannot have the following reserved private IP ranges:
```
192.168.0.0 - 192.168.255.255 (65,536 IP addresses)
172.16.0.0 - 172.31.255.255   (1,048,576 IP addresses)
10.0.0.0 - 10.255.255.255     (16,777,216 IP addresses)
``` 

##### Solution
- match host A's subnet mask to that of the router
- get host masks of interface R1: the subnet mask defines that the host address is defined by the last 7 bits (128 = 10000000, 227 = 11100011) and so is between ```.10000000``` and ```.11111111``` in binary translating to ```75.221.134.128``` and ```75.221.134.255``` in decimal, except:
	- ```75.221.134.128```: represents the network address
	- ```75.221.134.255```: represents the broadcast address
	- ```75.221.134.227```: already taken by host A 
- match next-hop of host A to the router's IP address
- reset the destination of router to default
- set the internet's destination to the network address of host A (calculated in the first step), including the subnet mask in / slash notation (/25) 

</details>

<details>
<summary>Level 7</summary>

##### Theory
- different networks have different ranges of IP addresses
- an overlap in IP address range would imply that the interfaces are on the same network

##### Solution
- the IP addresses of interface R11 and R12 are set and hence this is where we should start - by setting the subnet mask for them
- since the subnet mask defines which part of the IP represents the network and host address, it needs to be set so that the range of addresses for the network the interface R11 is in doesn't overlap with the range of the addresses for the network the interface R12 is in (and then also the 3rd network present)
- possible masks:
	- mask /25 isn't enough as it creates only two ranges:
		- ```.0``` to ```.127```
		- ```.128``` to ```.255```
	- mask /26 (or higher) is more suitable as it creates 4 ranges (including the network and broadcast addresses):
		- ```.0``` to ```.63``` 
		- ```.64``` to ```.127``` 
		- ```.128``` to ```.191``` 
		- ```.192``` to ```.255``` 
- lastly, the next-hop fields need to be setup in this way:
	- each route needs to have the other one's address
	- each host needs to have the address of the router it is connected to
</details>