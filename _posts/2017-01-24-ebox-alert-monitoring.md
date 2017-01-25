---
published: true
title: Un service fiable et résilient
categories: ebox-alert
tags:
  - ebox-alert
  - monitoring
category: web-development
---
Cet article est le 4e de la [série]({% link _my_categories/ebox-alert.md %}) sur [EBOX Alert][ebox-alert]. Le but de EBOX Alert est de m'éviter d'avoir à surveiller le portail client de EBOX en fin de mois tout en pouvant dormir sur mes deux oreilles, sachant qu'en cas de dépassement de mon forfait internet je serai prévenu. Et comme le service est en plus offert à d'autres abonnés d'EBOX, cela ne peut fonctionner que si le système est vraiment fiable. Si je dois m'assurer manuellement que les alertes ont bien été envoyées, je n'aurai que remplacé un problème par un plus gros.

C'est là que le _monitoring_ (supervision) rentre en jeu. Mais pas seulement le _monitoring_ du site web, certes nécessaire, mais surtout celui du processus de rafraîchissement des données d'utilisation et d'envoi d'alertes _"refresh&alert"_.

### Résilience

La résilience est la capacité à résister aux erreurs et aux pannes. Il existe des frameworks sophistiqués tels que [Netflix/Hystrix](https://github.com/Netflix/Hystrix) mais dans le cas d'EBOX Alert j'ai utilisé une solution adhoc plus simple.

![Architecture EBOX]({{site.baseurl}}/images/EBOX-Architecture.png)


L'exécution du processus _"refresh&alert"_ est déclenchée à intervals réguliers (toutes les minutes) par l'application, et tous les comptes dont les données ont expirées font alors une tentative de mise à jour, avec une alerte en cas de dépassement d'un seuil. Si tout se passe bien pour le compte, la date de prochaine mise à jour _nextRefreshTime_ est calculée en fonction de la priorité du compte. En cas d'erreur imprévue, la date de prochaine mise à jour ne change pas, de façon à ce qu'une nouvelle tentative soit effectuée lors de la prochaine exécution.

Le portail d'EBOX peut aussi renvoyer une erreur de quota de requêtes pour un compte (maximum 5 par heure) ou une page de maintenance avec une heure de retour. Dans ce cas la date de prochaine mise à jour _nextRefreshTime_ est mise à jour en fonction de l'heure renvoyée par EBOX.

Ainsi, pour chaque compte qui doit être mis à jour, il y aura des tentatives environ toutes les minutes jusqu'au succès de la mise à jour et l'alerte potentielle.

Si l'application redémarre, s'interrompt au milieu d'une mise à jour, elle recommence simplement la mise à jour des comptes qui n'ont pas terminé leur mise à jour avec succès.

### Fiabilité

Afin de s'assurer que tous les comptes sont bien mis à jour lorsqu'ils le doivent, et ce même si l'application ne répond plus et ne peut donc envoyer un courriel d'alerte, une solution de _monitoring_ externe est nécessaire. [DeadManSnitch](https://deadmanssnitch.com) propose une solution très simple sous forme d'une URL à appeler régulièrement, un "snitch" (par exemple au moins tous les heures). Si DeadManSnitch ne reçoit pas de notification sur le "snitch" au bout d'une heure, il envoie une alerte (par exemple un courriel). 

Initialement, le "snitch" était appelé après toute mise à jour réussie d'un compte, mais cela n'assure pas que tous les comptes se mettent bien à jour régulièrement. Le design actuel n'appelle le snitch que lorsqu'il n'y a plus aucun compte à mettre à jour. Et une alerte est envoyée si cette situation ne se présente pas pendant 1h d'affillée. 

En pratique, cela peut se produire en cas de situation imprévue avec le portail client d'EBOX (comme c'est arrivé avec les comptes "illimités" dont le total Go ne pouvait être déterminé). Dans ce cas, l'application est corrigée pour faire disparaître l'alerte.

### Conclusion

Grâce à ces mécanismes de gestion des erreurs et de _monitoring_, le site ne nécessite aucune vérification manuelle. Quoiqu'il arrive (à part si DeadManSnitch cesse de fonctionner sans prévenir), je reçois un courriel en cas de problème. Le reste du temps je peux dormir sur mes deux oreilles.


[ebox-alert]: http://www.ebox-alert.ca "ebox-alert.ca"
