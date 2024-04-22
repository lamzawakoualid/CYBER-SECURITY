# CYBER-SECURITY

**Partie 1: Pare-feu iptables**

**Exercice 1:**
1. Pour bloquer tout le trafic entrant par défaut, vous pouvez utiliser la commande :
   ```
   iptables -P INPUT DROP
   ```
2. Pour autoriser uniquement le trafic HTTP entrant sur le port 80, vous pouvez ajouter la règle :
   ```
   iptables -A INPUT -p tcp --dport 80 -j ACCEPT
   ```
3. Pour vérifier les règles iptables, vous pouvez utiliser la commande :
   ```
   iptables -L
   ```

**Exercice 2:**
1. Pour bloquer tout le trafic entrant et sortant par défaut, vous pouvez utiliser :
   ```
   iptables -P INPUT DROP
   iptables -P OUTPUT DROP
   ```
2. Autorisez ensuite les services spécifiés :
   ```
   iptables -A INPUT -s IP_interne -p tcp --dport 22 -j ACCEPT
   iptables -A OUTPUT -p tcp --dport 80 -j ACCEPT
   iptables -A OUTPUT -p tcp --dport 443 -j ACCEPT
   iptables -A OUTPUT -p udp --dport 53 -d  adress -j ACCEPT
   iptables -A INPUT -p icmp --icmp type echo request -j ACCEPT
   iptables -A OUTPUT -p icmp --icmp type echo reply -j ACCEPT

   ```
3. Configurez une règle de journalisation pour enregistrer les paquets rejetés ou acceptés :
   ```
   iptables -A INPUT -j LOG --log-prefix "iptables-rejected: " --log-level 7
   iptables -A OUTPUT -j LOG --log-prefix "iptables-accepted: " --log-level 7
   ```
4. Pour tester la configuration, vous pouvez essayer d'accéder à différents services depuis le réseau local et vérifier les journaux pour les activités autorisées et rejetées.
 

dmesg | grep "ACCEPTED-"
dmesg | grep "REJECTED-"



**Partie 2: Configuration de Snort en mode IDS**

1. Configurez Snort pour utiliser une base de données de règles de la communauté. Vous pouvez le faire en éditant le fichier de configuration de Snort pour spécifier la localisation des règles et les activer.
1.1 include $RULE_PATH/community.rules

   
3. Démarrez Snort en mode écoute pour capturer et analyser le trafic réseau en temps réel. Vous pouvez utiliser la commande :
   ```
   snort -i interface -c snort.conf -A console
   ```
   Assurez-vous de remplacer "interface" par l'interface réseau que vous souhaitez surveiller et "snort.conf" par le chemin vers votre fichier de configuration Snort.

4. Pour simuler des attaques, vous pouvez utiliser divers outils comme Nmap pour les scans de ports, ARP spoofing tools pour l'ARP poisoning, etc. Snort devrait détecter et enregistrer ces attaques dans ses journaux.

