
- les philosophes ne font qu'une action a la fois.

- chaque philosophe se voit assigner un numéro entre 1 et le nombre de philosophes

- Quand un philosophe a fini de manger, il repose les fourchettes sur la table et se met à dormir. Une fois réveillé, il se remet à penser. La simulation prend fin si un philosophe meurt de faim.

- ./philo prends 4 ou 5 arguments :

	-  [av[1]]les nombre de philosophe (qui représente aussi les nombre de fourchettes)
	
	-  [av[2]]millisecondes qu'il faut pour qu'un philosophe meurt de faim depuis le dernier repart ou les début de la simulation
	
	-  [av[3]]millisecondes que prends un philosophe a manger (il doit garder les deux fourchette)
	
	-  [av[4]]millisecondes que prends un philosophe a dormir
	
	-  [av[5]]nombre de fois qu'un philosophe dois manger pour que la simulation prenne fin (cette argument n'est pas obligatoire et si il n'est pas donné la simulation s’arrête lors de la mort d'un philosophe)

- Les règles spécifiques a la partie obligatoire sont :

	- Chaque philosophe doit être représenté par un thread.
	
	- Une fourchette est placée entre chaque paire de philosophes. Cela signifie que, s’il y a plusieurs philosophes, chaque philosophe a une fourchette à sa gauche et une à sa droite. S’il n’y a qu’un seul philosophe, il n’y aura donc qu’une seule fourchette sur la table
	
	- Afin d’empêcher les philosophes de dupliquer les fourchettes, vous devez protéger leur état en mémoire avec un mutex pour chacune d’entre elle.