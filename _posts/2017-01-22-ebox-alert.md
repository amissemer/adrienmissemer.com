---
layout: post
title: Comment j'évite d'exploser mon forfait internet
published: true
comments: false
---

## ... et comment n'importe quel abonné EBOX peut faire de même en 3 clics

Le lecteur Canadien connaît certainement le fournisseur de service Internet [EBOX](http://ebox.ca). Les tarifs sont intéressants et le service client très correct. Pour moi qui ne cherche qu'une connexion internet décente, sans téléphonie ni télévision par cable, c'est parfait, j'ai pris un forfait 150Go qui suffit amplement à mes besoins et me coûte dans les 40$ par mois.

Cependant, Netflix est passé par là, avec son lot d'excellentes séries, et lors des vacances d'hiver 2015-2016, je me suis fait surprendre à dépasser mon forfait de près d'une centaine de Go. EBOX facture 0,50$/Go jusqu'à un maximum de 50$ (dans mon contrat en tout cas), donc ce mois-ci, ma facture a plus que doublé ! 

Alors bien sûr, chacun est responsable de surveiller sa consommation en utilisant le portail client, mais comme en témoignent plusieurs posts sur le forum d'EBOX, je ne suis pas le seul à regretter qu'EBOX ne fournisse pas un service d'alerte de surconsommation, à l'instar des autres fournisseurs. On peut se demander s'il n'y a pas une stratégie commerciale un peu tordue derrière ce refus, car si j'avais été alerté avant la fin du mois, sans même arrêter de _binge watcher_ House of Cards, j'aurais pu acheter un bloc de consommation supplémentaire pour 5$, et donc économiser 45$ de frais de dépassement (EBOX permet généreusement d'acheter ces blocs jusqu'au dernier jour du mois, même si le forfait est déjà en dépassement).

Comme beaucoup de développeurs, je déteste les tâches routinières comme celle de vérifier où en est mon forfait à la fin de chaque mois (de toutes façons c'est quand je vais oublier de le faire que je vais dépasser). Alors devant ce manque d'un outil d'alerte de surconsommation, j'ai regardé comment d'autres avaient résolu ce problème.

Il existe un plugin pour Chrome qui surveille le portail client, intéressant, mais encore faut-il surveiller l'icone du plugin dans Chrome à la fin du mois. Et le plus gros de ma consommation internet est faite par le Home Cinema sur Netflix, je n'ai donc pas le nez sur mon ordinateur. Idéalement je voudrais être notifié par email voire par SMS.

Je me suis donc lancé dans le développement de ma propre solution, [ebox-alert.ca](http://www.ebox-alert.ca). D'abord pour mon besoin propre, mais je me suis dit, si ça résout mon problème, pourquoi ne pas en faire profiter les autres.

