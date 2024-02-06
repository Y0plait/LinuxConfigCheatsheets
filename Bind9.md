# Mise en place et configuration d'un serveur DNS (bind9)

## Sommaire

1. [Installation de bind9](#installation-de-bind9)
2. [Configuration de bind9](#configuration-de-bind9)
3. [Configuration des zones](#configuration-des-zones)
4. [Configuration des enregistrements](#configuration-des-enregistrements)
5. [Vérification de la configuration](#vérification-de-la-configuration)
6. [Configuration du pare-feu](#configuration-du-pare-feu)


## Installation de bind9

Pour installer bind9, il suffit de taper la commande suivante :

```bash
dnf install bind bind-utils
```

## Configuration de bind9

La configuration de bind9 se fait dans le fichier ```/etc/named.conf```. Il est conseillé de faire une sauvegarde de ce fichier avant de le modifier.
```bash
cp /etc/named.conf /etc/named.conf.bak
```

Il va nous falloir notre adresse IP pour configurer le serveur DNS. Pour la connaître, il suffit de taper la commande suivante :
```bash
ip a
```
Notez l'adresse IP de votre carte réseau. La seconde théoriquement, sous la forme ```ensXXX```. Pour la suite, nous allons considérer que l'adresse IP de notre carte réseau est de la forme ```AAA.BBB.CCC.DDD```.

Pour éditer le fichier de configuration, il suffit de taper la commande suivante :
```bash
nano /etc/named.conf
```

Ajouter ces lignes dans le fichier de configuration, dans la partie ```options```:
```bash
options {
        listen-on port 53 { any; };
        listen-on-v6 port 53 { any; };
        allow-query     { any; };

};
```

Supprimer ou commenter les lignes suivantes :
```bash
zone "." IN {
        type hint;
        file "named.ca";
};
```

## Configuration des zones

Ajouter ces lignes à la fin du fichier avant la ligne ```include "/etc/named.rfc1912.zones";``` :
```bash
zone "monnomdefamille.local" IN {
        type master;
        file "/etc/named/zones/monnomdefamille.local.zone";
};

zone "CCC.BBB.AAA.in-addr.arpa" IN {
        type master;
        file "/etc/named/zones/monnomdefamille.local.rev.zone";
};
```

## Configuration des enregistrements

Créer le dossier ```/etc/named/zones``` :
```bash
mkdir /etc/named/zones
```

Créer le fichier ```/etc/named/zones/monnomdefamille.local.zone``` :
```bash
nano /etc/named/zones/monnomdefamille.local.zone
```

Ajouter ces lignes dans le fichier :
```bash
$TTL 86400
@       IN      SOA     ns1.monnomdefamille.local. admin.monnomdefamille.local. (
                        datedujour+01      ; Serial
                        3600            ; Refresh
                        1800            ; Retry
                        604800          ; Expire
                        86400           ; Minimum TTL
)

@       IN      NS      ns1.monnomdefamille.local.
@       IN      A       AAA.BBB.CCC.DDD
www     IN      A       AAA.BBB.CCC.DDD
ns1     IN      A       AAA.BBB.CCC.DDD
```

Créer le fichier ```/etc/named/zones/monnomdefamille.local.rev.zone``` :
```bash
nano /etc/named/zones/monnomdefamille.local.rev.zone
```

Ajouter ces lignes dans le fichier :
```bash
$ORIGIN CCC.BBB.AAA.in-addr.arpa.
$TTL 86400
@       IN      SOA     ns1.monnomdefamille.local. admin.monnomdefamille.local. (
                        datedujour+01      ; Serial
                        3600            ; Refresh
                        1800            ; Retry
                        604800          ; Expire
                        86400           ; Minimum TTL
)

        IN      NS      ns1.monnomdefamille.local.
DDD     IN      PTR     monnomdefamille.local.
```

## Vérification de la configuration

Pour vérifier la configuration, il suffit de taper la commande suivante :
```bash
named-checkconf /etc/named.conf
```

Si la commande ne retourne rien, c'est que la configuration est correcte. Sinon, il faudra corriger les erreurs avant de continuer.
Pour vérifier la syntaxe des fichiers de zone, il suffit de taper la commande suivante :
```bash
named-checkzone monnomdefamille.local /etc/named/zones/monnomdefamille.local.zone
named-checkzone CCC.BBB.AAA.in-addr.arpa /etc/named/zones/monnomdefamille.local.rev.zone
```

Si les commandes ne retournent rien, c'est que la syntaxe des fichiers de zone est correcte. Sinon, il faudra corriger les erreurs avant de continuer.

## Configuration du pare-feu

Pour que le serveur DNS soit accessible depuis l'extérieur, il faut ouvrir le port 53. Pour cela, il suffit de taper la commande suivante :
```bash
firewall-cmd --add-service=dns --permanent --zone=public
firewall-cmd --reload
```

## Conclusion

Le serveur DNS est maintenant configuré. Il ne reste plus qu'à le démarrer et à le configurer pour qu'il démarre automatiquement au démarrage de la machine. Pour démarrer le serveur, il suffit de taper la commande suivante :
```bash
systemctl start named
```

Pour qu'il démarre automatiquement au démarrage de la machine, il suffit de taper la commande suivante :
```bash
systemctl enable named
```

Pour vérifier que le serveur est bien démarré, il suffit de taper la commande suivante :
```bash
systemctl status named
```

Pour tester le serveur, il faut modifier le fichier ```/etc/resolv.conf``` pour qu'il pointe vers le serveur DNS. Pour cela, il suffit de taper la commande suivante :
```bash
nano /etc/resolv.conf
```

Commenter la ligne ```nameserver 1.1.1.1``` et ajouter la ligne ```nameserver AAA.BBB.CCC.DDD```, où ```AAA.BBB.CCC.DDD``` est l'adresse IP de votre serveur DNS.

Pour tester le serveur, il suffit de taper la commande suivante :
```bash
nslookup monnomdefamille.local
```

Si tout est correct, la commande devrait retourner l'adresse IP du serveur DNS. Sinon, pour voir les erreurs, il suffit de taper la commande suivante :
```bash
journalctl -xeu named
```

Pour pouvoir utiliser Internet, il suffit de commenter la ligne ```nameserver AAA.BBB.CCC.DDD``` et de décommenter la ligne ```nameserver 1.1.1.1```.

## Sources

- [https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-centos-7](https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-centos-7)
- [https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how-to-configure-bind-as-a-private-network-dns-server-on-ubuntu-18-04)
- [https://www.tecmint.com/install-and-configure-dns-server-in-centos-7/](https://www.tecmint.com/install-and-configure-dns-server-in-centos-7/)
- [https://www.tecmint.com/install-and-configure-dns-server-in-ubuntu/](https://www.tecmint.com/install-and-configure-dns-server-in-ubuntu/)
