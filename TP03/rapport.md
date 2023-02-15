# INTRODUCTION
 Le site bosch-cyber a été victime d’une attaque informatique et son 
système a été compromis. Les attaquants se serait introduit et aurait 
volé des données très sensibles. Fort heureusement l’administrateur a pu 
isoler la machine compromise afin de faire une enquête sur ce qui s’est 
réellement passé.

## Contexte
 Suite à l’attaque du site bosh-cyber, nous avons été sollicités en tant 
que analyste forensique afin d’enquêter sur le point d’entrée de 
l’attaquant, déterminer les actions effectué ainsi que les données qui 
ont été exfiltré. Par la suite faire un rapport sur l’ensemble de 
l’attaque et de faire des recommandations.

# METHODOLOGY
## Technique

-Premièrement j’ai décidé de savoir quels sont les utilisateurs qui sont 
connectés à mon système pour dans le but de déterminé si l’attaquant a 
eu à ouvrir des sessions pour cela j’ai utilisé les commandes **(w,who et last)**. Qui 
comme le montre l’image qui suit l'historique Nous affiche qu’une seule session de l'utilisateur b0sch 
ouverte à cette date qui est la nôtre **b0sch  2023-02-15 08:40 (172.18.0.1)**.

![alt text](https://github.com/TekHonore/FORENSIC_TP_TEKOUHA_Honore/blob/main/TP03/Images/01%20W%2CWHO%2CLAST.png)

-Par la suite j’ai décidé de faire une analyse de l’ensemble des historiques sur le PC afin de retracer les actions effectuées par l’attaquant en commençant par des commandes qui ont été écrits sur la machine au préalable pour ceux j’ai utilisé la commande **(history)** qui permet d’afficher l’historique des commandes saisie sur le terminal. Il apparaît qu’un ensemble de commande ont été saisie avant la connexion donc n’ont pas été exécuter par nous comme l’illustre l’image en dessous.

![alt text](https://github.com/TekHonore/FORENSIC_TP_TEKOUHA_Honore/blob/main/TP03/Images/Histo2cm.png)


Après analyse de l’ensemble des commandes j’ai remarqué que l’inconnue a effectué exactement 15 commandes parmi les quels j’ai retenue ;
**`cat  /etc/passwd`** L’attaquant a pu avoir accès au fichier (passwd) qui contient les information sur les attributs de chaque utilisateurs.

**`cat  /etc/hosts`** L’attaquant s’est rendu dans le fichier hosts avec la commande qui l’a également permis d’afficher les informations du fichiers hosts.
 
**`ls /var/www/html`** La commande permet à l’attaquant de connaître le contenu des fichiers présent dans le dossier html entre autres le fichier index. 

Ensuite avec la commande **pwd** a permis à l’attaquant d’avoir le chemin d'accès vers le répertoire où il se situe. Puis il a fait un **ping 138.66.89.12** afin de faire un test de connexion 
vers l’adresse 138.77.89.12.

**`cat /etc/shadow`** Qui permet d’ouvrir le fichier shadow ce qui a pu permettre a l’attaquant d’avoir accès au fichier texte contenant les mots de passe des utilisateurs y compris ceux de 
root. Ainsi il pourra les voler

**`ls -lah`** grace a cette commande L’attaquant a par la suite effectuer un listing de façon plus détaillé les fichiers et répertoires contenu dans **/home/b0sh** avec **leurs taille 
permissions et permission d’Access **comme le démontre l’image suivante

![alt text](https://github.com/TekHonore/FORENSIC_TP_TEKOUHA_Honore/blob/main/TP03/Images/03%20LS-LH.png)

**`crontab -e`** Qui permet de crée des taches planifiées dans le but d’effectuer des actions automatiques de façon réguliers (lancer des scripts, des commandes etc…) a des heures spécifiques. 
L’attaquant a donc pu créer ou modifier une tache planifier ou un script.

L’attaquant a par la suite utilisée la commande `zip -r --password $(cat /tmp/mypassword) bosch_cyber_tools.zip 
/home/b0sch/bosch_cyber_tools qui la permis d’archivé les mots de passe présent dans le fichier temporaire et les a enregistré dans ** bosch_cyber_tools** qui se trouve dans /home/b0sch. puis il le deplace dans **opt/leak** avec la commande `mv` et le supprime par la suite avec `rm`. 

![alt text](https://github.com/TekHonore/FORENSIC_TP_TEKOUHA_Honore/blob/main/TP03/Images/04%20bosch%20cyber%20tol.png)



J'ai ensuite acceder au repertoire **/opt/leak** ou est stocke le fichier bosch_cyber_tools.zip
et tempté de le decompressé ce qui etait impossible vue qu'il etait proteger par mot de passe

![alt text](https://github.com/TekHonore/FORENSIC_TP_TEKOUHA_Honore/blob/main/TP03/Images/05%20zipmdp.png)


 
## Les Outils
L'ensemble des outils utilisé :
**fcrackzip** - un crackeur de mot de passe Zip gratuit/rapide

 
 
# RESULTATS
Il apparait que le systeme a bien ete piraté et altére la commande `history`a fait office dindicateur de compromission 
# CONCLUSION
A la suite de lannalyse nous avons decouvert que lataquant cest introduit et a part la suite tempter de dissimuler ces traces.
 
# RECOMMANDATIONS 
# CONCLUSION GENERALE
