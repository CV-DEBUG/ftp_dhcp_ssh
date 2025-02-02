## 1. **Configuration DHCP avec Kea DHCP**
Cette section explique comment installer et configurer un serveur **DHCP** avec **Kea DHCP**. Elle inclut la configuration des sous-réseaux, des pools d'adresses IP et des options DHCP.

- **Points clés :**
  - Installation de Kea DHCP : `sudo apt install kea-dhcp4-server -y`
  - Configuration dans `/etc/kea/kea-dhcp4.conf`.
  - Exemple de configuration pour un sous-réseau :
    ```json
    "subnet4": [
        {
            "subnet": "172.20.0.0/16",
            "pools": [ { "pool": "172.20.0.10 - 172.20.0.50" } ],
            "option-data": [ { "name": "domain-name-servers", "data": "172.20.0.5" } ]
        }
    ]
    ```
  - Redémarrage du service : `sudo systemctl restart kea-dhcp4-server.service`

---

## 2. **Configuration SSH avec OpenSSH** 
Cette section explique comment installer et configurer un serveur **SSH** sécurisé avec **OpenSSH**. Elle inclut des options pour restreindre l'accès, changer le port SSH et interdire les connexions root.

- **Points clés :**
  - Installation d'OpenSSH : `sudo apt install openssh-server`
  - Configuration dans `/etc/ssh/sshd_config` :
    - Restriction des utilisateurs : `AllowUsers laplateforme`
    - Changement du port SSH : `Port 6500`
    - Interdiction des connexions root : `PermitRootLogin no`
  - Redémarrage du service : `sudo systemctl restart ssh`

---

## 3. **Configuration FTP avec vsftpd** 
Cette section explique comment installer et configurer un serveur **FTP** sécurisé avec **vsftpd**. Elle inclut des options pour restreindre l'accès anonyme, configurer les permissions des fichiers et limiter les connexions.

- **Points clés :**
  - Installation de vsftpd : `sudo apt install vsftpd -y`
  - Configuration dans `/etc/vsftpd.conf` :
    - Désactivation de l'accès anonyme : `anonymous_enable=NO`
    - Restriction des utilisateurs : `chroot_local_user=YES`
    - Limitation des connexions : `max_per_ip=10`, `max_clients=20`
  - Redémarrage du service : `sudo systemctl restart vsftpd`

---

## 4. **Configuration DNS avec BIND9**
Cette section explique comment installer et configurer un serveur DNS avec **BIND9**. Elle inclut la création de zones DNS, la configuration des enregistrements NS et A, ainsi que la configuration des options DNS.

- **Points clés :**
  - Installation de BIND9 : `sudo apt install bind9 -y`
  - Configuration des zones DNS dans `/etc/bind/zones/db.ftp.com`.
  - Configuration des options DNS dans `/etc/bind/named.conf.options`.
  - Redémarrage du service : `sudo systemctl restart bind9`

---

## 5. **Configuration d'une Adresse IP Statique**
Cette section montre comment configurer une **adresse IP statique** sur une interface réseau. Cela est utile pour les serveurs qui nécessitent une IP fixe.

- **Points clés :**
  - Configuration de l'interface réseau dans `/etc/network/interfaces`.
  - Exemple de configuration :
    ```bash
    auto ens33
    iface ens33 inet static
    address 172.16.0.10
    netmask 255.255.0.0
    ```

---
