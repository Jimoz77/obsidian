
imaginons 5 philosophes autour d'une table ronde. Chaque philosophe a devant
lui un bol et entre chaque bol de trouve une fourchette.

La table est constitué comme ceci :

![[Pasted image 20250210191059.png]]


gardons à l'esprit que les philosophe ne peuvent pas communiquer entre eux et ils sont obligé d'utiliser deux fourchette a chaque fois que l un d'entre eux veux manger.

# Deadlock

maintenant imaginons un cas de figure ou tout les philosophes essayent de manger simultanément, ils attrapent tous leur fourchette gauche mais au moment d'attraper la deuxième fourchette a leur droite un blocage ce forme. Aillant tous les fourchette gauche dans la main il ne reste plus aucune fourchette droite pour personne on appel ce phénomène : "Deadlock", quand les philosophe attendent l'un sur l'autre la disponibilité de la ressource : "fourchette" qui créera un boucle d'attente.

# starvation ou famine

L'autre phénomène a éviter est "starvation" ou la famine dont la cause est l'attente trop longue avant de pouvoir remanger.

# Monitoring / waiter

Une solution a ce casse-tête serai l'implémentation d'un moniteur. Dans notre contexte imaginons une sorte de serveur de restaurant.

Comme les philosophe ne peuvent pas communiquer entre eux, un serveur peut gérer et contrôler la situation.

Chaque philosophe va demander la permission pour manger au serveur, le serveur va vérifier que deux fourchette devant le philosophe sont disponible et si c'est le cas lui donner le droit de manger ou au contraire lui interdire. Il va ensuite reposer les fourchette et permettre a ces voisins d'a leur tour faire une demande au serveur qui pourrait être acceptée ou pas.

ce système fonctionnerai si il n'y avait pas le facteur de famine.
en effet les demande sont faites aléatoirement et les mangeur sont ceux dont la demande coïncident avec les fourchette disponibles au moment de la demande.

Pour lutter contre ce facteur on peut donner la priorité de demande au serveur au philosophe qui a le plus faim (celui qui peut le moins attendre) ou celui qui a le plus attendu de tous les philosophes.
