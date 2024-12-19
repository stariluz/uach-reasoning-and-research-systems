# Busqueda local del templado simulado

La busqueda en templado simulado incorpora algo nuevo la alabriedad. El bipálo simulado es un estilo de búsqueda local que mejora algo nuevo.
> Se puede cambiar a un nuevo estado que es "por" al anterior, así se en lo queda atrasado en el primer óptimo local que el proceso encuentre.

Esto asegura que almenos en las primeras etapas del proceso de busqueda el proceso se quede atorado en el primer óptimo ideal, y al contrario, busque 2 óptimos locales con la esperanza de que este este sea un óptimo global. 
Sin embargo es una técnica de búsqueda local, eventualmente se quedará en un óptimo local, lo que sucede es que no lo hará en el primer óptimo local que encuentre, se detendrá más adelande en el proceso pero no al inicio.

### Temperatura del proceso
Para controlar aquello de cambiarse a un estado peor al acttual para no "atorarse" en el primer óptimo local, de manera que:

> Cambiarse a un estado peor que el actual es algo que ocurre mucho al inicio de la búsqueda, pero menos al final de la misma.
Así, conforme pasa el tiempo y aquello

Para controlar aquello de cambiarse a un estado peor al actualmás al inicio de la búsqueda, pero menos hacia el final, el templado simulado utiliza la temperatura del proceso (t), esta temperatura inicia con cierto valor inicial y con cada iteración disminuye, y solo cuando alcance un valor mínimo detendremos el proceso.
```py
t=t_ini
while t>=t_min:
    # Change state
    t=α_t #

```
Obviale que $0 \leq α \lt 1$, y sirve como factor para disminuir la temperatura en cada iteración. ¿Cuándo debe valer $α$? basta con conocer que:
1. $α \to 0$: habrlán muchas iteraciones y el proceso fluye suavemente pero lento
2. $ α \to 1$: habrán menos iteraciones pero el proceso fluctúa mucho y quizá no vconverga.
Normalmente se aconseja $α \to 0.5$. Por otro lado y puesto que templado simulado es una técnica de búsqueda local, procede en cada iteración así:
* Formar la vencindad del estado actual
* traer al mejor estado de la vecindad llamese nuevo
* Si el nuevo es mejor al actual:
  * Hacer el nuevo el estado actual
