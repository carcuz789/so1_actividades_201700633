# PROBLEMA 1
total de 4 procesos (1 original + 3 nuevos). El número de procesos generados se duplica por cada llamada a fork().

# PROBLEMA 2

Un proceso zombie ocurre cuando un proceso hijo termina su ejecución, pero su proceso padre aún no ha leído su estado de salida (es decir, el padre no ha ejecutado wait()).

```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();

    if (pid < 0) {
        perror("fork failed");
        exit(1);
    } else if (pid == 0) {
        printf(" hijo, mi PID es: %d", getpid());
        exit(0); 
    } else {
        printf("Soy el padre, mi PID es: %d", getpid());
        printf("El hijo se ha convertido en zombie\n");
        sleep(60); 
         // Espera 60 segundos mientras el proceso hijo se convierte en zombie
        // Luego de 60 segundos, el padre recoge el estado del hijo
        wait(NULL);
    }

    return 0;
}

```
Se llama a fork() para crear un proceso hijo.
El proceso hijo imprime su PID y luego termina inmediatamente (exit(0)).
El proceso padre espera 60 segundos antes de llamar a wait(). Durante este tiempo, el hijo permanece en estado zombie.
Finalmente, el padre recoge el estado del hijo con wait().

# PROBLEMA 3


```
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

void *funcion_hilo(void *arg) {
    printf("Soy un hilo, mi ID de hilo es: %ld\n", pthread_self());
    return NULL;
}

int main() {
    pthread_t hilo1, hilo2;
    pid_t id_proceso = fork();  // Crea un proceso hijo

    if (id_proceso == 0) {
        // Código del proceso hijo
        printf("Soy el proceso hijo, mi PID es: %d\n", getpid());
        pthread_create(&hilo1, NULL, funcion_hilo, NULL);  // Crea un hilo en el proceso hijo
        pthread_create(&hilo2, NULL, funcion_hilo, NULL);  // Crea un segundo hilo en el proceso hijo
        pthread_join(hilo1, NULL);
        pthread_join(hilo2, NULL);
    } else if (id_proceso > 0) {
        // Código del proceso padre
        printf("Soy el proceso padre, mi PID es: %d\n", getpid());
    }

    return 0;
}


```