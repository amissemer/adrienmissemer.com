---
layout: post
title: Comment j'évite d'exploser mon forfait internet
published: true
comments: false
category: web-development
tags:
  - ebox-alert
---

## ... et comment n'importe quel abonné EBOX peut faire de même en 3 clics

Le lecteur Canadien connaît certainement le fournisseur de service Internet [EBOX](http://ebox.ca). Les tarifs sont intéressants et le service à la clientèle très correct. Pour moi qui ne cherche qu'une connexion internet décente, sans téléphonie ni télévision par cable, c'est parfait, j'ai pris un forfait 150Go qui suffit amplement à mes besoins et me coûte dans les 40$ par mois.

Cependant, Netflix est passé par là, avec son lot d'excellentes séries, et lors des vacances d'hiver 2015-2016, je me suis fait surprendre à dépasser mon forfait de près d'une centaine de Go. EBOX facture 0,50$/Go jusqu'à un maximum de 50$ (dans mon contrat en tout cas), donc ce mois-ci, ma facture a plus que doublé ! 

Alors bien sûr, chacun est responsable de surveiller sa consommation en utilisant le portail client, mais comme en témoignent plusieurs posts sur le forum d'EBOX, je ne suis pas le seul à regretter qu'EBOX ne fournisse pas un service d'alerte de surconsommation, à l'instar des autres fournisseurs. On peut se demander s'il n'y a pas une stratégie commerciale un peu tordue derrière ce refus, car si j'avais été alerté avant la fin du mois, sans même arrêter de _binge watcher_ House of Cards, j'aurais pu acheter un bloc de consommation supplémentaire pour 5$, et donc économiser 45$ de frais de dépassement (EBOX permet généreusement d'acheter ces blocs jusqu'au dernier jour du mois, même si le forfait est déjà en dépassement).

Comme beaucoup de développeurs, je déteste les tâches routinières comme celle de vérifier où en est mon forfait à la fin de chaque mois (de toutes façons c'est quand je vais oublier de le faire que je vais dépasser). Et je déteste également être pris pour un pigeon. Alors devant ce manque d'un outil d'alerte de surconsommation, j'ai regardé comment d'autres avaient résolu ce problème.

Il existe deux extensions EBOX pour Chrome [ici](https://chrome.google.com/webstore/detail/electronic-box-internet-u/naddhcamlnfbidmhpfnkfcekjhdjelia?hl=fr) et [ici](https://chrome.google.com/webstore/detail/bandwidth-monitoring-for/hhobonigdddkgbnmhapcihbilefoaifd?hl=fr) qui surveillent le portail client. Intéressant, mais encore faut-il surveiller l'icone de l'extension dans Chrome ou les notifications du bureau avant la fin du mois. Le plus gros de ma consommation internet est faite par mon _home cinema_ sur Netflix, je n'ai donc pas le nez sur mon ordinateur à ce moment là ni nécessairement à la fin du mois. Idéalement je voudrais être notifié par courriel, voire par SMS.

Je me suis donc lancé dans le développement de ma propre solution, qui est devenue [EBOX Alert][ebox-alert]. D'abord pour mon besoin propre, mais je me suis dit : si ça résout mon problème, pourquoi ne pas en faire profiter les autres ?

Le principe de fonctionnement de [EBOX Alert][ebox-alert] est relativement simple et similaire au fonctionnement de l'extension EBOX pour Chrome : EBOX ne fournit aucune API de suivi de la consommation, mais fournit un [portail](http://conso.ebox.ca) qui ne requiert aucune authentification et ne nécessite que le code client, à entrer dans un formulaire très simple. Il n'y a pas vraiment besoin de sécurité en effet vu que les informations accessibles sont anonymes et ne concernent que l'utilisation du forfait. Donc avec le code client, il est possible de parser la page HTML et obtenir les informations souhaitées sur le forfait et la consommation.

Comme je veux être prévenu même lorsque mon ordinateur est éteint, il me faut utiliser un serveur quelque part ailleurs, vérifier le portail périodiquement, et envoyer un courriel ou un SMS lorsque l'un des seuils de consommation est atteint. Rien de bien sorcier.

Évidemment là où cela se complique, c'est pour fournir le service à d'autres clients EBOX, car EBOX se protège contre les petits malins qui veulent faire exactement cela. Je vous raconte ça dans le [prochain article]({% post_url 2017-01-22-ebox-alert-2 %}).


[ebox-alert]: http://www.ebox-alert.ca "ebox-alert.ca"
