# Jarkom-Modul-2-B16-2023
**Praktikum Jaringan Komputer Modul 2 Tahun 2023**

## Kelompok B16
| Nama | NRP |Github |
|---------------------------|------------|--------|
|Ahmad Fauzan A | 5025211091 | https://github.com/--- |
|Syomeron Ansell W | 5025211540 | https://github.com/Ansell10 |

# Laporan Resmi
## Topologi
![topo](https://github.com/Ansell10/readme/assets/114125933/f9feeb42-f692-49b2-9796-3fae2a119ff4)

## Nomor 1-8
```
#!/bin/bash
echo nameserver 192.168.122.1 > /etc/resolv.conf
apt-get update
apt-get install bind9 -y


echo 'zone "arjuna.B16.com" {
type slave;
masters {192.186.2.2;};
file "/var/lib/bind/arjuna.B16.com" ;
};


zone "abimanyu.B16.com" {
type slave;
masters {192.186.2.2;};
file "/var/lib/bind/abimanyu.B16.com" ;
};

zone "baratayuda.abimanyu.B16.com" {
type master;
file "/etc/bind/baratayuda/baratayuda.abimanyu.B16.com";
};

zone "1.186.192.in-addr.arpa" {
type slave;
masters {192.186.2.2;};
file "/var/lib/bind/1.186.192.in-addr.arpa" ;
};' > /etc/bind/named.conf.local

echo 'options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0'"'"'s placeholder.

        // forwarders {
        //      0.0.0.0;
        // };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options


mkdir /etc/bind/baratayuda

cp /etc/bind/db.local /etc/bind/baratayuda/baratayuda.abimanyu.B16.com

echo '$TTL    604800
@       IN      SOA     baratayuda.abimanyu.B16.com. root.baratayuda.abimanyu.B16.com. (
                         2023101101     ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@               IN      NS      baratayuda.abimanyu.B16.com.
@               IN      A       192.186.1.4
rjp             IN      A       192.186.1.4
www             IN      CNAME   baratayuda.abimanyu.B16.com.
www.rjp         IN      CNAME   baratayuda.abimanyu.B16.com.' > /etc/bind/baratayuda/baratayuda.abimanyu.B16.com

service bind9 restart
```

## Nomer 1
Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut 


## Nomer 2
Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.
![image](https://github.com/Ansell10/readme/assets/114125933/f13e0659-32df-4754-9444-384e37086e4f)
![image](https://github.com/Ansell10/readme/assets/114125933/1253e976-23c9-4f41-b038-0b900c49dab6)

## Nomer 3
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.
![image](https://github.com/Ansell10/readme/assets/114125933/ee7135b8-2d7c-4431-97ec-21ae30adbd83)
![image](https://github.com/Ansell10/readme/assets/114125933/88915d50-15a3-4e3a-901b-fbd195b38022)


## Nomer 4
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.
![image](https://github.com/Ansell10/readme/assets/114125933/f2920e4d-0113-4d69-a9b1-b9d9e9ebbbce)
![image](https://github.com/Ansell10/readme/assets/114125933/fb4b9231-d351-4fcb-b3a3-99da9dc86b1c)


## Nomer 5
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)
![image](https://github.com/Ansell10/readme/assets/114125933/a9cebebc-ec93-4484-9e12-9efead650117)
![image](https://github.com/Ansell10/readme/assets/114125933/bb12d9b5-d5da-4b1d-97f7-36d9188b60d6)


## Nomer 6
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.
![image](https://github.com/Ansell10/readme/assets/114125933/da97fab7-97d0-4815-9bbd-dc35a0d06e4e)


## Nomer 7
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.
![image](https://github.com/Ansell10/readme/assets/114125933/7b7a261a-7752-4bb4-8ea8-8775d2f0f464)


## Nomer 8
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.
![Uploading image.png…]()

