
### Qu'est-ce qu'un processus ?

> Un processus est un programme qui s'exécute sur votre ordinateur. Cela peut être n'importe quoi d'une petite tâche de fond, comme un vérificateur orthographique ou un gestionnaire d'événements système à une application à part entière comme Internet Explorer ou Microsoft Word. Tous les procédés sont composés d'un ou plusieurs [[Thread]]

Si vous voulez un exemple plus précis de ce qu'est un processus, vous pouvez cliquer ici [here](https://42-cursus.gitbook.io/guide/rank-02/minitalk/understand-minitalk#processes-and-signals). Laura a créé et montré un bon exemple.

> Étant donné que la plupart [des systèmes d'exploitation](https://techterms.com/definition/operating_system) ont de nombreuses tâches de fond en cours, votre ordinateur a probablement beaucoup plus de processus en cours d'exécution que les programmes réels. Par exemple, vous n'avez peut-être que trois programmes en cours, mais il peut y avoir vingt processus actifs. Vous pouvez visualiser les processus actifs dans Windows en ouvrant le gestionnaire de tâches (appuyez Ctrl-Alt-Delete et cliquez sur Gestionnaire de tâches). Sur un Mac, vous pouvez voir les processus actifs en ouvrant Activity Monitor (dans le dossier Applications-Utilities).

# Qu'est ce qu'un thread ?

les threads d'un programme informatique permettent au programme d'exécuter des actions séquentielles ou plusieurs action a la fois. Chaque fil d'un programme identifie un processus qui s'exécute lorsque le programme le lui demande.

Les threads ont généralement une certaine priorité, ce qui signifie que certains threads ont la priorité sur d'autres. Une fois que le processus a fini de traiter un thread, il peut exécuter le thread suivant qui attend dans la file d'attente.
Cependant, ce n'est pas comme si le thread devait faire la queue à la caisse de la Migros le samedi avant Noël. Les threads doivent rarement attendre plus de quelques millisecondes avant de s'exécuter. Les programmes informatiques qui implémentent le "multithreading" peuvent exécuter plusieurs thread a la fois. La plupart des systèmes d'exploitation modernes prennent en charge le multithreading au niveau du système, ce qui signifie que lorsqu'un programme essaie d'occuper toutes les ressources de votre processus, vous pouvez toujours passer à d'autres programmes et forcer le programme accaparant le processus à partager un peu le processeur.
[source](techterms.com/definition/thread)


# Différence entre les threads et les processus

Les processus et les threads sont des séquences d'exécution indépendantes. La différence typique est que les threads (du même processus) s'exécutent dans un espace mémoire partagé, tandis que les processus s'exécutent dans des espaces mémoire séparés.

## Processus

* Peut avoir plusieurs threads

* Lors de l'utilisation de fork(), duplique tout

	* cela signifie qu'une variable est simplement copiée, si nous modifions la variable dans un processus, elle ne sera pas modifiée dans l'autre 


## Fils

* partager l'espace mémoire

	* si je déclare une variable quelque part et que je la modifie à l'intérieur d'un thread, elle sera également modifiée pour tous les autres threads
	
* peut participer à ce qu'on appelle une "course mémoire"
	* comme la mémoire est partagée entre les threads, si plusieurs threads tentent d'accéder à la même variable en même temps, on parle de "course de mémoire" puisque le thread le plus "rapide" modifiera la valeur de la variable, puis l'autre le fera. Mais la valeur de la première modification pourrait avoir une utilité quelque part.
	* nous devons protéger notre programme contre la "course a la mémoire", comme nous faisons pour les "leak de mémoire"


Vidéo explicative sur les Courses de mémoire ou "race condition" :
https://www.youtube.com/watch?v=FY9livorrJI

# Qu'est ce qu'un mutex (pthread_mutex)

Un mutex est en fait un verrou. Nous pouvons verrouiller une variable afin qu'un seul thread puisse accéder à la fois. Lorsque le premier thread a terminé son opération sur la variable, nous déverrouillons le mutex afin que l'autre thread puisse y accéder.

Vidéo explicative sur mutex :
https://www.youtube.com/watch?v=oq29KUy29iQ


# [[The dining philosophers problem]]