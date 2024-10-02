# Jarkom-Modul-2-IT04-2024

|Nama  | NRP |
|--|--|
| Dionisius Marcell Putra Indranto | 502723044 |
| Aswalia Novitriasari		   | 5027231012|

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
| **Mulawarman**   | eth0      | 192.235.2.3| 255.255.255.0 | 192.235.2.2 |
| **Alexander Volta**| eth0    | 192.235.2.4| 255.255.255.0 | 192.235.2.2 |
| **Balaraja**   | eth0      | 192.235.2.5| 255.255.255.0 | 192.235.2.2 |
| **Kotalingga**| eth0    | 192.235.2.6| 255.255.255.0 | 192.235.2.2 |



# No. 1
> Untuk mempersiapkan peperangan World War MMXXIV (Iya sebanyak itu), Sriwijaya membuat dua kotanya menjadi web server yaitu Tanjungkulai, dan Bedahulu, serta Sriwijaya sendiri akan menjadi DNS Master. Kemudian karena merasa terdesak, Majapahit memberikan bantuan dan menjadikan kerajaannya (Majapahit) menjadi DNS Slave. 


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

# No. 2
>Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com

## Setup DNS @ Sriwijaya

Update package lists
```
apt-get update -y
```
Install bind9
```
 apt-get install bind9 -y
```
Configure domain in ```/etc/bind/named.conf.local``` file
```
nano /etc/bind/named.conf.local
```
Write the domain configuration in ```/etc/bind/named.conf.local```
```
zone "sudarsana.it04.com" {
	type master;
	file "/etc/bind/it04/sudarsana.it04.com";
};
```
Create /etc/bind/it04 directory
```
mkdir /etc/bind/it04
```
Copy db.local file to it04 folder that was made
```
cp /etc/bind/db.local /etc/bind/it04/sudarsana.it04.com
```
Edit the DNS record
```
nano /etc/bind/it04/sudarsana.it04.com
```
Edit file /etc/bind/it04/sudarsana.it04.com as follows:
```
;
; BIND data file for sudarsana.it04.com
;
$TTL    604800
@       IN      SOA     sudarsana.it04.com. root.sudarsana.it04.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      sudarsana.it04.com.
@       IN      A       192.235.1.3
@       IN      AAAA    ::1
www     IN      CNAME   sudarsana.it04.com
```
- Specify hostname in NS records: sudarsana.it04.com.
- Specify address in A records: 192.235.1.3
- Specify canonical name (alias) in CNAME records: sudarsana.it04.com.


Restart bind9
```
service bind9 restart
```


# No. 3
> Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.

## Setup DNS @ Sriwijaya

Update package lists
```
apt-get update -y
```
Install bind9
```
 apt-get install bind9 -y
```
Configure domain in ```/etc/bind/named.conf.local``` file
```
nano /etc/bind/named.conf.local
```
Write the domain configuration in ```/etc/bind/named.conf.local```
```
zone "pasopati.it04.com" {
	type master;
	file "/etc/bind/it04/pasopati.it04.com";
};
```
Create /etc/bind/it04 directory
```
mkdir /etc/bind/it04
```
Copy db.local file to it04 folder that was made
```
cp /etc/bind/db.local /etc/bind/it04/pasopati.it04.com
```
Edit the DNS record
```
nano /etc/bind/it04/pasopati.it04.com
```
Edit file /etc/bind/it04/pasopati.it04.com as follows:
```
;
; BIND data file for pasopati.it04.com
;
$TTL    604800
@       IN      SOA     pasopati.it04.com. root.pasopati.it04.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it04.com.
@       IN      A       192.235.2.6
@       IN      AAAA    ::1
www     IN      CNAME   pasopati.it04.com
```
- Specify hostname in NS records: pasopati.it04.com.
- Specify address in A records: 192.235.2.6
- Specify canonical name (alias) in CNAME records: pasopati.it04.com.


Restart bind9
```
service bind9 restart
```

# No. 4
> Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com.


## Setup DNS @ Sriwijaya

Update package lists
```
apt-get update -y
```
Install bind9
```
 apt-get install bind9 -y
```
Configure domain in ```/etc/bind/named.conf.local``` file
```
nano /etc/bind/named.conf.local
```
Write the domain configuration in ```/etc/bind/named.conf.local```
```
zone "rujapala.it04.com" {
	type master;
	file "/etc/bind/it04/rujapala.it04.com";
};
```
Create /etc/bind/it04 directory
```
mkdir /etc/bind/it04
```
Copy db.local file to it04 folder that was made
```
cp /etc/bind/db.local /etc/bind/it04/rujapala.it04.com
```
Edit the DNS record
```
nano /etc/bind/it04/rujapala.it04.com
```
Edit file /etc/bind/it04/rujapala.it04.com as follows:
```
;
; BIND data file for rajapala.it04.com
;
\$TTL    604800
@       IN      SOA     rajapala.it04.com. root.rajapala.it04.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      rajapala.it04.com.
@       IN      A       192.235.3.3
@       IN      AAAA    ::1
www     IN      CNAME   rajapala.it04.com
```
- Specify hostname in NS records: rujapala.it04.com.
- Specify address in A records: 192.235.3.3
- Specify canonical name (alias) in CNAME records: rujapala.it04.com.


Restart bind9
```
service bind9 restart
```

# No. 6
> Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).


## Setup DNS @ Sriwijaya

Update package lists
```
apt-get update -y
```
Install bind9
```
 apt-get install bind9 -y
```
Configure domain in ```/etc/bind/named.conf.local``` file
```
nano /etc/bind/named.conf.local
```
Write the domain configuration in ```/etc/bind/named.conf.local```
```
echo "zone \"pasopati.it04.com\" {
    type master;
    file \"/etc/bind/it04/pasopati.it04.com\";
};" >> /etc/bind/named.conf.local

```
Create /etc/bind/it04 directory
```
mkdir /etc/bind/it04
```
Copy db.local file to it04 folder that was made
```
cp /etc/bind/db.local /etc/bind/it04/pasopati.it04.com

```
Edit the DNS record
```
nano /etc/bind/it04/pasopati.it04.com
```
Edit file /etc/bind/it04/rujapala.it04.com as follows:
```
; BIND data file for pasopati.it04.com
$TTL    604800
@       IN      SOA     pasopati.it04.com. root.pasopati.it04.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it04.com.
@       IN      A       192.235.2.6
@       IN      AAAA    ::1
www     IN      CNAME   pasopati.it04.com

```
Add Reverse Zone Configuration: Add the reverse zone to ``` /etc/bind/named.conf.local ``` :
```
nano /etc/bind/named.conf.local
```
Edit File : 
```
zone "2.235.192.in-addr.arpa" {
    type master;
    file "/etc/bind/it04/192.235.2";
};

```
Create the Reverse Zone File: Create the reverse zone file
```
nano /etc/bind/it04/192.235.2
```
edit file :
```
\$TTL    604800
@       IN      SOA     pasopati.it04.com. root.pasopati.it04.com. (
                            2         ; Serial
                       604800         ; Refresh
                        86400         ; Retry
                      2419200         ; Expire
                       604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it04.com.
6       IN      PTR     pasopati.it04.com.
```
Edit the Logging Configuration: Add logging options in ``` /etc/bind/named.conf ```:
```
options {
    directory "/var/cache/bind";

    logging {
        channel default_log {
            file "/var/log/named/bind.log";
            severity info;
            print-time yes;
        };
        category default { default_log; };
    };
};
```
Restart bind9
```
service bind9 restart
```
Ping the Domain: Test the DNS resolution by pinging:
```
ping pasopati.it04.com
ping rujapala.it04.com
```

![Screenshot 2024-10-03 010931](https://github.com/user-attachments/assets/6254789e-aa1e-4b7c-af5f-de33fc7790e3)
masih gagal.

# No. 7
> Akhir-akhir ini seringkali terjadi serangan brainrot ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Majapahit untuk semua domain yang sudah dibuat sebelumnya yang mengarah ke Sriwijaya.

## Setup DNS @ Majapahit

Update package lists
```
apt-get update -y
```
Install bind9 and dnsutils
```
apt-get install bind9 dnsutils -y
```
Edit the DNS configuration in /etc/bind/named.conf.local
```
nano /etc/bind/named.conf.local
```
Add the zones for pasopati.it04.com and rujapala.it04.com as follows:
```
zone "pasopati.it04.com" {
    type slave;
    file "/etc/bind/slave/pasopati.it04.com";
    masters { 192.235.2.6; }; // IP of the DNS Master at Sriwijaya
};

zone "rujapala.it04.com" {
    type slave;
    file "/etc/bind/slave/rujapala.it04.com";
    masters { 192.235.2.6; }; // IP of the DNS Master at Sriwijaya
};

zone "2.235.192.in-addr.arpa" {
    type slave;
    file "/etc/bind/slave/2.235.192.in-addr.arpa";
    masters { 192.235.2.6; }; // IP of the DNS Master at Sriwijaya
};
```
Create a directory to store the slave files
```
mkdir /etc/bind/slave
```
Create /etc/bind/it04 directory
```
mkdir /etc/bind/it04
```
Restart bind9
```
service bind9 restart
```
Verify DNS Slave Configuration
```
named-checkconf
named-checkzone pasopati.it04.com /etc/bind/slave/pasopati.it04.com
named-checkzone rujapala.it04.com /etc/bind/slave/rujapala.it04.com
named-checkzone 2.235.192.in-addr.arpa /etc/bind/slave/2.235.192.in-addr.arpa
```
Test the DNS Slave using nslookup
```
ping pasopati.it04.com
ping rujapala.it04.com
```
![Screenshot 2024-10-02 152218](https://github.com/user-attachments/assets/d1af817d-678f-49c5-9efe-946d381ce0c5)

# No. 8
> Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.

## Setup DNS @ Sriwijaya

Update package lists
```
apt-get update -y
```
Install bind9 and dnsutils
```
apt-get install bind9 dnsutils -y
```
Edit the DNS configuration in /etc/bind/named.conf.local
```
nano /etc/bind/named.conf.local
```
Add the following zone configuration to ``` named.conf.local ``` :
```
zone "cakra.sudarsana.it04.com" {
    type master;
    file "/etc/bind/it04/cakra.sudarsana.it04.com";
};

```
Create /etc/bind/it04 directory
```
mkdir /etc/bind/it04
```
Create the Zone File for the Subdomain

Copy the template DNS record file to the new location:
```
cp /etc/bind/db.local /etc/bind/it04/cakra.sudarsana.it04.com
```
Restart bind9
```
service bind9 restart
```
Edit the DNS Record File

Open the newly created zone file for editing:
```
nano /etc/bind/it04/cakra.sudarsana.it04.com

```
Modify the contents to reflect the DNS records for ``` cakra.sudarsana.it04.com ``` :
```
;
; BIND data file for cakra.sudarsana.it04.com
;
$TTL    604800
@       IN      SOA     cakra.sudarsana.it04.com. root.cakra.sudarsana.it04.com. (
                          1         ; Serial
                      604800         ; Refresh
                       86400         ; Retry
                     2419200         ; Expire
                      604800 )       ; Negative Cache TTL
;
@       IN      NS      cakra.sudarsana.it04.com.
@       IN      A       192.235.2.6     ; IP of Bedahulu

```
Restart bind9
```
service bind9 restart
```
Verify DNS Slave Configuration
```
named-checkconf
named-checkzone cakra.sudarsana.it04.com /etc/bind/it04/cakra.sudarsana.it04.com
```
Test the DNS Slave using nslookup
```
ping cakra.sudarsana.it04.com
```
![Screenshot 2024-10-02 235548](https://github.com/user-attachments/assets/94a62dcf-f489-4867-b6ce-a61efb625538)

