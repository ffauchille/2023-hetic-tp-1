# TP#1: déploiement d'une application minimale

Ce TP cible les étudiants de l'école HETIC pour le cours d'infrastructure.

Dans ce TP, vous allez:
- Accéder à un serveur distant en utilisant le protocole `ssh`
- Exposer une page web sur internet en utilisant [Nginx](https://www.nginx.com/)

## Étape 1 - Connectez-vous à votre serveur distant

**Objectif**: S'assurrer que vous pouvez accéder en sécurité à votre serveur distant, mis à disposition pour ce TP, depuis votre poste de travail.

Pour cela:
- Téléchargez la clé SSH fournie par votre professeur
- Une fois téléchargée, tapez la commande suivante:

```sh
# Depuis votre terminal favori

# le chemin de la clé peut être relatif or absolue
# assurez-vous de remplacer "etudiant" par votre identifiant
$ ssh -i <chemin_vers_votre_cle_ssh_privee> ubuntu@<etudiant>.floless.fr

# Acceptez le message (apparaît uniquement à la première connexion SSH)
# ...
# Vous devriez être connecté
```

> Note: assurez-vous des droits appliqués à votre clé SSH privée(qu'ils ne soient pas trop ouverts):
> tapez `$ chmod 400 <chemin_vers_votre_cle_ssh_privee>` pour avoir les droits correctement configurés sur votre clé


## Étape 2 - Déployez votre application minimale

**Objectif**: Déployer une simple page web sur internet depuis un serveur fournit pour le TP.

Il s'agit d'écrire une simple page `html` avec votre prénom en titre et votre slogan en texte.

Pour cela:
- Connectez-vous à votre serveur via `ssh`
- Installez [Nginx](https://ubuntu.com/tutorials/install-and-configure-nginx#2-installing-nginx) (votre OS est `ubuntu`):

```sh
sudo apt update
sudo apt install nginx
```

- Assurez-vous de l'accès à la page par défaut `Welcome to nginx!` en visitant l'adresse `http://<etudiant>.floless.fr` depuis votre navigateur(en remplaçant `<etudiant>` par votre identifiant)
- Sur votre poste de travail, créez un nouveau fichier `index.html` file avec:

```html
<!doctype html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>HETIC TP#1</title>
  </head>
  <body>
    <h1>Prénom</h1>
    <p>
      Slogan
    </p>
  </body>
</html>

```
En remplaçant:
- `Prénom` par votre prénom
- `Slogan` par votre slogan d'accroche (soyez inventifs!)

Assurez-vous que votre page `html` est correctement rendue depuis votre poste de travail (en l'ouvrant simplement avec votre navigateur ou en tapant `file://<chemin_vers_votre_fichier_html>` dans la barre d'adresse).

- Déployez votre fichier `index.html` en remplaçant le fichier par défaut d'`Nginx` sur votre machine distante:

```sh
# depuis votre poste de travail; 
# assurez-vous de bien finir la commande par ':'
scp -i <chemin_vers_votre_cle_ssh_privee> <chemin_vers_votre_fichier_html> ubuntu@<etudiant>.floless.fr:
```

- Connectez-vous via `ssh` à votre serveur, et déplacez le fichier `index.html` à la place du fichier `html` par défaut d'`Nginx`:

```sh
# Reportez-vous à l'étape précédente pour vous connecter en ssh
# une fois connecté à votre machine distante:
sudo cp /home/ubuntu/index.html /var/www/html/index.nginx-debian.html 
```

- Avec votre navigateur, vous devriez accéder à votre page web à l'adresse `http://<etudiant>.floless.fr`

Bravo, vous avez déployé une version minimale d'une application web!
