
# usleep()

```
int usleep(useconds_t usec);
```

`usleep()`est une fonction dans la bibliothèque de normes C qui fait dormir le processus d'appel pendant un nombre spécifié de microsecondes.

```
#include <stdio.h>
#include <unistd.h>

int main(void) {
    printf("Sleeping for 500000 microseconds...\n");
    usleep(500000);
    printf("Done sleeping.\n");
    return 0;
}
```


# gettimeofday()

```
int gettimeofday(struct timeval *restrict tv, struct timezone *restrict tz);
```

La fonction _**gettimeofday()**_ obtient l'heure de l'horloge du système. L'heure actuelle est exprimée en secondes et microsecondes écoulées depuis 00:00:00, janvier 1, 1970 (Unix Epoch).

```
#include <sys/time.h>
#include <stdio.h>

int main() {
  struct timeval current_time;
  gettimeofday(&current_time, NULL);
  printf("seconds : %ld\nmicro seconds : %ld",
    current_time.tv_sec, current_time.tv_usec);

  return 0;
}
```

Le 1er paramètre est un pointeur vers un `timeval` structure. Le `timeval`la structure est définie comme suit dans le `<sys/time.h>`Fichier d'en-tête.

```
struct    timeval  {
  time_t        tv_sec ;   //used for seconds
  suseconds_t       tv_usec ;   //used for microseconds
}
```

Le deuxième argument devrait **toujours** être fixé à `NULL`. Ce deuxième argument est obsolète et n'est là que pour la rétrocompatibilité.

Vous trouverez plus d'informations sur **gettimeofday()** [ici](https://man7.org/linux/man-pages/man2/settimeofday.2.html).




# pthread-create()

```
int pthread_create(pthread_t *restrict thread,
       const pthread_attr_t *restrict attr,
       void *(*start_routine)(void *),
       void *restrict arg);
```

Le `pthread_create()`La fonction démarre un nouveau fil dans le processus d'appel. Le nouveau fil commence l'exécution en invoquant `start_routine()`; `arg`est passé comme seul argument de `start_routine()`.

Vous trouverez plus d'informations sur `pthread_create()`[Ici](https://man7.org/linux/man-pages/man3/pthread_create.3.html).



# pthread-join()

```
int pthread_join(pthread_t thread, void **retval);
```

```
      La fonction pthread_join() attend que le thread spécifié par
       thread à terminer.  Si ce fil est déjà terminé, alors
       pthread_join() renvoie immédiatement.  Le thread spécifié par
       le thread doit pouvoir être joint.
```

Le `pthread_join()`la fonction attend le filetage spécifié par `thread`de mettre fin. Si ce fil s'est déjà terminé, alors `pthread_join()`retours immédiatement.

Attention il ne faut pas confondre cette fonction avec un mutex.
Le mutex veille a ce que un partie du code soit accessible pour un seul thread à la fois alors que "`pthread_join`" sert a bloquer un thread jusqu'à ce que le premier ait terminé son exécution.

```
#include <pthread.h>
#include <stdlib.h>
#include <stdio.h>

void *thread(void *arg) {
  char *ret;
  printf("thread() entered with argument '%s'\n", arg);
  if ((ret = (char*) malloc(20)) == NULL) {
    perror("malloc() error");
    exit(2);
  }
  strcpy(ret, "This is a test");
  pthread_exit(ret);
}

main() {
  pthread_t thid;
  void *ret;

  if (pthread_create(&thid, NULL, thread, "thread 1") != 0) {
    perror("pthread_create() error");
    exit(1);
  }

  if (pthread_join(thid, &ret) != 0) {
    perror("pthread_create() error");
    exit(3);
  }

  printf("thread exited with '%s'\n", ret);
}
```

Dans cet example, nous utilisons la fonction pthread-create() pour créer un nouveau thread qui est initié avec la fonction appelée thread().

On attend alors que le fil se termine avant d'imprimer la valeur de retour du fil.

Vous trouverez plus d'informations sur `pthread_join()`[Ici](https://man7.org/linux/man-pages/man3/pthread_join.3.html).








# pthread-mutex-init()

```
int pthread_mutex_init(pthread_mutex_t *restrict mutex, const pthread_mutexattr_t *restrict attr);
```

Le `pthread_mutex_init()`initialise la fonction mutex référencée par `mutex`avec les attributs spécifiés par `attr`. Si `attr`est `NULL`, les attributs mutex par défaut sont utilisés. Lorsque le `mutex`est initialisé avec succès, l'état mutex devient `initialized`et `unlocked`.

attention a ne pas confondre avec "`pthread_join`" comment expliqué dans le paragraphe concernant la fonction

```
#include <pthread.h>

int main(void)
{
    pthread_mutex_t mutex;

    // Initializing the mutex
    pthread_mutex_init(&mutex, NULL);
}
```

L'exemple ci-dessus utilise le `pthread_mutex_init()`fonction d'initialiser une nouvelle `mutex`qui peut être utilisé à partir de tous les fils que nous voulons.

Vous trouverez plus d'informations sur `pthread_mutex_init()`[Ici](https://man7.org/linux/man-pages/man3/pthread_mutex_destroy.3p.html).




# pthread-mutex-destroy()

```
int pthread_mutex_destroy(pthread_mutex_t *mutex);
```

`The pthread_mutex_destroy()`la fonction détruit l'objet mutex référencé par `mutex`. Le `mutex`un objet devient non initialisé et peut être réinitialisé avec `pthread_mutex_init()`si nécessaire.

```
#include <pthread.h>
#incluce <stdio.h>

int main(void)
{
    pthread_mutex_t mutex;
    
    // Initializing the mutex
    pthread_mutex_init(&mutex, NULL);
    
    printf("You can use the mutex from now on");
    
    // Destroying the mutex
    pthread_mutex_destroy(&mutex);
}
```

Vous trouverez plus d'informations sur `pthread_mutex_destroy()`[Ici](https://man7.org/linux/man-pages/man3/pthread_mutex_destroy.3p.html).








# pthread-mutex-lock()

```
int pthread_mutex_lock(pthread_mutex_t *mutex);
```

Le `pthread_mutex_lock()`fonction verrouille le mutex référencé par `mutex`.

Vous trouverez plus d'informations sur `pthread_mutext_lock()`[Ici](https://man7.org/linux/man-pages/man3/pthread_mutex_lock.3p.html).



# pthread-mutex-unlock()

```
int pthread_mutex_unlock(pthread_mutex_t *mutex);
```

Le `pthread_mutex_unlock()`fonction déverrouille le mutex référencé par `mutex`.

```
#include <pthread.h>
#include <stdio.h>

int main(void)
{
    pthread_mutex_t fork_mutex;
    
    pthread_mutex_init(&fork_mutex, NULL);
    
    pthread_mutex_lock(&fork_mutex);
    set_unavailable(fork);
    pthread_mutex_unlock(&fork_mutex);
    
    pthread_mutex_destroy(&fork_mutex);
    
    return (0);
}
```

Vous trouverez plus d'informations sur `pthread_mutex_unlock()`[Ici](https://man7.org/linux/man-pages/man3/pthread_mutex_lock.3p.html).


[](https://42-cursus.gitbook.io/guide/rank-03/philosophers/functions-used#gettimeofday)