## Procédure d'installation et de configuration des droits d'un serveur de partage de fichiers

#### Installation du rôle et du share:
L'installation se fait de manière classique en rajoutant un rôle de partage de fichier a un serveur via le manager windows serveur

Puis dans l'onglet Share il suffit de faire clic droit dans l'onglet Share puis New share et de parametrer le nom, l'emplacement et toute les options voulues.

![](https://github.com/EpicFail20/quete5/blob/b8912eb035b627efae3284e96c4f5db834b9d34e/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2011-23-01.png)

Puis il suffit de faire un clic droit sur le share nouvellement crée pour avoir l'option de l'ouvrir ou de le parametrer.
La commande Get-SmbShare nous donne les différents partage sur le serveur de fichiers:

![](https://github.com/EpicFail20/quete5/blob/ab12a3a585e6eabdd2bfbfc8023370e690aa44eb/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2011-03-11.png)

On va commencer par modifier les propriétés de tout les autres utilisateurs afin qu'ils n'aient acces au dossier qu'en lecture.

![](https://github.com/EpicFail20/quete5/blob/ab12a3a585e6eabdd2bfbfc8023370e690aa44eb/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2011-33-43.png)

Puis on ouvre le dossier de partage nommé Docs dans cet exemple et on crée les différents sous dossiers RH, comptabilité, et direction avec un simple clic droit nouveau dossier:

![](https://github.com/EpicFail20/quete5/blob/ab12a3a585e6eabdd2bfbfc8023370e690aa44eb/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2011-01-38.png)

Cet exemple nous montre le résultat obtenu. On voit bien que les sous dossiers ont hérités des permissions en lecture de tout les utilisateurs parametrées juste avant.

#### Parametrage des droits particuliers

Afin de limiter les droits des différents sous dossiers on va d'abord créé les différents groupes d'utilisateurs au niveau AD:

![](https://github.com/EpicFail20/quete5/blob/440fd8f37e3858c8f6accbc944f3b95508edf2d9/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2011-46-13.png)

Et on rajoute aussi le client qu'on va utiliser pour tester les permissions

Puis on va rentrer sur chaque dossier dans les différentes options de droits NTFS de chaque dossiers afin de cloisonner les différents groupes:

![](https://github.com/EpicFail20/quete5/blob/2538f171328799755aa955c2e92bd0c2af16e3b3/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2011-52-04.png)

Pour cela il suffit de faire un clic droit sur chaque dossiers puis dans l'onglet sécurité des propriétés du dossier (1) on va cliquer sur "edit" pour ouvrir le panneau suivant (2) et on ajoute le groupe qu'on va autoriser en cliquant sur add puis en le recherchant grâce au panneau (3)

Une fois le groupe ajouter on retourne sur le panneau (2) afin de parametrer les bons droits au groupe que l'on vient d'ajouter.

#### Poste client:

Une fois tout les groupes paramétrés correctement on va configurer un client afin de tester que les droits sont bien effectifs. Pour cela on va commencer par configurer un nouveau lecteur reseau sur le client:

![](https://github.com/EpicFail20/quete5/blob/2538f171328799755aa955c2e92bd0c2af16e3b3/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-26%2021-23-14.png)

Un clic droit sur This pc puis add a network location puis il suffit de lui attibuer une lettre et de rentrer le nom du serveur comme spécifié sur cette screen:

![](https://github.com/EpicFail20/quete5/blob/7e49da2b03696c35d2abfb6dd05dd1828ad72d36/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2012-09-41.png)

Une fois lié le dossier partagé apparait et on peut verifier les droits.
Dans les screens suivantes le client fait parti du groupe RH.

![](https://github.com/EpicFail20/quete5/blob/7e49da2b03696c35d2abfb6dd05dd1828ad72d36/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2011-01-38.png)

On voit qu'il a bien les droits de tout les utilisateurs sur les autres dossiers

Il peut donc aussi lire les fichiers:

![](https://github.com/EpicFail20/quete5/blob/7e49da2b03696c35d2abfb6dd05dd1828ad72d36/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2011-15-25.png)

Mais pas les modifier:

![](https://github.com/EpicFail20/quete5/blob/7e49da2b03696c35d2abfb6dd05dd1828ad72d36/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2011-14-58.png)

Et on voit bien qu'il a comme convenu les bons droits pour son propre dossier:

![](https://github.com/EpicFail20/quete5/blob/08d1582c3cbf69a4e3cb15beac12ab96c1cacbfa/qu%C3%AAte_AD/Capture%20d%E2%80%99%C3%A9cran%20du%202026-04-27%2012-16-17.png)








