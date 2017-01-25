---
published: false
title: Comment rendre un fiable et résilient
categories: ebox-alert
tags:
  - ebox-alert
  - monitoring
category: web-development
---
Cet article est le 4e de la série sur [EBOX Alert][ebox-alert], 

Le but de EBOX Alert est de m'éviter d'avoir à surveiller le portail client de EBOX en fin de mois tout en pouvant dormir sur mes deux oreilles sachant qu'en cas de dépassement de mon forfait internet je serai prévenu. Et comme le service est en plus offert à d'autres abonnés, cela ne peut fonctionner que si le système est vraiment fiable. Si je dois m'assurer manuellement que les alertes ont bien été envoyées, je n'aurai que remplacé un problème par un plus gros.

C'est là que le monitoring (supervision) rentre en jeu. Mais pas seulement le monitoring du site web, certes nécessaire, mais surtout celui du processus de rafraîchissement des données d'utilisation et d'envoi d'alertes "refresh&alert".

L'exécution du processus "refresh&alert" est déclenchée à intervals réguliers (toutes les minutes) par l'application


![Architecture EBOX]({{site.baseurl}}/images/EBOX-Architecture.png)

[ebox-alert]: http://www.ebox-alert.ca "ebox-alert.ca"
