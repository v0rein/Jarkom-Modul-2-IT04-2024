# Jarkom-Modul-2-IT04-2024

|Nama  | NRP |
|--|--|
| Dionisius Marcell Putra Indranto | 502723044 |

## Topologi
![image](https://github.com/user-attachments/assets/bbd3962d-1c5e-47fc-b400-5b4ec2e9cdfc)


## IP Addresses
| Device      | Interface | IP Address | Netmask       | Gateway     |
|-------------|-----------|------------|---------------|-------------|
| **Nusantara** | eth0      | DHCP (192.168.122.1)       |               |             |
|             | eth1      | 192.235.1.2| 255.255.255.0 |             |
|             | eth2      | 192.235.2.2| 255.255.255.0 |             |
|             | eth3      | 192.235.3.2| 255.255.255.0 |             |
| **Sriwijaya**| eth0      | 192.235.2.1| 255.255.255.0 | 192.235.2.2 |
| **Tanjungkulai**| eth0     | 192.235.3.3| 255.255.255.0 | 192.235.3.2 |
| **Bedahulu** | eth0      | 192.235.3.4| 255.255.255.0 | 192.235.3.2 |
| **Majapahit** | eth0      | 192.235.3.1| 255.255.255.0 | 192.235.3.2 |
| **Samaratungga** | eth0      | 192.235.1.1| 255.255.255.0 | 192.235.1.2 |
| **Solok**   | eth0      | 192.235.1.3| 255.255.255.0 | 192.235.1.2 |
| **Mulawarman**   | eth0      | 192.244.2.3| 255.255.255.0 | 192.244.2.2 |
| **Alexander Volta**| eth0    | 192.244.2.4| 255.255.255.0 | 192.244.2.2 |
| **Balaraja**   | eth0      | 192.244.2.5| 255.255.255.0 | 192.244.2.2 |
| **Kotalingga**| eth0    | 192.244.2.6| 255.255.255.0 | 192.244.2.2 |



# No. 1
> Untuk membantu pertempuran di Erangel, kamu ditugaskan untuk membuat jaringan komputer yang akan digunakan sebagai alat komunikasi. Sesuaikan rancangan Topologi dengan rancangan dan pembagian yang berada di link yang telah > disediakan, dengan ketentuan nodenya sebagai berikut:
> - DNS Master akan diberi nama Pochinki, sesuai dengan kota tempat dibuatnya server tersebut
> - Karena ada kemungkinan musuh akan mencoba menyerang Server Utama, maka buatlah DNS Slave Georgopol yang mengarah ke Pochinki
> - Markas pusat juga meminta dibuatkan tiga Web Server yaitu Severny, Stalber, dan Lipovka. Sedangkan Mylta akan bertindak sebagai Load Balancer untuk server-server tersebut


On each node, configure network.


### Nusantara (Router)
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.244.1.2
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.244.2.2
	netmask 255.255.255.0
	
auto eth3
iface eth3 inet static
	address 192.244.3.2
	netmask 255.255.255.0
```

### Sriwijaya (DNS Master)
```
auto eth0
iface eth0 inet static
	address 192.235.2.1
	netmask 255.255.255.0
	gateway 192.235.2.2
```

### Majapahit (DNS Slave)
```
auto eth0
iface eth0 inet static
	address 192.235.3.1
	netmask 255.255.255.0
	gateway 192.235.3.2
```

### Tanjungkulai (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.235.3.3
	netmask 255.255.255.0
	gateway 192.235.3.2
```

### Bedahulu (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.235.3.4
	netmask 255.255.255.0
	gateway 192.235.3.2
```

### Kotalingga (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.235.2.6
	netmask 255.255.255.0
	gateway 192.235.2.2
```

### Solok (Load Balancer)
```
auto eth0
iface eth0 inet static
	address 192.235.1.3
	netmask 255.255.255.0
	gateway 192.235.1.2
```

### Samaratungga (Client)
```
auto eth0
iface eth0 inet static
	address 192.235.1.1
	netmask 255.255.255.0
	gateway 192.235.1.2
```

### Mulawarman (Client)
```
auto eth0
iface eth0 inet static
	address 192.235.2.3
	netmask 255.255.255.0
	gateway 192.235.2.2
```

### Alexander Volta (Client)
```
auto eth0
iface eth0 inet static
	address 192.235.2.4
	netmask 255.255.255.0
	gateway 192.235.2.2
```

### Balaraja (Client)
```
auto eth0
iface eth0 inet static
	address 192.235.2.5
	netmask 255.255.255.0
	gateway 192.235.2.2
```

## Check IP address
```
ip a
```
![image](https://github.com/user-attachments/assets/25c4fda2-1f8b-46a1-98a3-1db252afe0f4)
