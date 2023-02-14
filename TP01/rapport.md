# Contexte
Alors qu'il se reposait près du parking du poste de police, un policier a trouvé une clé USB par terre. Par conséquent, il a décidé d'apporter cette clé au service d'analyse.

# Introduction
Il nous est demander de ce positionner en tant que spécialiste en forensique afin de déterminez de manière technique si la clé est malveillante avant de la connecter à votre ordinateur. 

# Méthode
A partir du hash donne j'ai choisi tout d’abord de faire une comparaison du hash de l’image en sha256sum USB_Image sur un site web spécialisée appelé virus total J’ai donc comparé le hash qui a été préalablement donné 
(a6fd7b3072187b2b6a31119f4580e58d5219fef157514c28d2de6df5ecf3185c) Avec la liste des hash malveillant connue grâce à virus total ce qui n’a rien donné. Toujours avec virus total j’ai essayé de scanner le fichier entier mais 
l’élément était trop volumineux.
![alt text](https://github.com/TekHonore/FORENSIC_TP_TEKOUHA_Honore/blob/main/TP01/Icones%20tp/HASHs.png)
![alt text](https://github.com/TekHonore/FORENSIC_TP_TEKOUHA_Honore/blob/main/TP01/Icones%20tp/fichier%20vT.png)

jai également essayer de verifier les proprieté du fichier qui ma 
revéle que limage est un Executable
![alt text](https://github.com/TekHonore/FORENSIC_TP_TEKOUHA_Honore/blob/main/TP01/Icones%20tp/Propri%C3%A9te%20de%20limage%20usb.png)
jai continué par une analyse du fichier avec la command "file" 
![alt text](https://github.com/TekHonore/FORENSIC_TP_TEKOUHA_Honore/blob/main/TP01/Icones%20tp/INFO%20File.png)
ce qui ma revelé que le fichier est un "DOS/MBR boot sector" qui signifie que le fichier est un executable bootable il est aussi mentionné quil ya des secteurs disimulé "hidden sectors 2048"

J’ai décidé de procédé différemment avec la commande ' minfo -i usb.dd'
