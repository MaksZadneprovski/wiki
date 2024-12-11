
### Шаг 1: Установка OpenVPN и Easy-RSA

1. **Обновите пакеты:**
    
    bash
    
    Копировать код
    
    `sudo apt update sudo apt upgrade`
    
2. **Установите OpenVPN и Easy-RSA:**
    
    bash
    
    Копировать код
    
    `sudo apt install openvpn easy-rsa`
    

### Шаг 2: Настройка PKI (Public Key Infrastructure)

1. **Создайте директорию для Easy-RSA:**
    
    bash
    
    Копировать код
    
    `make-cadir ~/openvpn-ca cd ~/openvpn-ca`



**Инициализируйте PKI:**

bash

Копировать код

`./easyrsa init-pki ./easyrsa build-ca`


```bash
root@v200069594:~/openvpn-ca# ./easyrsa build-ca
Using SSL: openssl OpenSSL 3.0.2 15 Mar 2022 (Library: OpenSSL 3.0.2 15 Mar 2022)

Enter New CA Key Passphrase:
Re-Enter New CA Key Passphrase:
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Common Name (eg: your user, host, or server name) [Easy-RSA CA]:kz

CA creation complete and you may now import and sign cert requests.
Your new CA certificate file for publishing is at:
/root/openvpn-ca/pki/ca.crt
```

./easyrsa gen-req server nopass

```bash
root@v200069594:~/openvpn-ca# ./easyrsa gen-req server nopass
Using SSL: openssl OpenSSL 3.0.2 15 Mar 2022 (Library: OpenSSL 3.0.2 15 Mar 2022)
.+..+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*...+....+......+..+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*...+....+.....+....+..+.........+.+..+.......+...+......+..............+......+.+...+..+...+......+.+......+............+..+...+...+...+.+......+...+..+...+.......+............+.....+.+......+...+...+.....+.........+...+................+..+...+....+..+.........+.+...+...........+....+...+..+...+............+...............+.+.....+.+.....+.+.........+........+.+.........+...+.........+.....+.+..............+.+...+.........+..+..........+...........+...+......+.+...+...........+......+.......+...+..+..........+...........+......+......+.........+................+........+.........+...............+...+....+.....+.+.....+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
...+...+..........+..........................+......+...+.+.........+.....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*...+..+.............+..+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++*.+..+.......+...+........+....+..+.+.........+......+...+..+....+......+.......................+............+....+...+..+.........+....+.....+...+...+.+...+.................+......+..........+.....+...+......+......+..........+...+...............+.....+................+........+......+.........+...+...+......+......+.......+..+......+.......+......+..+............+.+..+.............+..+...+......+..................+.......+.....+.........+.....................+.+..+......................+.........+......+...+...+..+......+.+........+.+..+....+...+..+..........+.....+.+...+............+..+.+.........+......+.....+............+............+.....................+....+..+.........+....+...+...+...........+......+.......+.....+.+.....+.+........+.......+.....+.........+.+.....................+........+.+......+...+.................+.......+.....+......+..........+.........+.....+.+.....+...............+....+...+........+.....................+......+.......+......+............+...+......+...+............+.....+.+..+..........+...+..+...+....+...+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Common Name (eg: your user, host, or server name) [server]:kz

Keypair and certificate request completed. Your files are:
req: /root/openvpn-ca/pki/reqs/server.req
key: /root/openvpn-ca/pki/private/server.key
```

./easyrsa sign-req server server

```bash
root@v200069594:~/openvpn-ca# ./easyrsa sign-req server server
Using SSL: openssl OpenSSL 3.0.2 15 Mar 2022 (Library: OpenSSL 3.0.2 15 Mar 2022)


You are about to sign the following certificate.
Please check over the details shown below for accuracy. Note that this request
has not been cryptographically verified. Please be sure it came from a trusted
source or that you have verified the request checksum with the sender.

Request subject, to be signed as a server certificate for 825 days:

subject=
    commonName                = kz


Type the word 'yes' to continue, or any other input to abort.
  Confirm request details: yes
Using configuration from /root/openvpn-ca/pki/easy-rsa-1843.VeiaZg/tmp.6jevLi
Enter pass phrase for /root/openvpn-ca/pki/private/ca.key:
404757F37F7F0000:error:0700006C:configuration file routines:NCONF_get_string:no value:../crypto/conf/conf_lib.c:315:group=<NULL> name=unique_subject
Check that the request matches the signature
Signature ok
The Subject's Distinguished Name is as follows
commonName            :ASN.1 12:'kz'
Certificate is to be certified until Jan  2 19:43:33 2027 GMT (825 days)

Write out database with 1 new entries
Data Base Updated

Certificate created at: /root/openvpn-ca/pki/issued/server.crt
```

./easyrsa gen-dh


### Шаг 4: Настройка конфигурации OpenVPN

1. **Создайте конфигурационный файл:**
    
    bash
    
    Копировать код
    
    `sudo nano /etc/openvpn/server.conf`
    
    Пример базовой конфигурации:
    
    plaintext
    
    Копировать код
    
```
port 1194
proto udp
dev tun
ca /etc/openvpn/ca.crt
cert /etc/openvpn/server.crt
key /etc/openvpn/server.key
dh /etc/openvpn/dh.pem
server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS 8.8.8.8"
push "dhcp-option DNS 8.8.4.4"
keepalive 10 120
cipher AES-256-CBC
user nobody
group nogroup
persist-key
persist-tun
status openvpn-status.log
verb 3

```


```shell
sudo cp ~/openvpn-ca/pki/ca.crt /etc/openvpn/
sudo cp ~/openvpn-ca/pki/issued/server.crt /etc/openvpn/
sudo cp ~/openvpn-ca/pki/private/server.key /etc/openvpn/
sudo cp ~/openvpn-ca/pki/dh.pem /etc/openvpn/
```

sudo systemctl restart openvpn@server


sudo systemctl enable openvpn@server

### Шаг 6: Настройка клиентских конфигураций

1. **Создайте файл конфигурации для клиента:**
    
    bash
    
    Копировать код
    
    `nano ~/client.ovpn`

### Шаг 8: Настройка брандмауэра (если необходимо)

Если у вас есть активный брандмауэр, откройте порт 1194:

bash

Копировать код

`sudo ufw allow 1194/udp`

конфиг
Чтобы подключить клиент на iOS, выполните следующие шаги:

### 1. Подготовьте сертификаты

Скопируйте файлы `ca.crt`, `client.crt` и `client.key` на ваше iOS-устройство. Вы можете использовать AirDrop, email или облачные сервисы.

### 2. Сгенерируйте клиентский сертификат и ключ

Используйте следующие команды для создания клиентского сертификата и ключа:

bash

Копировать код

`./easyrsa gen-req client nopass ./easyrsa sign-req client client`

### 3. Найдите файлы

После этого файлы `client.crt` и `client.key` должны появиться в директориях `pki/issued` и `pki/private`. Теперь вы можете снова использовать команду `cat`, чтобы открыть их:

bash

Копировать код

`cat ~/openvpn-ca/pki/issued/client.crt cat ~/openvpn-ca/pki/private/client.key`


### Перейдите в папку с Easy-RSA

Убедитесь, что вы находитесь в директории `openvpn-ca`:

bash

Копировать код

`cd ~/openvpn-ca`

### 2. Создайте файл client.ovpn

Если вы хотите избежать ручного копирования, вы можете:

1. **Сохранить все сертификаты и конфигурацию в одном файле**: Вы можете создать единый файл `.ovpn`, который будет содержать и конфигурацию, и сертификаты. Это делается с помощью директивы `inline` в конфиге.

Вот пример, как создать единый файл `.ovpn`, который включает сертификаты:

```
client
dev tun
proto udp
remote 38.180.206.110 1194
resolv-retry infinite
nobind
persist-key
persist-tun

<ca>
-----BEGIN CERTIFICATE-----
# Содержимое ca.crt
-----END CERTIFICATE-----
</ca>

<cert>
-----BEGIN CERTIFICATE-----
# Содержимое client.crt
-----END CERTIFICATE-----
</cert>

<key>
-----BEGIN PRIVATE KEY-----
# Содержимое client.key
-----END PRIVATE KEY-----
</key>

remote-cert-tls server
cipher AES-256-CBC
auth SHA256
comp-lzo
verb 3

```
### Как создать файл

1. Откройте текстовый редактор.
2. Скопируйте и вставьте вышеуказанный код.
3. Вставьте содержимое файлов `ca.crt`, `client.crt` и `client.key` в соответствующие блоки `<ca>`, `<cert>` и `<key>`.

Вы можете открыть файлы `ca.crt`, `client.crt` и `client.key` с помощью текстового редактора в терминале. Вот как это сделать:

1. **Используйте `cat` для отображения содержимого**:
    
    bash
    
    Копировать код
    
    `cat ~/openvpn-ca/pki/ca.crt`
    
    Замените `~/openvpn-ca/pki/` на фактический путь к вашим файлам, если он отличается. Повторите для остальных файлов:
    
    bash
    
    Копировать код
    
```
cat ~/openvpn-ca/pki/issued/client.crt
cat ~/openvpn-ca/pki/private/client.key
```


```
client
dev tun
proto udp
remote 38.180.206.110 1194
resolv-retry infinite
nobind
persist-key
persist-tun

<ca>
-----BEGIN CERTIFICATE-----
MIIDMDCCAhigAwIBAgIUNktSpJEIW5gSRBLmHricMxwtqVswDQYJKoZIhvcNAQEL
BQAwDTELMAkGA1UEAwwCa3owHhcNMjQwOTI5MTkzODI2WhcNMzQwOTI3MTkzODI2
WjANMQswCQYDVQQDDAJrejCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEB
AO8LYnVMbaZVUdR3kAUEBT5RNiWFsATzYVDTKH6PHJdaH/IvzNyDP0yL9XeC0Rj4
GOWKthgLU3NoZ7vsEIo3xk59dEgGgCmrGhKjoa2AL9Yy0sh4qYc98rRm38A7h/BD
nYC3wlvebGQpPxu3GBc6Wcw2/8BrPKeuRQXfXx+FwuBcfcXoCSAvVHTZu9SvDLmD
Iz1fqBdR5Gcdux/sFmoj+39IMVQ66Yr2tCZa1UoFCrk5FCCIZqcTNJjYb+nR23+C
tQ+YjFtdwCCwfjbCeFHpwXy1CAE9xAtP5JoGMpSqBfZ36sOM3DNEWwO0PHEluTt9
1/XxrQBi5eZP0oP2Q6Qxh6MCAwEAAaOBhzCBhDAdBgNVHQ4EFgQUFe/wOb/inBId
eflSxvbMX43NbAswSAYDVR0jBEEwP4AUFe/wOb/inBIdeflSxvbMX43NbAuhEaQP
MA0xCzAJBgNVBAMMAmt6ghQ2S1KkkQhbmBJEEuYeuJwzHC2pWzAMBgNVHRMEBTAD
AQH/MAsGA1UdDwQEAwIBBjANBgkqhkiG9w0BAQsFAAOCAQEAtikhEDS/tEhPvGTv
ld7/uSDkLaIpA/Kj6qKzSdLnDvdAos4mJSiInWdPM90we3yEbW2ZMshJVlCgaugN
7J6koSInxLBAd7vMvA9lTMw41k2RjWDeyC0+GTZmJ2sf9bMbVeYvA5bNV/zDM0c3
LS53/nlpvC2gQoiF4zz56qQcPnEJxBGjsxb2j6dR4ik9vvCLN8O0I2jAzTDTmqQt
96J8decO5Mrn1kNhn/mpKl2fFHinl1pNqv3dqQGb2rmZkxy3xzGmlnVN07PxDieM
7hCrFWRn1KktrPDaLP/pLpjtSJFuQnePZU1bIM3HFwz3psF2CasemxdBf3IGgOD5
HRyZig==
-----END CERTIFICATE-----
</ca>

<cert>
-----BEGIN CERTIFICATE-----
MIIDPzCCAiegAwIBAgIRAItZDH6HbJYCNcv9Dc3cElowDQYJKoZIhvcNAQELBQAw
DTELMAkGA1UEAwwCa3owHhcNMjQwOTI5MjAxNjA1WhcNMjcwMTAyMjAxNjA1WjAN
MQswCQYDVQQDDAJrejCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBALWA
hNL5nPZ+Zv1JJDpMRWllcHGo10VXZnXABxJViGBZbuf8uDj9Z0nTNax44B/vKBQa
b+wcCtDuO/fYjenj94z3S+n0zljMbvIi27/+PJfMivLtgXBVRwcPOawHv0h4Pt1M
bvwJ1sokXp3FL51gHbiGPsqSYregFMV7JIIkkrG2BTaqcIKsTgYM1DgybuSy3weT
HutW5VVJmDY/12IXIx8Xi6vMpUjcQgR7syQuFfyvVtF033OWN+zXN98gZOtx3ls5
HV7A3QYPIz4Zvd1FEo77ZllbzIz2RZYvUG2O6YfabQtIHqA2lkLgjekDlJYg9YGt
Qjs6Yb/v1plGEEniqaUCAwEAAaOBmTCBljAJBgNVHRMEAjAAMB0GA1UdDgQWBBTH
EM2ZesQy5xGp74uz/FS4oq5hKjBIBgNVHSMEQTA/gBQV7/A5v+KcEh15+VLG9sxf
jc1sC6ERpA8wDTELMAkGA1UEAwwCa3qCFDZLUqSRCFuYEkQS5h64nDMcLalbMBMG
A1UdJQQMMAoGCCsGAQUFBwMCMAsGA1UdDwQEAwIHgDANBgkqhkiG9w0BAQsFAAOC
AQEA5UNKBqB4ZhDz6RDdh+yOvqSaPd2ghUFKrCr/vvqtIYRQ1UKaHqHkmxE93P0h
H6sx9OFWHKI0qWl3BwOKHY7o0tIAlvITHebC8iOSCc2KalppflUAetZeVkcosGKf
gkW8HGK54rzdN+ZluA+oepvxHxIgoIaOicEictKmAoJic3jXo05yLfBQQzJFc5oD
1L7DuWFdSDEgjwNfci2QudWrQojqK9O+JqNOXCI6euLlAnXUkGAHNGRGsx2IlERg
jrPwHGINxPrbER4g/TX/t0hzJbJOn5WJRREJ6ObzcYM07vqBjsEG2LCZMLctaoYY
Q6I8fwDzcERulJVl5kDkuthdmA==
-----END CERTIFICATE-----
</cert>

<key>
-----BEGIN PRIVATE KEY-----
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQC1gITS+Zz2fmb9
SSQ6TEVpZXBxqNdFV2Z1wAcSVYhgWW7n/Lg4/WdJ0zWseOAf7ygUGm/sHArQ7jv3
2I3p4/eM90vp9M5YzG7yItu//jyXzIry7YFwVUcHDzmsB79IeD7dTG78CdbKJF6d
xS+dYB24hj7KkmK3oBTFeySCJJKxtgU2qnCCrE4GDNQ4Mm7kst8Hkx7rVuVVSZg2
P9diFyMfF4urzKVI3EIEe7MkLhX8r1bRdN9zljfs1zffIGTrcd5bOR1ewN0GDyM+
Gb3dRRKO+2ZZW8yM9kWWL1BtjumH2m0LSB6gNpZC4I3pA5SWIPWBrUI7OmG/79aZ
RhBJ4qmlAgMBAAECggEAV5dPwm8jAFQNCMQg/x9qygvhwYBNb1HYCRBkeUUc3P6c
BsnP7/TewWJz/ymQY+jrKxR9GfGIiL7H4vq3tf3FrFp14NC7OmBiVGldKqEbhdh4
3/adpmQJNI908iAFAIjDMdIep3RqG0CFBtev/F9zyGbE68bMbDiNfaZJfqL+xlK0
YQ0OOvdXiKDaG1kDloqn8eROjohDNfB9oRy0HUzEcHZ5ZITpMd8zVrEsKlaR9QDi
HhbYe6c/Mce8AcK+08lnMSgGKJ+xuyhUxKPbGJ1SFMXWWIDPV47TK+arhWQSJk2G
1/DJoeARBd2nAaL/ifG3oaCLCRTxgXMw0FlLohHPuwKBgQDl98PTG1Mn7fa90QiU
J/eaOL3CvH8yYMlcws+YQJd5zEmqLUoo7QYB+CyGGZ8Thix7YG1wJ5TQefIpUrw8
X8AG7CxI2GV36FGWOIHbiOBVxxO0nSQ3tROlLNJI14iBv6xUR8v2yNrBJl0+Sra7
VN09CrTX7CGUw9jnYkd6HoRdRwKBgQDKDEOQBQ0qD3yyMNu+56EAzc/AT09Zk7mJ
7G+wuJk4ldRBlr3JTuc30CYdd8au7xu3MRfUOlFYB3LWQdZd/M43TBbkjeLFow1A
UCoTcx6uK4iP2qZu27I/6AkDIjt9s76pktRdqZadEEC4i6OQjqGOZ4RgDGzJIPHt
985ZZzOHswKBgQDifY0uQ8E4mFPlSxTp5hsklzG9s6yKz2xCodOXnjYRzTPYGVbq
y9aY5fXj9SQJNKJmuOfQCAu28AOi00t1ItCbgMt0yzvURsjj7K9oqnxXvwQXZJUh
EIRSr7xD5ZMaRs7RCw1E9zkL9l7rVOZ3xfNHhV3rMzM3s1PTP6YqDhhLTQKBgEQX
5AE6opglRgoryzNIjwtdUYHneL+guKwSAgZWAFWAsVs1eVrJ+8TkoqPVxSEZtoaD
xhshWF7Ji9tHrv5YAAvE2gZHB0FCVWnyWmvZpWJfi5OnxeWgpy9AfSEQPWp81GoD
8Qxr5jWiz50ieopyd2It4wAXz+Xs83wWwvWAgW5fAoGAJGLD7LRQi9et3jFfeYnI
G/NUuPXYy/zY0ZwoqnoV4+qfdVjUwtq/GWTGlNda100tjaITILGd72P6zOCAbsfk
oeOhcCbLIsjtlkw2syvPsOj8bynZS3t28z6/zjBsIf7c3tOb7ODCZdhPfymYbOQP
0MIqfCNI39dGF4PNCr+Mhyk=
-----END PRIVATE KEY-----
</key>

remote-cert-tls server
cipher AES-256-CBC
auth SHA256
comp-lzo
verb 3
```

**Проверка маршрутизации**: Убедитесь, что на сервере включена IP-таблица для пересылки трафика:

В файле `/etc/sysctl.conf` проверьте, что строка:

bash

Копировать код

`net.ipv4.ip_forward=1`

не закомментирована, и выполните:

bash

Копировать код

`sudo sysctl -p`
