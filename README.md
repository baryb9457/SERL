C'est ci est un guide complète d'installation d'un serveur linux, et un serveur fichier (samba) # librairie samba, avec sécuritésation



# Créer l'utilisateur 'technicien'
sudo adduser technicien

 
	
utilisateur: techinfos psww: techtech
	# Création des dossiers physiques
sudo mkdir -p /home/samba/commun
sudo mkdir -p /home/samba/prive

# Création des groupes Linux
sudo addgroup smb_compta
sudo addgroup smb_public

# Création des comptes Linux
sudo adduser alice
sudo adduser bob

# Ajout aux groupes respectifs
sudo usermod -aG smb_compta alice
sudo usermod -aG smb_public bob

# Création des mots de passe SAMBA (indispensable)
sudo smbpasswd -a alice
sudo smbpasswd -a bob	# Pour le dossier Public
sudo chown -R root:smb_public /home/samba/commun
sudo chmod -R 775 /home/samba/commun

# Pour le dossier Privé (Seul le groupe compta peut entrer)
sudo chown -R root:smb_compta /home/samba/prive
sudo chmod -R 770 /home/samba/prive


# Lui donner le droit d'utiliser 'sudo'
sudo usermod -aG sudo technicien

# Tester : change d'utilisateur sans quitter la session
su - technicien
sudo apt update
# 1. Autoriser SSH (sinon tu vas te couper l'accès)
sudo ufw allow OpenSSH

# 2. Activer le firewall
sudo ufw enable


# 3. Vérifier le statut
sudo ufw status
connecting via ssh:
ssh user@ip_address

longin:
psw: *****

Mise à jour du serveur:
sudo apt update && sudo apt upgrade -y

change name:
sudo hostnamectl set-hostname nouveau nom


seetime:
timedatectl
 
lister les zone disponible
timedatectl list-timzone| gre Paris

installation outils:

sudo apt install -y htop curl wget vim git net-tools
pour voir ( htop)

accéder à la cmd (ipconfig)

Installation des outils indispensable:
sudo apt install -y htop curl wget vim git net-tools

Sécurisation:
fail2Ban (garde du corps)
sudo apt install fail2ban -y
 vérifi du status
sudo systemctl status fail2ban # par defautl il protege le SSH, par ex: bannir quelqu'un pour une période, après 5 tentative de connexion

suppression de utilisateur teste:
sudo deluser --remove-home testssh

Installation de serveur fichier (samba)
sudo apt update
sudo apt isntall samba -y

config de partage sur nano:
sudo nano /etc/samba/smb.conf
[Accuiel]
   path = /home/partage_samba
   browseable = yes
   read only = no
   guest ok = no
   valid users = @smbgroup

Assignation d'utilisateur:

# 1. Créer un groupe spécial pour Samba
sudo addgroup smbgroup

# 2. Ajouter ton utilisateur au groupe (remplace 'ton_user')
sudo usermod -aG smbgroup ton_user

# 3. Définir le mot de passe Samba (il peut être le même que celui de Linux)
sudo smbpasswd -a ton_user




ouverutre de firewall
sudo ufw allow samba
sudo systemctl restart smbd


Autorisation d'accès:
# On change le propriétaire : l'utilisateur 'ton_user' et le groupe 'smbgroup'
sudo chown -R ton_user:smbgroup /home/partage_samba

# On s'assure que le groupe a bien les droits de lecture/écriture
sudo chmod -R 775 /home/partage_samba

# Liste simple
ls

# Liste détaillée (pour voir les tailles, les dates et les permissions)
ls -lh

# Créer un fichier vide
touch salut_windows.txt

# Créer et éditer un fichier avec du texte
nano note.txt
