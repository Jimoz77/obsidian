
on commence par initialiser une structure qui regroupe toutes les infos de chaque philosophe.

> `typedef struct s_philo`
> `{`
> 	`int id;`
> 	`int left_fork;`
> 	`int right_fork;`
> 	`int eat_count;`
> 	`pthread_t thread;`
> `} t_philo;`

puis on a besoin d'initialiser toutes ces valeurs pour tous les philosophes
le nombre de philosophe est spécifié par `av[1]` 

pour cela nous allons créer la fonction "init_philo" qui prend uniquement un int en parametre qui représente le nombre de philosophe a initialiser donc `av[1]`

### la fonction sera prototypé de cette façon :

> `t_philo *init_philo(int nb)`
> `{`
> 	`t_philo *philo;`
> 	`int i;`
> 	
> 	`i = 0;`
> 	`philo = malloc(sizeof(t_philo) * nb);`
> 	`if (!philo)`
> 		`return (NULL);`
> 	`while (i < nb)`
> 	`{`
> 		`philo[i].id = i;`
> 		`philo[i].left_fork = i;`
> 		`philo[i].right_fork = (i + 1) % nb;`
> 		`philo[i].eat_count = 0;`
> 		`i++;`
> 	`}`
> 	`return (philo);`
> `}`


left_fork est initialisé a "`i`" car chaque philosophe prend la fourchette a sa gauche, qui est représenté par son propre index "`i`"

et right_fork est initialisé a "`(i + 1) % nb`" car chaque philosophe prends la fourchette a sa droite, qui est représenté par l'index "`(i + 1)`".
L'opérateur "`% nb`" assure que le dernier philosophe (a l'index "`nb - 1`") prends la première fourchette (index "`0`") comme sa fourchette droite, créant ainsi une disposition circulaire 

la variable "`pthread_t thread`" représente le thread associé a chaque philosophe.
Dans le contexte du problème des philosophe mangeurs, chaque philosophe est modélisé comme un thread séparé. cela permet a chaque philosophe d'exécuter ses actions (manger, penser ou dormir) de manière concurrente et indépendante des autres philosophes.

la variable "`pthread_t thread`" stocke l'identifiant du thread créé pour chaque philosophe.

### Comment la variable "`pthread_t thread`" est initialisée :

1. **Création du thread** : pour chaque philosophe, un thread est créé en utilisant la fonction "`pthread_create()`". Cette fonction prends un pointeur vers une variable "`pthread_t`" (ici "`thread`") pour stocker l'identifiant du thread nouvellement créé.
2. **Exécution du thread** : le thread exécute une fonction spécifique qui contient la logique des actions du philosophe(manger, penser ou dormir).
3. **Gestion du thread** : L'identifiant du thread (stocké dans thread) peut être utilisé pour diverses opérations, comme attendre la fin du thread avec "`pthread_join()`", ou annuler le thread avec "`pthread_cancel()`" 

voici un exemple de comment cela pourrait être utilisé dans le code :

`void *philosopher_routine(void *arg)
`{`
	`t_philo *philo = (t_philo *)arg;`
	`// Logique du philosophe (penser, manger, etc)`
	`return (NULL);`
`}`

`int main (int ac , char **av)`
`{`
	`t_philo *philos;`
	`int     nb;`
	`int     i;`
	
	i = 0;
	if (ac == 5 || ac == 6)
	{
		nb = ft_atoi(av[1]);
		philos = init_philo(nb);
		while(i < nb)
		{
			pthread_create(&philos[i].thread, NULL, philosopher_routine, &philos[i]);
			i++;
		}
		i = 0;
		while (i < nb)
		{
			pthread_join(philos[i].thread, NULL);
			i++;
		}
		free(philos);
	}
	`return (0);`

`}`



