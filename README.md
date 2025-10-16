gedit client.c
//client.c

#include <stdio.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <string.h>  // for strlen()
#include <stdlib.h>  // for atoi()

int main(int c, char *v[]) {
    int s = socket(AF_INET, SOCK_STREAM, 0), n;
    char b[4096];
    struct sockaddr_in a = {AF_INET, htons(atoi(v[3]))};
    a.sin_addr.s_addr = inet_addr(v[1]);
    connect(s, (void *)&a, sizeof(a));
    write(s, v[2], strlen(v[2]) + 1);
    while ((n = read(s, b, 4096)) > 0)
        write(1, b, n);
}
gcc client.c -o client
./client 127.0.0.1 ex.txt 5003


gedit server.c
//server.c

#include <stdio.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <fcntl.h>
#include <stdlib.h>   // for atoi()

int main(int c, char *v[]) {
    int s = socket(AF_INET, SOCK_STREAM, 0), n, f;
    char b[4096];
    struct sockaddr_in a = {AF_INET, htons(atoi(v[1])), INADDR_ANY};
    bind(s, (void *)&a, sizeof(a));
    listen(s, 1);
    int ns = accept(s, 0, 0);
    read(ns, b, 4096);
    f = open(b, O_RDONLY);
    while ((n = read(f, b, 4096)) > 0)
        write(ns, b, n);
        puts("Transfer Completed");
}

gcc server.c -o server
./server 5003




Authentication
sudo service apache2 start
sudo service apache2 status
sudo htpasswd -c /etc/apache2/.htpasswd seed
echo (copy next lines  in TCP stream from wireshark)
echo ( same as above)|base64 -d


Cookie

<html>
<?php
setcookie("namecookie","netqwerty",time()+123);
setcookie("nickname","work");
?>
<img src= "img7.jpg" width="300" height="300" title="password" />
</html>

*localhost/demo.php(firefox)

persistent:-
1st terminal
Cd /var/www/html
Ifconfig

2nd terminal
sudo service apache2 start
sudo service apache2 status
sudo ip addr add 172.16.10.1/24 dev enp0s3
sudo nano /etc/apache2/apache2.conf
sudo service apache2 restart


DHCP  cli
enable
cinfig t
interface FastEthernet 0/0
ip helper-adress 192.168.2.2
no shutdown
do write memory

<Directory "/var/www/html">
AuthType Basic
AuthName "RESTRICTED"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
</Directory>
